# Plan 001: Mojo UI Standalone Package

## Overview

This plan covers migrating Mojo UI from the Radio monorepo (`radio/packages/mojo-ui`) to an independent NPM package in its own repository (`mojo-ui`).

**Source:** Radio monorepo at `/home/croco/dev/radio/packages/mojo-ui/`
**Target:** Standalone repo at `/home/croco/dev/mojo-ui/`, published as `mojo-ui` on NPM

**Status:** Phase 1 ✅ COMPLETE | Phase 2 ⏳ PENDING

---

## Goal

Publish `mojo-ui` as a standalone NPM package with:
- 28 retro-styled React components
- Tailwind CSS preset with nature-themed design tokens
- Glassmorphism shared style utilities
- Interactive component showcase
- Full TypeScript support

---

## Phase 1: Repository Bootstrap ✅ COMPLETE

**Objective:** Set up the standalone repository structure by copying source from radio monorepo.

### Completed Tasks

#### 1.1 Copy Source Files ✅
- [x] Copy all source files from `radio/packages/mojo-ui/` to `mojo-ui/`
- [x] 27 component categories with SCSS modules
- [x] Showcase application (5 pages)
- [x] Icons (11 icons)
- [x] Shared styles (glassmorphism, layouts, grids)
- [x] Fonts (63 woff2 font files)
- [x] Design token documentation files

#### 1.2 Update Package Configuration ✅
- [x] Rename from `@radio/mojo-ui` to `mojo-ui`
- [x] Update description and keywords
- [x] Add npm metadata (repository, bugs, homepage URLs)
- [x] Include additional published files (tailwind.config.js, postcss.config.js, styles, globals)

#### 1.3 Create Standalone TypeScript Config ✅
- [x] Remove dependency on `../../tsconfig.base.json` (radio monorepo base)
- [x] Create self-contained `tsconfig.json` with all required compiler options
- [x] Configure for library output (declaration files, ESNext target)

#### 1.4 Update Import References ✅
- [x] Replace all `@radio/mojo-ui` references with `mojo-ui` in:
  - Showcase pages (welcome, components, docs, layout, tokens)
  - README examples and documentation
  - Installation instructions

#### 1.5 Add Package Files ✅
- [x] Add `LICENSE` (MIT)
- [x] Add `CHANGELOG.md`
- [x] Rewrite `README.md` for standalone NPM usage
- [x] Add usage examples with Tailwind CSS preset

---

## Phase 2: Dependencies & Build ⏳ PENDING

**Objective:** Install dependencies and verify the project builds and runs correctly.

### Tasks
- [ ] Run `npm install` (or `bun install`) to install all dependencies
- [ ] Run `npm run check-types` — fix any TypeScript errors
- [ ] Run `npm run build` — verify library builds (ESM + CJS + CSS)
- [ ] Run `npm run dev` — verify showcase works at localhost:3010
- [ ] Run `npm run lint` — verify code quality
- [ ] Fix any issues found

### Dependencies to Verify
| Package | Type | Status |
|---------|------|--------|
| React 18 | peer | ⏳ |
| React DOM 18 | peer | ⏳ |
| framer-motion 11 | peer | ⏳ |
| clsx | dependency | ⏳ |
| Tailwind CSS 3.4 | dev | ⏳ |
| Vite 5.4 | dev | ⏳ |
| Sass | dev | ⏳ |
| TypeScript 5 | dev | ⏳ |

### Definition of Done
- [ ] All dependencies installed without errors
- [ ] TypeScript compiles without errors
- [ ] Library builds successfully (ESM + CJS)
- [ ] Showcase runs in dev mode
- [ ] All lint checks pass

---

## Phase 3: Showcase Polish ⏳ PENDING

**Objective:** Ensure the showcase is clean and functional as a standalone demo.

### Tasks
- [ ] Verify all 28 components render correctly in showcase
- [ ] Verify design tokens page displays correctly
- [ ] Verify documentation page content is accurate for standalone package
- [ ] Verify welcome page with correct installation commands
- [ ] Test responsive layout
- [ ] Fix any broken references or visual issues

---

## Phase 4: NPM Publication ⏳ PENDING

**Objective:** Publish the package to NPM.

### Tasks
- [ ] Finalize version number (0.1.0)
- [ ] Run `npm run build` for production output
- [ ] Verify `files` field in package.json includes all necessary files
- [ ] Test package locally with `npm pack`
- [ ] Verify exported paths: `.`, `./tailwind`, `./styles`
- [ ] Publish to NPM: `npm publish`
- [ ] Verify installation: `npm install mojo-ui` in a test project

### Pre-Publish Checklist
- [ ] README has correct install instructions
- [ ] CHANGELOG is up to date
- [ ] LICENSE file present
- [ ] No sensitive data in repository
- [ ] All TypeScript declarations generated
- [ ] CSS is included in build output

---

## Phase 5: Monorepo Migration ⏳ PENDING

**Objective:** Update the Radio monorepo to consume mojo-ui from NPM instead of workspace.

