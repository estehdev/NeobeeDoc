# Github Packages - Preparation Steps

Preparation steps for working with projects that reference private utils in Github Packages Npm Registry.

## 1. Install Github CLI

```bash
brew install gh
```

## 2. Login to github

```bash
gh auth login
```

## 3. Refresh token scopes

```bash
gh auth refresh --scopes read:packages
```

## 4. Verify token scopes

```bash
gh auth status
```

## 5. Set `GITHUB_PACKAGES_AUTH_TOKEN` to bash env

```bash
export GITHUB_PACKAGES_AUTH_TOKEN=`gh auth token`
```

> Tip: Create a script `github_packages_auth_token.sh` in your user folder and paste the code from above

## 6. *@estehdev/eutil* reinstall test (optional)

```bash
npm un @estehdev/eutil && npm i @estehdev/eutil
```
