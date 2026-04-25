# Contributing to Mojo UI

Thank you for your interest in contributing to Mojo UI!

## Development Workflow

### Setup

```bash
# Clone the repository
git clone https://github.com/croco-dendy/mojo-ui.git
cd mojo-ui

# Install dependencies
npm install

# Start development server
npm run dev
```

### Available Scripts

| Script | Description |
|--------|-------------|
| `npm run dev` | Start development server with showcase |
| `npm run build` | Build library for production |
| `npm run check-types` | Run TypeScript type checking |
| `npm run lint` | Run linter |
| `npm run lint:fix` | Fix linting issues |
| `npm run ci` | Run full CI pipeline (types + build + test) |

## Making Changes

### 1. Make Your Changes

Edit the code, add features, fix bugs, etc.

```bash
# Make changes to src/
# Test locally with npm run dev
```

### 2. Run CI Checks Locally

```bash
npm run ci
```

### 3. Commit Your Changes

```bash
git add .
git commit -m "feat: add new feature"
git push origin main
```

## Release Process

### How Releases Work

When you push to `main` with a **version bump** in `package.json`:

1. GitHub Actions detects the new version
2. Runs CI checks (types, build, test)
3. Publishes to NPM automatically
4. Creates Git tag and GitHub Release

### To Release a New Version

```bash
# 1. Update version
npm version patch   # 0.1.0 -> 0.1.1 (bug fixes)
npm version minor   # 0.1.0 -> 0.2.0 (new features)
npm version major   # 0.1.0 -> 1.0.0 (breaking changes)

# 2. Push to main
git push origin main

# 3. GitHub Actions automatically publishes to NPM!
```

### What Gets Published

- ESM build (`dist/index.mjs`)
- CJS build (`dist/index.js`)
- CSS (`dist/index.css`)
- TypeScript declarations (`dist/*.d.ts`)
- Source files for Tailwind preset

## Code Style

- Follow the existing code patterns
- Use TypeScript for all new code
- Use SCSS modules for component styles
- Run `npm run lint:fix` before committing

## Commit Message Convention

We follow conventional commits:

| Type | Description | Example |
|------|-------------|---------|
| `feat:` | New feature | `feat: add ghost button variant` |
| `fix:` | Bug fix | `fix: correct button padding` |
| `docs:` | Documentation | `docs: update installation guide` |
| `style:` | Code style | `style: fix formatting` |
| `refactor:` | Refactoring | `refactor: simplify button logic` |
| `test:` | Tests | `test: add button tests` |
| `chore:` | Build/tooling | `chore: update dependencies` |

## Skip CI

To push without triggering workflows:

```bash
# Skip release workflow
git commit -m "docs: update README [skip-release]"

# Skip all workflows
git commit -m "docs: update README [skip ci]"
```

## Versioning Guide

| Bump | When to Use | Example |
|------|-------------|---------|
| **patch** | Bug fixes, docs updates | Fix button hover state |
| **minor** | New features, components | Add Tooltip component |
| **major** | Breaking changes, API removal | Remove deprecated component |

## Questions?

Open an issue on GitHub if you have any questions!