### Tasks
- [ ] Install `mojo-ui` from NPM in `apps/admin`
- [ ] Update admin Tailwind config to use `mojoPreset` from `mojo-ui/tailwind`
- [ ] Update all imports from `@radio/mojo-ui` to `mojo-ui`
- [ ] Remove local `packages/mojo-ui` directory from monorepo
- [ ] Remove `@radio/mojo-ui` from workspace dependencies
- [ ] Verify admin app builds and runs correctly
- [ ] Verify player app if it uses mojo-ui

### Risk Mitigation
- Keep source copy in radio monorepo during migration
- Test thoroughly before removing local package
- Document rollback procedure

---

## Phase 6: CI/CD ⏳ PENDING

**Objective:** Set up continuous integration and showcase deployment.

### Tasks
- [ ] Add GitHub Actions workflow for:
  - Type checking on PR
  - Linting on PR
  - Build verification on PR
  - NPM publish on tag/release
- [ ] Set up showcase deployment (GitHub Pages or similar)
- [ ] Add version badge to README
- [ ] Add build status badge to README

---

## File Map

### Source Files (from radio/packages/mojo-ui)
```
mojo-ui/
├── src/
│   ├── index.ts                    # Main entry point (exports all components)
│   ├── main.tsx                    # Showcase entry point
│   ├── showcase.tsx                # Showcase main component
│   ├── globals.scss                # Global styles + Tailwind directives + fonts
│   ├── components/                 # 27 component directories
│   │   ├── alert/                  # Alert banner
│   │   ├── badge/                  # Status badge
│   │   ├── button/                 # Retro button
│   │   ├── card/                   # Basic card
│   │   ├── checkbox/               # Checkbox input
│   │   ├── circular-progress/      # Circular progress
│   │   ├── data-table/             # Data table
│   │   ├── icon-button/            # Icon button
│   │   ├── input/                  # Text input
│   │   ├── layout/                 # PageLayout, StatsGrid
│   │   ├── modal/                  # Modal dialog
│   │   ├── navigation-island/      # Navigation island
│   │   ├── panel/                  # Panel container
│   │   ├── popup/                  # Popup menu
│   │   ├── progress-bar/           # Progress bar
│   │   ├── radio/                  # Radio group
│   │   ├── select/                 # Select dropdown
│   │   ├── skeleton/               # Skeleton loader
│   │   ├── slider/                 # Range slider
│   │   ├── stats-card/             # Stats card
│   │   ├── status-indicator/       # Status indicator
│   │   ├── switch/                 # Toggle switch
│   │   ├── tabs/                   # Tab navigation
│   │   ├── textarea/               # Textarea input
│   │   ├── toast/                  # Toast notification
│   │   ├── tooltip/                # Tooltip
│   │   └── vinyl-tabs/             # Vinyl themed tabs
│   ├── icons/                      # 11 SVG icon components
│   ├── showcase/                   # Showcase application
│   │   ├── components/             # Showcase UI components
│   │   └── pages/                  # Showcase pages
│   ├── styles/                     # Shared style utilities
│   ├── types/                      # TypeScript declarations
│   └── utils/                      # Utility functions
├── public/
│   ├── fonts/                      # 63 woff2 font files
│   └── images/                     # Visual assets
├── tailwind.config.js              # Full Tailwind config (for mojo-ui itself)
├── tailwind.ts                     # Mojo preset export (for consumers)
├── postcss.config.js               # PostCSS config
├── vite.config.ts                  # Vite build config
├── tsconfig.json                   # Standalone TypeScript config
├── package.json                    # NPM package config
├── index.html                      # Showcase HTML entry
├── README.md                       # Package documentation
├── CHANGELOG.md                    # Release history
├── LICENSE                         # MIT license
└── paperplan/                      # Planning documents
```

---

## Key Decisions

### Package Name: `mojo-ui`
Simple, clean, no scope. Matches the repo name and is easy to install.

### Export Strategy
- Main entry: all components, icons, utils
- `./tailwind`: Tailwind CSS preset for consumer apps
- `./styles`: Glassmorphism/layout shared utility classes

### Build Output
- ESM (`.mjs`) + CJS (`.js`)
- TypeScript declarations (`.d.ts`)
- Single CSS output (`dist/index.css`)

### Peer Dependencies
- React 18+
- React DOM 18+
- framer-motion 11+

### Tailwind Integration
Consumers import `mojoPreset` from `mojo-ui/tailwind` and add it to their Tailwind config presets. This gives them all nature-themed colors, font families, text shadows, and plugins.

---

## Notes

- The source code remains in `radio/packages/mojo-ui/` during migration as a safety net
- After successful NPM publish and monorepo migration, the radio copy can be removed
- Font files (~3.5MB) are included in the package — consider lazy-loading in consumer apps
- The `tailwind.ts` preset uses `require()` for plugins — ensure this works in consumer build environments
- Framer Motion is used for modal animations and toast transitions
