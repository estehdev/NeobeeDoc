# Development cycle & build process — team guide

This document describes how building and publishing Docker images works after the move to the
new system. It applies to all migrated services (MoUser, MoSafewatch, MoCompany, MoLlm, …) —
the workflow is the same; only the image name differs.

## Key change

- **A production build is NO LONGER triggered by committing to `application.properties`.**
- Production is published **only by creating a GitHub Release** on a `vX.Y.Z` tag.
- The version is no longer maintained by hand in a file — **the git tag is the single source of truth**.

## Build channels

| Channel | Trigger | Registry | Image tags |
|---------|---------|----------|------------|
| **dev** | push to `main` (or `master`) | `ghcr.io/estehdev` (+ DockerHub `neobeedev`, temporary) | one floating tag: `dev` (`main` in a few repos); mirror adds `dev`, `dev-3` |
| **feat** | manual (`workflow_dispatch`) from any branch | `ghcr.io/estehdev` | `feat-<name>` |
| **rc / staging** | GitHub Release marked *pre-release* on `vX.Y.Z-rc.N` | `ghcr.io/estehdev` | `rc-<version>-<n>`, `staging` |
| **prod** | published GitHub Release on `vX.Y.Z` | DockerHub `neobeedev` | `X.Y.Z`, `X.Y`, `X` |

> The GHCR dev tag is **floating only** — no version-specific dev tags are published there, so
> packages don't pile up. The real version (from `git describe`, e.g. `3.65.4-5-gabc123`) is still
> baked into the image via `-Dquarkus.application.version`.

## Where images are published (registries)

- **Production** images go to **DockerHub** (`neobeedev/<image>`) — unchanged.
- **Everything else** (dev / feat / rc-staging) now goes to **GitHub Container Registry (GHCR)**:
  `ghcr.io/estehdev/<image>`.
- **Transition:** for now, **dev** images are *also* mirrored to DockerHub
  (`neobeedev/<image>:dev*`) so existing dev-environment references keep working. Once every
  dev environment pulls from GHCR, that mirror is removed and dev will live on GHCR only.

> Rolled out per service (MoSafewatch first). Until a given service's workflow is updated, all of
> its images still go to DockerHub. As of 2026-09-16 every migrated service shares this workflow;
> `NeobeeKeycloak` is the remaining exception — it still builds on push to `main` and pushes
> `<pom version>` / `latest` / `prod` / `test` unconditionally.

### Pulling images from GHCR

GHCR is **not** DockerHub — your DockerHub credentials do not work for it. To pull an image you
need a GitHub token with the `read:packages` scope:

1. Create a Personal Access Token (classic): GitHub → **Settings → Developer settings →
   Personal access tokens → Tokens (classic) → Generate new token**, tick **`read:packages`**.
2. Log in once on the machine/environment that pulls:
   ```bash
   echo <TOKEN> | docker login ghcr.io -u <github-username> --password-stdin
   ```
3. Pull as usual:
   ```bash
   docker pull ghcr.io/estehdev/<image>:dev
   ```

For a Kubernetes pull secret, use the same token:
```bash
kubectl create secret docker-registry ghcr \
  --docker-server=ghcr.io \
  --docker-username=<github-username> \
  --docker-password=<TOKEN>
```

**Package visibility:** the first push creates the package as **private**, auto-linked to its repo.
If a package should be pullable without authentication, an org admin sets it public:
**Org → Packages → `<image>` → Package settings → Change visibility**.

> **Pushing from CI needs no setup** — the workflow authenticates to GHCR with the built-in
> `GITHUB_TOKEN` (the job has `packages: write`). The notes above are only for *pulling*.

## Versioning — `vX.Y.Z`

- We use **semantic versioning** with a `v` prefix: `v3.65.5`.
- `X` = major, `Y` = minor, `Z` = patch.
- A full release tag must be clean semver (`v3.66.2`). Tags like `v3.66.2-beta` published as a
  **full** release are rejected — use a pre-release flag or a clean tag.

---

## 1. Day-to-day work (dev)

Nothing special — **just push/merge to `main`**. CI automatically:
- builds and publishes the image to GHCR under a single floating tag (`dev`, or `main` in a few
  repos), and mirrors `dev` + `dev-3` to DockerHub.
- derives the version from git (you don't touch `application.properties`).

```bash
git push origin main
# → ghcr.io/estehdev/<image>:dev   (mirrored to neobeedev/<image>:dev and :dev-3)
```

## 2. Feature / preview build (to test a branch)

When you're working on a feature branch and want an image you can pull on a dev environment:

**From the command line:**
```bash
gh workflow run build-and-push.yml --ref my-branch -f tag=my-feature
# → ghcr.io/estehdev/<image>:feat-my-feature
```
If you omit `-f tag`, the branch name is used (`feat-<branch>`).

**From the GitHub UI:**
1. Repo → **Actions** → the build-and-push workflow (named either *Build and Push Container
   Image* or *Build and Push to DockerHub*, depending on the repo).
2. **"Run workflow"** button → pick the branch → (optional) enter `tag` → **Run workflow**.

> Note: the "Run workflow" button only appears once a workflow with the `workflow_dispatch`
> trigger is on the default branch (`main`/`master`).
>
> A feature build **does not move** the `dev` / `prod` / `staging` tags — it gets only `feat-<...>`.

## 3. Release candidate / staging

When you want to test a production candidate before it goes to prod:

```bash
gh release create v3.65.6-rc.1 --prerelease --title "3.65.6-rc.1" --notes "..."
# → ghcr.io/estehdev/<image>:rc-3.65.6-1  +  :staging
```
- `staging` always points to the latest pre-release — handy for deploying to a staging environment.
- It **does not touch** the production tags.
- When the candidate is good, promote it with a full release (step 4).

## 4. Production release

```bash
gh release create v3.65.6 --title "3.65.6" --notes "..."
# → neobeedev/<image>:3.65.6  +  :3.65  :3
```
Or via the GitHub UI: **Releases** → **Draft a new release** → tag `v3.65.6` → **Publish release**.

- `3.65` (MAJOR.MINOR) and `3` (MAJOR) move only if this is the **newest** version in that group
  (see "Hotfix" below) — so a hotfix on an older line never drags `3` backward.
- There is **no floating `prod` tag** — it was removed on 2026-09-16. Pin deployments to the exact
  `X.Y.Z`, or follow `X.Y` / `X` if you want a tier pointer.

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
  `3.65.7` + `3.65` and does **not** move `3` backward.

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
- **`dev-3`** is a floating tag on the DockerHub mirror pointing at the latest dev on that major
  line; it is derived from the last release tag, not written by hand. There is no `dev-3.65`.
