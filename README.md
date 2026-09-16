# Wildwood Portfolio

A React portfolio website for showcasing GitHub repositories, projects, and the
skills behind them. The app is organized by responsibility so new pages and
features can be added without coupling the whole site together.

## Getting started

```bash
npm install
npm run dev
```

Useful commands:

- `npm run build` creates a production build.
- `npm run preview` serves the production build locally.

## Folder structure

```text
.
├── public/              # Static files copied directly to the site
├── src/
│   ├── assets/          # Images, icons, and other imported media
│   ├── components/      # Reusable UI pieces, such as ProjectCard
│   ├── data/            # Portfolio content and repository metadata
│   ├── hooks/            # Reusable React hooks, such as useRepositories
│   ├── layouts/          # Shared page shells, such as the site navigation
│   ├── pages/            # Route-level views, such as Home and ProjectDetails
│   ├── styles/           # Global Tailwind/CSS entry points
│   ├── types/            # Shared TypeScript types and interfaces
│   └── utils/            # Framework-independent helpers and formatters
├── index.html            # Vite's HTML entry point
├── postcss.config.js     # PostCSS plugins used by Tailwind
├── tailwind.config.js    # Tailwind content paths and theme extensions
└── vite.config.ts        # Vite development and build configuration
```

Each source folder contains an `index.ts` barrel file so related exports can
be imported from a stable path as the project grows. For example:

```ts
import { ProjectCard } from './components'
import { repositories } from './data'
```

### What belongs where?

| Folder | Purpose | Example |
| --- | --- | --- |
| `assets` | Media imported by components | `github-mark.svg` |
| `components` | Small, reusable UI elements | `ProjectCard.tsx` |
| `data` | Static or fetched portfolio content | `repositories.ts` |
| `hooks` | Stateful, reusable React logic | `useRepositories.ts` |
| `layouts` | Shared page structure | `PortfolioLayout.tsx` |
| `pages` | Full views mapped to routes | `HomePage.tsx` |
| `styles` | Global styles and design tokens | `global.css` |
| `types` | Shared application contracts | `repository.ts` |
| `utils` | Pure helper functions | `formatLanguage.ts` |

## Tailwind CSS

Tailwind is wired through `src/styles/global.css`, which contains the
`@tailwind base`, `@tailwind components`, and `@tailwind utilities` layers.
Import that file once from `src/main.tsx`. Add custom theme values to
`tailwind.config.js` rather than scattering one-off styles across components.

## Connecting other repositories

See [`hookup.md`](./hookup.md) for options to display or consume other GitHub
repositories without copying their source code into this project.
