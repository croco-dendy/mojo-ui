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
| `npm run changeset` | Create a new changeset |
| `npm run changeset:version` | Version packages (used by CI) |
| `npm run changeset:publish` | Publish packages (used by CI) |

## Making Changes

### 1. Create a Branch

```bash
git checkout -b feature/my-feature
```

### 2. Make Your Changes

Edit the code, add features, fix bugs, etc.

### 3. Add a Changeset

**This is required for any change that should be released!**

```bash
npx changeset
```

This will:
1. Ask what kind of change it is:
   - `patch` - Bug fixes (0.1.0 → 0.1.1)
   - `minor` - New features (0.1.0 → 0.2.0)
   - `major` - Breaking changes (0.1.0 → 1.0.0)
2. Ask for a summary of the change
3. Create a markdown file in `.changeset/`

**Example:**
```bash
$ npx changeset
🦋  What kind of change is this for @dendelion/mojo-ui? … 
❯ patch  # Bug fixes
  minor  # New features
  major  # Breaking changes

🦋  Please enter a summary for this change …
Added new Button variant "ghost" for subtle actions

🦋  Changeset added! …
```

### 4. Commit Your Changes

```bash
git add .
git commit -m "feat: add ghost button variant"
git push origin feature/my-feature
```

### 5. Create a Pull Request

Open a PR on GitHub. The CI will run automatically.

## Release Process

### How Releases Work

We use **Changesets** for version management:

1. **You create changesets** with your PRs
2. **GitHub Action** creates a "Version Packages" PR automatically
3. **You review & merge** the PR when ready to release
4. **GitHub Action** publishes to NPM automatically

### Release Workflow

```
Developer                    GitHub Actions                NPM
    |                              |                        |
    |-- PR with changeset -------->|                        |
    |                              |                        |
    |-- Merge PR ----------------->|                        |
    |                              |-- Create "Version      |
    |                              |   Packages" PR         |
    |                              |                        |
    |-- Review & merge "Version    |                        |
    |   Packages" PR ------------->|                        |
    |                              |-- Update version       |
    |                              |-- Update CHANGELOG     |
    |                              |-- Publish to NPM ----->|
    |                              |                        |
    |                              |-- Create GitHub        |
    |                              |   Release              |
```

### What Happens When You Merge a Changeset PR?

1. Version is bumped in `package.json`
2. `CHANGELOG.md` is updated
3. Package is published to NPM
4. GitHub Release is created

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
# Skip all workflows
git commit -m "docs: update README [skip ci]"

# Skip only deploy
git commit -m "docs: update README [skip-deploy]"
```

## Questions?

Open an issue on GitHub if you have any questions!
