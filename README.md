# mojo-ui

Retro styled React component library with nature-themed design tokens and glassmorphism.

## Features

- **28 Components** — Buttons, forms, layout, navigation, feedback, data display
- **Tailwind CSS Preset** — Reusable `mojoPreset` with nature-themed color tokens
- **Glassmorphism** — Shared style utilities for glass card patterns
- **TypeScript** — Full TypeScript support with strict typing
- **SCSS Modules** — Scoped styling with SCSS modules
- **Accessible** — ARIA labels and keyboard navigation
- **Animated** — Smooth transitions powered by framer-motion

## Installation

### From NPM

```bash
npm install mojo-ui
# or
yarn add mojo-ui
# or
pnpm add mojo-ui
```

### From JSR (JavaScript Registry)

```bash
# With Deno
npx jsr add @croco-dendy/mojo-ui

# With npm (using jsr.io)
npm install @jsr/croco-dendy__mojo-ui
```

### Peer Dependencies

```bash
npm install react react-dom framer-motion tailwindcss
```

## Quick Start

### 1. Configure Tailwind CSS

```js
// tailwind.config.js
import { mojoPreset } from 'mojo-ui/tailwind';

export default {
  presets: [mojoPreset],
  content: ['./src/**/*.{js,jsx,ts,tsx}'],
};
```

### 2. Import Global Styles

```scss
// In your app entry (e.g., main.scss)
@import 'mojo-ui/src/globals.scss';
```

### 3. Use Components

```tsx
import { Button, Card, Input } from 'mojo-ui';

function App() {
  return (
    <Card title="Welcome">
      <Input placeholder="Enter your name" />
      <Button variant="green" title="Submit" />
    </Card>
  );
}
```

## Components

### Basic Input
- **Button** — Retro-styled 3D buttons (green, yellow, gray, red)
- **IconButton** — Circular icon buttons
- **Input** — Text input with label support
- **Checkbox** — Toggle checkbox
- **Select** — Dropdown select
- **Textarea** — Multi-line text input
- **Switch** — Toggle switch with variants
- **Radio** — Radio button group (horizontal/vertical)
- **Slider** — Range slider with analog feel

### Layout
- **Card** — Container with header and footer
- **Panel** — Multi-section container
- **PageLayout** — Standard page structure
- **StatsGrid** — Statistics grid layout

### Navigation
- **Tabs** — Tab navigation
- **VinylTabs** — Themed tab navigation
- **NavigationIsland** — Floating navigation bar

### Feedback
- **ProgressBar** — Segmented progress bar
- **CircularProgress** — Circular progress indicator
- **StatsCard** — Single statistic display
- **StatusIndicator** — Color-coded status badge
- **Skeleton** — Loading placeholder
- **Badge** — Status/label badge with dot indicators
- **Alert** — Alert banner with variants
- **Toast** — Notification toasts with auto-dismiss

### Overlay
- **Modal** — Animated dialog overlay
- **Popup** — Dropdown menu
- **Tooltip** — Hover information tooltip

### Data Display
- **DataTable** — Table with retro styling

## Icons

```tsx
import {
  CheckIcon, CloseIcon, PlusIcon, SearchIcon,
  MenuIcon, SettingsIcon, ArrowUpIcon, ArrowDownIcon,
  SortIcon, FilterIcon,
} from 'mojo-ui';
```

## Shared Styles

Reusable glassmorphism and layout utilities:

```tsx
import {
  container, content, title,
  statsCard, statsTitle, statsValue,
  statsGrid, serviceGrid, actionsGrid, recentList,
  glassmorphism, layout, grids, sharedStyles,
} from 'mojo-ui/styles';
```

## Design Tokens

### Nature Colors

| Color | Shades | Usage |
|-------|--------|-------|
| **moss** | fog, calm, DEFAULT, deep, relic, accent | Success, growth |
| **bark** | fog, calm, DEFAULT, deep, relic | Structure, wood |
| **coal** | fog, calm, DEFAULT, deep, relic | Backgrounds, dark surfaces |
| **clay** | fog, calm, DEFAULT, deep, relic | Warm accents |
| **river** | fog, calm, DEFAULT, deep, relic | Info, water elements |
| **paper** | fog, calm, DEFAULT, deep, relic, accent | Light surfaces |
| **sun** | fog, calm, DEFAULT, deep, relic | Highlights, warnings |
| **ember** | fog, calm, DEFAULT, deep, relic | Errors, danger |

### Typography

| Family | Usage |
|--------|-------|
| **Tiny5** | Display text, headings |
| **KyivType Sans** | UI elements, form inputs |
| **KyivType Serif** | Body text |
| **JetBrains Mono** | Code, monospace |

## Development

```bash
# Install dependencies
npm install

# Start showcase
npm run dev

# Build library
npm run build

# Type check
npm run check-types
```

## License

MIT
