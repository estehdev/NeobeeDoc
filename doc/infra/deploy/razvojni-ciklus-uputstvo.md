# Развојни циклус и build процес — упутство за тим

Овај документ описује како функционише build и објављивање Docker image-а након
преласка на нови систем. Важи за све мигриране сервисе (MoUser, MoSafewatch, MoCompany,
MoLlm, …) — workflow је исти, разликује се само име image-а.

## Кључна промена

- **Продукциони build се више НЕ покреће commit-ом у `application.properties`.**
- Продукција се објављује **искључиво креирањем GitHub Release-а** на `vX.Y.Z` таг-у.
- Верзија се више не одржава ручно у фајлу — **једини извор истине је git таг**.

## Канали build-а

| Канал | Када се покреће | Регистри | Тагови image-а |
|-------|-----------------|----------|----------------|
| **dev** | push на `main` (или `master`) | `ghcr.io/estehdev` (+ DockerHub `neobeedev`, привремено) | `dev`, `dev-<верзија>`, `dev-3`, `dev-3.65` |
| **feat** | ручно (`workflow_dispatch`) са било које гране | `ghcr.io/estehdev` | `feat-<назив>` |
| **rc / staging** | GitHub Release означен као *pre-release* на `vX.Y.Z-rc.N` | `ghcr.io/estehdev` | `rc-<верзија>-<n>`, `staging` |
| **prod** | објављен GitHub Release на `vX.Y.Z` | DockerHub `neobeedev` | `prod-X.Y.Z`, `prod`, `prod-3`, `prod-3.65` |

> `dev-<верзија>` је облика `dev-3.65.4-5-gabc123` (последњи release + број commit-а + sha),
> добијен преко `git describe`. Пре првог `v*` тага користи се `dev-<sha>`.

## Где се објављују image-и (регистри)

- **Продукциони** image-и иду на **DockerHub** (`neobeedev/<image>`) — без промене.
- **Све остало** (dev / feat / rc-staging) сада иде на **GitHub Container Registry (GHCR)**:
  `ghcr.io/estehdev/<image>`.
- **Прелаз:** за сада се **dev** image-и *такође* копирају на DockerHub
  (`neobeedev/<image>:dev*`) да би постојеће референце на dev окружењима наставиле да раде.
  Када сва dev окружења буду повлачила са GHCR-а, то копирање се уклања и dev остаје само на GHCR.

> Уводи се сервис по сервис (прво MoSafewatch). Док се workflow одређеног сервиса не ажурира,
> сви његови image-и и даље иду на DockerHub.

### Повлачење image-а са GHCR-а

GHCR **није** DockerHub — твоји DockerHub креденцијали ту не раде. За повлачење image-а треба ти
GitHub токен са `read:packages` овлашћењем:

1. Направи Personal Access Token (classic): GitHub → **Settings → Developer settings →
   Personal access tokens → Tokens (classic) → Generate new token**, штиклирај **`read:packages`**.
2. Улогуј се једном на машини/окружењу које повлачи:
   ```bash
   echo <TOKEN> | docker login ghcr.io -u <github-korisnicko-ime> --password-stdin
   ```
3. Повлачи као и обично:
   ```bash
   docker pull ghcr.io/estehdev/<image>:dev
   ```

За Kubernetes pull secret користи исти токен:
```bash
kubectl create secret docker-registry ghcr \
  --docker-server=ghcr.io \
  --docker-username=<github-korisnicko-ime> \
  --docker-password=<TOKEN>
```

**Видљивост пакета:** први push прави пакет као **приватан**, аутоматски повезан са својим repo-м.
Ако пакет треба да буде доступан без аутентикације, админ организације га поставља на јаван:
**Org → Packages → `<image>` → Package settings → Change visibility**.

> **Push из CI-ја не захтева никакво подешавање** — workflow се аутентикује на GHCR преко
> уграђеног `GITHUB_TOKEN`-а (job има `packages: write`). Горње напомене важе само за *повлачење*.

## Верзионисање — `vX.Y.Z`

- Користимо **семантичко верзионисање** са префиксом `v`: `v3.65.5`.
- `X` = major, `Y` = minor, `Z` = patch.
- Пун release таг мора бити чист semver (`v3.66.2`). Тагови типа `v3.66.2-beta` као **пун**
  release биће одбијени — користи pre-release ознаку или чист таг.

