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

### Making Changes

1. Create a new branch: `git checkout -b feature/my-feature`
2. Make your changes
3. Run `npm run ci` to ensure everything passes
4. Commit your changes: `git commit -m "feat: add new feature"`
5. Push to GitHub: `git push origin feature/my-feature`
6. Create a Pull Request

## CI/CD Pipeline

### Continuous Integration (CI)

Every Pull Request and push to `main` triggers:
- TypeScript type checking
- Build verification
- Tests (when added)

Runs on Node.js 18.x and 20.x.

### Continuous Deployment (CD)

When you push to `main` with changes to:
- Source files (`src/**`)
- Package configuration
- Build configuration

The workflow will:
1. Build the package
2. Check if the version is already published
3. Publish to NPM if it's a new version
4. Create a GitHub Release

### Version Management

To publish a new version:

1. Update the version in `package.json`:
   ```bash
   npm version patch  # for bug fixes
   npm version minor  # for new features
   npm version major  # for breaking changes
   ```

2. Push to main:
   ```bash
   git push origin main
   ```

3. The CD workflow will automatically publish the new version.

### Skipping Publish

If you need to push without triggering a publish, include `[skip-publish]` in your commit message:

```bash
git commit -m "docs: update README [skip-publish]"
```

## Code Style

- Follow the existing code patterns
- Use TypeScript for all new code
- Use SCSS modules for component styles
- Run `npm run lint:fix` before committing

## Commit Message Convention

We follow conventional commits:

- `feat:` New feature
- `fix:` Bug fix
- `docs:` Documentation changes
- `style:` Code style changes (formatting, etc.)
- `refactor:` Code refactoring
- `test:` Adding or updating tests
- `chore:` Build process or auxiliary tool changes

## Questions?

Open an issue on GitHub if you have any questions!
