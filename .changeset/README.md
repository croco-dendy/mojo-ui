# Changesets

This directory contains changesets for the Mojo UI package.

## What are Changesets?

Changesets are a way to track changes and automate versioning. When you make a change that should be released, you create a changeset file describing the change.

## Creating a Changeset

```bash
npx changeset
```

This will:
1. Ask what kind of change it is (patch/minor/major)
2. Ask for a summary of the change
3. Create a markdown file in this directory

## How Versioning Works

- **patch** (0.1.0 → 0.1.1): Bug fixes, small changes
- **minor** (0.1.0 → 0.2.0): New features, backwards compatible
- **major** (0.1.0 → 1.0.0): Breaking changes

## Workflow

1. Make your code changes
2. Run `npx changeset` to create a changeset
3. Commit the changeset file with your code
4. Push to GitHub
5. When ready to release, the "Version Packages" PR will be created automatically
6. Review and merge the PR to publish to NPM

## Example Changeset

```markdown
---
"@dendelion/mojo-ui": minor
---

Added new Button variant "ghost" for subtle actions
```

## More Info

- [Changesets Documentation](https://github.com/changesets/changesets)
- [GitHub Integration](https://github.com/changesets/changesets/blob/main/docs/automating-changesets.md)