---

## 1. Свакодневни рад (dev)

Ништа посебно — **само push/merge на `main`**. CI аутоматски:
- направи и објави image са таговима `dev`, `dev-<git-describe>`, `dev-3`, `dev-3.65`.
- верзију извуче из git-а (не дираш `application.properties`).

```bash
git push origin main
# → neobeedev/<image>:dev  и  :dev-3.65.4-5-gabc123  и  :dev-3  и  :dev-3.65
```

## 2. Feature / preview build (за тестирање гране)

Када радиш на feature грани и желиш image који можеш да повучеш на dev окружење:

**Из командне линије:**
```bash
gh workflow run build-and-push.yml --ref naziv-grane -f tag=moj-feature
# → neobeedev/<image>:feat-moj-feature
```
Ако изоставиш `-f tag`, користи се назив гране (`feat-<grana>`).

**Из GitHub UI:**
1. Repo → **Actions** → workflow **„Build and Push to DockerHub“**.
2. Дугме **„Run workflow“** → изабери грану → (опционо) упиши `tag` → **Run workflow**.

> Напомена: дугме „Run workflow“ се појављује тек када је workflow са `workflow_dispatch`
> тригер-ом на подразумеваној грани (`main`/`master`).
>
> Feature build **не помера** `dev` / `prod` / `staging` тагове — добија само `feat-<...>`.

## 3. Release кандидат / staging

Када желиш да тестираш кандидат за продукцију пре него што оде у prod:

```bash
gh release create v3.65.6-rc.1 --prerelease --title "3.65.6-rc.1" --notes "..."
# → neobeedev/<image>:rc-3.65.6-1  +  :staging
```
- `staging` увек показује на најновији pre-release — згодно за деплој на staging окружење.
- **Не дира** продукционе тагове.
- Када је кандидат добар, промовишеш га пуним release-ом (корак 4).

## 4. Продукциони release

```bash
gh release create v3.65.6 --title "3.65.6" --notes "..."
# → neobeedev/<image>:prod-3.65.6  +  :prod  :prod-3  :prod-3.65
```
Или кроз GitHub UI: **Releases** → **Draft a new release** → таг `v3.65.6` → **Publish release**.

- `prod` / `prod-3` / `prod-3.65` се померају само ако је ово **најновија** верзија у тој
  групи (види „Hotfix“ испод) — тако hotfix на старој линији не враћа `prod` уназад.

## 5. Hotfix са објављеног тага

Када треба хитна исправка на већ објављеној верзији, без повлачења свега што је у
међувремену стигло на `main`:

```bash
git checkout -b hotfix/3.65.7 v3.65.6      # грана ОД release тага
# направи исправку + commit
git push -u origin hotfix/3.65.7
gh release create v3.65.7 --target hotfix/3.65.7 --title "3.65.7" --notes "hotfix"
#   затим PR hotfix/3.65.7 → main да се исправка не изгуби
```
- `--target` веже нови таг за врх hotfix гране.
- Ако је `main` већ отишао на новију линију (нпр. 3.66.x), hotfix објављује само
  `prod-3.65.7` + `prod-3.65` и **не** помера `prod` / `prod-3` уназад.

---

## Важна правила и честе грешке

- **Празан push тага не ради ништа.** Продукција иде **само** преко објављеног GitHub
  Release-а. `git push --tags` сам по себи не покреће build.
- **Таг мора да показује на commit који већ садржи нови workflow.** Ако направиш release
  на старом commit-у (од пре миграције), build се НЕЋЕ покренути. Прави release на таг-у
  везаном за актуелни `main` (`--target main`).
- **Пун release мора бити чист semver** (`vX.Y.Z`). За кандидате користи `--prerelease`
  и `-rc.N` суфикс.
- **Верзију не дираш у `application.properties`** — CI је прослеђује преко `-D` параметара.
  Вредност `quarkus.application.version=dev` у фајлу је само default за локални build.
- **Верзија која се исписује при старту апликације** је тачна јер је „упечена“ у image
  током build-а (prod → `3.65.6`, dev → `3.65.4-5-gabc123`, локално → `dev`).
- **`dev-3` / `dev-3.65`** су „покретни“ тагови који показују на најновији dev на тој
  major/minor линији; изведени су из последњег release тага, не пишу се ручно.
