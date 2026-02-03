# Github Packages - project migration

Instructions for migrating projects to use private npm libraries from Github Packages.
The examples given in this guide are for `@estehdev/eutil` npm package.

## Prerequisites

If not done already, first follow instructions from "Github Packages - Preparation Steps".
Try to print out `GITHUB_PACKAGES_AUTH_TOKEN` in the terminal

```bash
> echo $GITHUB_PACKAGES_AUTH_TOKEN
> gho_*************** # your token
```

If the value of the `GITHUB_PACKAGES_AUTH_TOKEN` variable is missing, you need to execute the `github_packages_auth_token.sh` script.

## 1. Update `.npmrc` file

Add private Github Packages npm repo for @estehdev/*** libraries

```ini
@estehdev:registry=https://npm.pkg.github.com/
//npm.pkg.github.com/:_authToken=${GITHUB_PACKAGES_AUTH_TOKEN}
registry=https://registry.npmjs.org
```

## 2. Reinstall `@estehdev/eutil`

```bash
npm un @estehdev/eutil && npm i @estehdev/eutil
```

## 3. Modify CI/CD (optional)

**This is step is only required if it hasn't been done before in this project.**

### 3.1. Modify `infrastructure/lib/buildvuedocker-stack.ts`

- In the codebuild step add `GITHUB_PACKAGES_AUTH_TOKEN` export.
- Modify the `docker build` instruction by adding the secret: `--secret id=github_token,env=GITHUB_PACKAGES_AUTH_TOKEN`.
- Add `secretsmanager:GetSecretValue` permission to the rolePolicy statement.

*Example: CodeBuild step:*
```bash
export GITHUB_PACKAGES_AUTH_TOKEN=$(aws secretsmanager get-secret-value --secret-id githubpackages --query SecretString --output text)
```

*Example: Docker build*
```bash
docker build --secret id=github_token,env=GITHUB_PACKAGES_AUTH_TOKEN -t neobeedev/PROJECT-IMAGE-NAME .
```

### 3.2. Modify `Dockerfile`

Modify these two `COPY` and `RUN` commands.

```dockerfile
# old commands
# COPY package*.json ./
# RUN npm ci

# new commands
COPY package*.json .npmrc ./
RUN --mount=type=secret,id=github_token,env=GITHUB_PACKAGES_AUTH_TOKEN \
    npm ci
```

### 3.3. Commit changes to the *main* branch

Commit changes all the changes from above to the branch that triggers the build pipeline.

### 3.4. Redeploy cdk pipeline

After committing, redeploy the stack.

```typescript
cdk --require-approval never --profile mo-prod deploy STACK_NAME
```