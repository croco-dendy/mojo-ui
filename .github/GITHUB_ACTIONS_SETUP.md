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

## How It Works

### CI Workflow (`.github/workflows/ci.yml`)

Triggers on:
- Push to `main`
- Pull requests to `main`

Runs:
- Type checking
- Build
- Test (placeholder)

Matrix: Node.js 18.x and 20.x

### CD Workflow (`.github/workflows/cd.yml`)

Triggers on:
- Push to `main` (only when source files change)

Steps:
1. Install dependencies
2. Run type check
3. Build package
4. Check if version already published
5. Publish to NPM (if new version)
6. Create GitHub Release

## Version Bump Workflow

To release a new version:

```bash
# 1. Update version
npm version patch   # 0.1.1 -> 0.1.2
npm version minor   # 0.1.1 -> 0.2.0
npm version major   # 0.1.1 -> 1.0.0

# 2. Push to main
git push origin main

# 3. GitHub Actions will automatically publish!
```

## Skipping CI

To push without triggering workflows:

```bash
# Skip all workflows
git commit -m "docs: update [skip ci]"

# Skip only publish
git commit -m "docs: update [skip-publish]"
```

## Monitoring

Check workflow status:
- Go to https://github.com/croco-dendy/mojo-ui/actions
- View run logs
- Debug failures

## Troubleshooting

### Publish fails with 403

- Check `NPM_TOKEN` is correctly set
- Verify token has write access to `@dendelion/mojo-ui`
- Ensure 2FA bypass is enabled on the token

### Version already exists

The CD workflow checks if the version is already published and skips if it is. 
Bump the version with `npm version` before pushing.

### Build fails

- Check that `npm run check-types` passes locally
- Check that `npm run build` works locally
- Review the Actions logs for specific errors
