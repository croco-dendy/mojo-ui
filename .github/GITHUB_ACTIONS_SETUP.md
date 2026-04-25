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
- Push to `main`

**Behavior:**
- If changesets exist: Creates "Version Packages" PR
- If "Version Packages" PR merged: Publishes to NPM

---

## Changesets Workflow

### For Contributors

When you make a change that should be released:

```bash
# 1. Make your changes
# ... edit code ...

# 2. Add a changeset
npx changeset

# 3. Follow the prompts:
#    - Select patch/minor/major
#    - Write a summary

# 4. Commit the changeset with your code
git add .
git commit -m "feat: add new feature"
git push
```

### For Maintainers

When you're ready to release:

1. The Changesets bot will create a "Version Packages" PR automatically
2. Review the PR:
   - Check version bumps are correct
   - Review CHANGELOG updates
3. Merge the PR
4. The Release workflow will automatically:
   - Update version in `package.json`
   - Update `CHANGELOG.md`
   - Publish to NPM
   - Create GitHub Release

---

## Versioning Guide

### When to use each type:

| Type | Example | Version Change |
|------|---------|----------------|
| **patch** | Bug fix, docs update | 0.1.0 → 0.1.1 |
| **minor** | New feature, new component | 0.1.0 → 0.2.0 |
| **major** | Breaking change, API removal | 0.1.0 → 1.0.0 |

### Example Changesets

**Patch (bug fix):**
```markdown
---
"@dendelion/mojo-ui": patch
---

Fix button hover state not working in Safari
```

**Minor (new feature):**
```markdown
---
"@dendelion/mojo-ui": minor
---

Add new `Tooltip` component with 4 placement options
```

**Major (breaking change):**
```markdown
---
"@dendelion/mojo-ui": major
---

Remove deprecated `OldButton` component
```

---

## Manual Release (Emergency)

If you need to publish manually:

```bash
# 1. Version packages locally
npm run changeset:version

# 2. Commit changes
git add .
git commit -m "chore: version packages"
git push

# 3. Publish to NPM
npm run changeset:publish
```

**Note:** This requires `NPM_TOKEN` to be set in your environment.

---

## Monitoring

Check workflow status:
- Go to https://github.com/croco-dendy/mojo-ui/actions
- View run logs
- Debug failures

## Troubleshooting

### Changeset PR not created

- Ensure you have changeset files in `.changeset/` directory
- Check the Release workflow ran successfully
- Look for errors in the Actions logs

### Publish fails with 403

- Check `NPM_TOKEN` is correctly set in GitHub Secrets
- Verify token has write access to `@dendelion/mojo-ui`
- Ensure 2FA bypass is enabled on the token

### Version already exists

Changesets handles this automatically - it checks npm before publishing.

### Build fails

- Check that `npm run check-types` passes locally
- Check that `npm run build` works locally
- Review the Actions logs for specific errors
