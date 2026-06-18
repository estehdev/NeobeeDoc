# Development cycle & build process — team guide

This document describes how building and publishing Docker images works after the move to the
new system. It applies to all migrated services (MoUser, MoSafewatch, MoCompany, MoLlm, …) —
the workflow is the same; only the image name differs.

## Key change

- **A production build is NO LONGER triggered by committing to `application.properties`.**
- Production is published **only by creating a GitHub Release** on a `vX.Y.Z` tag.
- The version is no longer maintained by hand in a file — **the git tag is the single source of truth**.

## Build channels

| Channel | Trigger | Docker tags |
|---------|---------|-------------|
| **dev** | push to `main` (or `master`) | `dev`, `dev-<version>`, `dev-3`, `dev-3.65` |
| **feat** | manual (`workflow_dispatch`) from any branch | `feat-<name>` |
| **rc / staging** | GitHub Release marked *pre-release* on `vX.Y.Z-rc.N` | `rc-<version>-<n>`, `staging` |
| **prod** | published GitHub Release on `vX.Y.Z` | `prod-X.Y.Z`, `prod`, `prod-3`, `prod-3.65` |

> `dev-<version>` looks like `dev-3.65.4-5-gabc123` (last release + commit count + sha), produced
> by `git describe`. Before the first `v*` tag exists, it falls back to `dev-<sha>`.

## Versioning — `vX.Y.Z`

- We use **semantic versioning** with a `v` prefix: `v3.65.5`.
- `X` = major, `Y` = minor, `Z` = patch.
- A full release tag must be clean semver (`v3.66.2`). Tags like `v3.66.2-beta` published as a
  **full** release are rejected — use a pre-release flag or a clean tag.

---

## 1. Day-to-day work (dev)

Nothing special — **just push/merge to `main`**. CI automatically:
- builds and publishes the image with tags `dev`, `dev-<git-describe>`, `dev-3`, `dev-3.65`.
- derives the version from git (you don't touch `application.properties`).

```bash
git push origin main
# → neobeedev/<image>:dev  and  :dev-3.65.4-5-gabc123  and  :dev-3  and  :dev-3.65
```

## 2. Feature / preview build (to test a branch)

When you're working on a feature branch and want an image you can pull on a dev environment:

**From the command line:**
```bash
gh workflow run build-and-push.yml --ref my-branch -f tag=my-feature
# → neobeedev/<image>:feat-my-feature
```
If you omit `-f tag`, the branch name is used (`feat-<branch>`).

**From the GitHub UI:**
1. Repo → **Actions** → workflow **"Build and Push to DockerHub"**.
2. **"Run workflow"** button → pick the branch → (optional) enter `tag` → **Run workflow**.

> Note: the "Run workflow" button only appears once a workflow with the `workflow_dispatch`
> trigger is on the default branch (`main`/`master`).
>
> A feature build **does not move** the `dev` / `prod` / `staging` tags — it gets only `feat-<...>`.

## 3. Release candidate / staging

When you want to test a production candidate before it goes to prod:

```bash
gh release create v3.65.6-rc.1 --prerelease --title "3.65.6-rc.1" --notes "..."
# → neobeedev/<image>:rc-3.65.6-1  +  :staging
```
- `staging` always points to the latest pre-release — handy for deploying to a staging environment.
- It **does not touch** the production tags.
- When the candidate is good, promote it with a full release (step 4).

## 4. Production release

```bash
gh release create v3.65.6 --title "3.65.6" --notes "..."
# → neobeedev/<image>:prod-3.65.6  +  :prod  :prod-3  :prod-3.65
```
Or via the GitHub UI: **Releases** → **Draft a new release** → tag `v3.65.6` → **Publish release**.

- `prod` / `prod-3` / `prod-3.65` move only if this is the **newest** version in that group
  (see "Hotfix" below) — so a hotfix on an older line never drags `prod` backward.

## 5. Hotfix from a released tag

When you need an urgent fix on an already-published version, without pulling in everything that
has since landed on `main`:

```bash
git checkout -b hotfix/3.65.7 v3.65.6      # branch FROM the release tag
# make the fix + commit
git push -u origin hotfix/3.65.7
gh release create v3.65.7 --target hotfix/3.65.7 --title "3.65.7" --notes "hotfix"
#   then PR hotfix/3.65.7 → main so the fix isn't lost
```
- `--target` points the new tag at the hotfix branch tip.
- If `main` has already moved to a newer line (e.g. 3.66.x), the hotfix publishes only
  `prod-3.65.7` + `prod-3.65` and does **not** move `prod` / `prod-3` backward.

---

## Important rules & common mistakes

- **Pushing a bare tag does nothing.** Production goes **only** through a published GitHub
  Release. `git push --tags` by itself does not trigger a build.
- **The tag must point to a commit that already contains the new workflow.** If you create a
  release on an old commit (from before the migration), the build will NOT start. Create the
  release on a tag tied to the current `main` (`--target main`).
- **A full release must be clean semver** (`vX.Y.Z`). For candidates, use `--prerelease` with
  an `-rc.N` suffix.
- **You don't touch the version in `application.properties`** — CI passes it via `-D` parameters.
  The `quarkus.application.version=dev` value in the file is only a default for local builds.
- **The version printed at application startup** is correct because it is baked into the image
  at build time (prod → `3.65.6`, dev → `3.65.4-5-gabc123`, local → `dev`).
- **`dev-3` / `dev-3.65`** are floating tags pointing to the latest dev on that major/minor line;
  they are derived from the last release tag, not written by hand.
