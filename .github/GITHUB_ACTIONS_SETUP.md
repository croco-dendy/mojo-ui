# GitHub Actions Setup

This document explains how to set up GitHub Actions for automatic publishing.

## Required Secrets

### NPM_TOKEN

To enable automatic publishing to NPM, you need to add an NPM access token to GitHub Secrets.

#### Step 1: Generate NPM Access Token

1. Go to https://www.npmjs.com/settings/dendelion/tokens
2. Click **"Create New Token"** → **"Granular Access Token"**
3. Configure the token:
   - **Token name:** `github-actions-publish`
   - **Packages:** Select "Only select packages and scopes"
   - **Add package:** `@dendelion/mojo-ui`
   - **Permissions:** Read and write
   - **2FA bypass:** Enable (allows CI to publish without 2FA)
4. Click **"Generate Token"**
5. Copy the token (you won't see it again!)

#### Step 2: Add Token to GitHub Secrets

1. Go to https://github.com/croco-dendy/mojo-ui/settings/secrets/actions
2. Click **"New repository secret"**
3. Name: `NPM_TOKEN`
4. Value: Paste the token from Step 1
5. Click **"Add secret"**

**Note:** `GITHUB_TOKEN` is automatically provided by GitHub, you don't need to create it.

---

## Workflows

### 1. CI Workflow (`.github/workflows/ci.yml`)

**Triggers:**
- Push to `main`
- Pull requests to `main`

**Runs:**
- TypeScript type checking
- Build verification
- Tests (placeholder)

**Matrix:** Node.js 18.x and 20.x

### 2. CD Workflow (`.github/workflows/cd.yml`)

**Triggers:**
- Push to `main` (excluding changeset files)

**Runs:**
- Build verification
- Artifact upload

### 3. Release Workflow (`.github/workflows/release.yml`)

**Triggers:**
- Push to `main` with changes to source files

**Behavior:**
1. Checks if version in `package.json` is already published
2. If new version: runs CI checks
3. Publishes to NPM
4. Creates Git tag
5. Creates GitHub Release

---

## Release Workflow

### To Release a New Version

```bash
# 1. Bump version locally
npm version patch   # or minor, major

# 2. Push to main
git push origin main

# 3. GitHub Actions automatically:
#    - Detects new version
#    - Runs CI checks
#    - Publishes to NPM
#    - Creates Git tag: v0.1.2
#    - Creates GitHub Release
```

### What Happens

```
Developer                    GitHub Actions                NPM
    |                              |                        |
    |-- npm version patch -------->|                        |
    |-- git push origin main ----->|                        |
    |                              |-- Check if v0.1.2      |
    |                              |   exists on NPM        |
    |                              |                        |
    |                              |-- Run CI checks        |
    |                              |   (types, build)       |
    |                              |                        |
    |                              |-- Publish to NPM ----->|
    |                              |                        |
    |                              |-- Create Git tag       |
    |                              |-- Create GitHub        |
    |                              |   Release              |
```

---

## Versioning Guide

### When to use each bump:

| Type | Example | Version Change |
|------|---------|----------------|
| **patch** | Bug fix, docs update | 0.1.0 → 0.1.1 |
| **minor** | New feature, new component | 0.1.0 → 0.2.0 |
| **major** | Breaking change, API removal | 0.1.0 → 1.0.0 |

---

## Skip Release

To push without triggering a release:

```bash
# Skip release workflow
git commit -m "docs: update README [skip-release]"

# Skip all workflows
git commit -m "docs: update README [skip ci]"
```

---

## Monitoring

Check workflow status:
- Go to https://github.com/croco-dendy/mojo-ui/actions
- View run logs
- Debug failures

## Troubleshooting

### Publish fails with 403

- Check `NPM_TOKEN` is correctly set in GitHub Secrets
- Verify token has write access to `@dendelion/mojo-ui`
- Ensure 2FA bypass is enabled on the token

### Version already exists

The workflow checks npm before publishing. If the version exists, it skips publishing.

### Build fails

- Check that `npm run check-types` passes locally
- Check that `npm run build` works locally
- Review the Actions logs for specific errors

### Release not triggered

Make sure you're pushing changes to:
- `src/**`
- `package.json`
- `tsconfig.json`
- `vite.config.ts`
- `tailwind.config.js`
- `tailwind.ts`

Or use `[skip-release]` in commit message to skip.
