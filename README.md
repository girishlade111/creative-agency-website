# KERN® — Creative Agency Website

A dark, editorial-style marketing site for **KERN®**, an independent digital design studio. Built as a single-page experience with scroll-driven storytelling, smooth inertial scrolling, a custom cursor, and full multi-page routing for case studies and journal articles.

![React](https://img.shields.io/badge/React-19-61DAFB?style=flat-square&logo=react&logoColor=black)
![TypeScript](https://img.shields.io/badge/TypeScript-5.9-3178C6?style=flat-square&logo=typescript&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-7-646CFF?style=flat-square&logo=vite&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.4-38B2AC?style=flat-square&logo=tailwindcss&logoColor=white)
![Framer Motion](https://img.shields.io/badge/Framer_Motion-12-0055FF?style=flat-square&logo=framer&logoColor=white)
![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Getting Started](#getting-started)
- [Available Scripts](#available-scripts)
- [Project Structure](#project-structure)
- [Routing](#routing)
- [Sections](#sections)
- [Content Model](#content-model)
- [Styling & Design System](#styling--design-system)
- [Performance Notes](#performance-notes)
- [Deployment](#deployment)
- [Contributing](#contributing)
- [License](#license)

---

## Overview

KERN® is a fictional creative studio website designed as a premium agency portfolio. The home page is a long-form scroll experience: a full-bleed hero, a running marquee, a manifesto statement, a split-scroll studio section, a works grid with hover previews, an image break, services, awards, a journal teaser, and a contact-heavy footer. Case studies and journal entries live on their own routes with detail pages.

Everything is driven by a single typed content file (`src/data/content.ts`), so projects and articles can be added or edited without touching component code.

---

## Features

- **Smooth scrolling** — [Lenis](https://lenis.darkroom.engineering/) inertial scrolling wired into a `requestAnimationFrame` loop, with anchor links intercepted and scrolled through Lenis.
- **Custom cursor** — a follower cursor that reacts to interactive elements across the whole site.
- **Scroll & page animations** — [Framer Motion](https://www.framer.com/motion/) driven transitions, `AnimatePresence` route/overlay animation, reveal-on-scroll sections.
- **Multi-page routing** — [React Router v7](https://reactrouter.com/) with home, works index, project detail, journal index, and article detail routes.
- **Live studio clock** — the nav displays a real-time clock in `Europe/Paris` time.
- **Responsive navigation** — desktop anchor nav plus an animated mobile menu overlay.
- **Data-driven content** — projects and articles defined as typed data with slug lookup helpers and "next item" navigation.
- **shadcn/ui-ready component set** — a full set of accessible Radix-based primitives under `src/components/ui` (dialog, dropdown, tabs, carousel, chart, forms with react-hook-form + zod, etc.).
- **Grain texture overlay** — subtle film-grain background over the near-black canvas for an editorial print feel.
- **Strict TypeScript** — path alias `@/*` → `src/*`, project references (`tsconfig.json`, `tsconfig.app.json`, `tsconfig.node.json`).
- **Linting** — flat ESLint config with React Hooks and React Refresh rules.

---

## Tech Stack

| Layer | Tools |
| --- | --- |
| Build | Vite 7, `@vitejs/plugin-react` |
| UI | React 19, TypeScript 5.9, React Router 7 |
| Styling | Tailwind CSS 3.4, PostCSS, Autoprefixer, `tailwindcss-animate`, `tw-animate-css` |
| Animation | Framer Motion 12, Lenis 1.3 |
| Components | Radix UI primitives, shadcn/ui patterns, Lucide icons, `class-variance-authority`, `clsx`, `tailwind-merge` |
| Forms / Validation | react-hook-form, zod, `@hookform/resolvers` |
| Misc UI | embla-carousel, sonner toasts, recharts, cmdk, vaul, react-day-picker, input-otp |
| Quality | ESLint 9 (flat config), typescript-eslint |

---

## Getting Started

### Prerequisites

- **Node.js** 18+ (20+ recommended)
- **npm** (or pnpm / yarn — a lockfile for npm is committed)

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/creative-agency-website.git
cd creative-agency-website

# 2. Install dependencies
npm install

# 3. Start the dev server (http://localhost:3000)
npm run dev
```

> `node_modules/` is git-ignored — always run `npm install` after cloning.

### Production build

```bash
npm run build     # type-check (tsc -b) + production bundle into dist/
npm run preview   # serve the dist/ build locally
```

---

## Available Scripts

| Script | Description |
| --- | --- |
| `npm run dev` | Start Vite dev server on port **3000** with HMR |
| `npm run build` | Type-check with `tsc -b`, then build production bundle to `dist/` |
| `npm run lint` | Run ESLint across the project |
| `npm run preview` | Preview the production build locally |

---

## Project Structure

```
.
├── index.html                 # HTML entry (meta, title, mount point)
├── package.json
├── vite.config.ts             # Vite config — port 3000, base './', '@' alias
├── tailwind.config.js         # Tailwind theme + shadcn/ui CSS variables
├── postcss.config.js
├── eslint.config.js
├── tsconfig.json              # Project references
├── tsconfig.app.json          # App (browser) TS config
├── tsconfig.node.json         # Tooling TS config
├── components.json            # shadcn/ui config
└── src/
    ├── main.tsx               # React entry point
    ├── App.tsx                # Router, Lenis setup, layout shell
    ├── index.css              # Global styles, CSS variables, grain overlay
    ├── App.css
    ├── assets/                # Project imagery (work1–6, break)
    ├── data/
    │   └── content.ts         # Projects, articles, lookup helpers
    ├── hooks/
    │   └── use-mobile.ts      # Responsive breakpoint hook
    ├── lib/
    │   └── utils.ts           # cn() helper (clsx + tailwind-merge)
    ├── components/
    │   └── ui/                # shadcn/ui + Radix primitives
    ├── sections/              # Home page sections
    │   ├── Cursor.tsx         # Custom cursor follower
    │   ├── Nav.tsx            # Fixed nav + mobile menu + clock
    │   ├── Hero.tsx
    │   ├── Marquee.tsx
    │   ├── Manifesto.tsx
    │   ├── SplitScroll.tsx    # Pinned/sticky studio split section
    │   ├── Works.tsx          # Selected works grid
    │   ├── ImageBreak.tsx
    │   ├── Services.tsx
    │   ├── Awards.tsx
    │   ├── Journal.tsx
    │   └── Footer.tsx         # Contact + footer
    └── pages/
        ├── Home.tsx           # Composes all home sections
        ├── WorksPage.tsx      # /works
        ├── ProjectPage.tsx    # /works/:slug
        ├── JournalPage.tsx    # /journal
        └── ArticlePage.tsx    # /journal/:slug
```

---

## Routing

Defined in `src/App.tsx`:

| Route | Page | Description |
| --- | --- | --- |
| `/` | `Home` | Full scroll experience (all sections) |
| `/works` | `WorksPage` | All projects |
| `/works/:slug` | `ProjectPage` | Single case study (e.g. `/works/chromatic-drift`) |
| `/journal` | `JournalPage` | All journal articles |
| `/journal/:slug` | `ArticlePage` | Single article (e.g. `/journal/start-on-paper`) |
| `*` | `Home` | Fallback |

Scroll position resets on every route change, and global anchor links (`#works`, `#services`, …) smooth-scroll through Lenis — navigating to an anchor from a sub-page returns home first, then scrolls.

---

## Sections

Home page, top to bottom:

1. **Hero** — studio intro, oversized display type
2. **Marquee** — infinite horizontal running text
3. **Manifesto** — studio statement with scroll reveals
4. **SplitScroll** — sticky split layout telling the studio story
5. **Works** — selected project grid linking to case studies
6. **ImageBreak** — full-width editorial image divider
7. **Services** — capabilities / offering list
8. **Awards** — recognition list
9. **Journal** — latest articles linking to the journal
10. **Footer** — contact CTA, links, colophon

Global chrome: **Cursor** (custom follower) and **Nav** (fixed header with anchors, mobile menu, live Paris clock).

---

## Content Model

All copy lives in [`src/data/content.ts`](src/data/content.ts).

### `Project`

```ts
interface Project {
  slug: string           // URL segment, e.g. 'chromatic-drift'
  title: string
  category: string       // e.g. 'Brand Identity'
  year: string
  img: string            // imported image (src/assets)
  client: string
  deliverables: string[]
  description: string[]  // paragraphs
  gallery: string[]
}
```

### `Article`

```ts
interface Article {
  slug: string
  title: string
  date: string           // e.g. 'Jun 2026'
  tag: string            // e.g. 'Process'
  img: string
  excerpt: string
  quote: string
  body: string[]
}
```

### Helpers

```ts
getProject(slug)    // Project | undefined
getArticle(slug)    // Article | undefined
nextProject(slug)   // cycles through projects
nextArticle(slug)   // cycles through articles
```

**To add a project:** drop an image into `src/assets/`, import it at the top of `content.ts`, and append a new object to `projects`. The works grid, detail route, and next-project navigation pick it up automatically. Articles work the same way.

---

## Styling & Design System

- **Canvas:** near-black `#0a0a0a` with warm off-white type `#ece9e4`, plus a grain overlay (`grain` class in `App.tsx`).
- **Tailwind + shadcn/ui tokens:** colors are exposed as CSS variables (`--background`, `--primary`, `--muted`, …) and mapped in `tailwind.config.js`, so components can use semantic classes (`bg-background`, `text-muted-foreground`, `rounded-lg`, …).
- **Path alias:** import from anywhere in `src` with `@/` — e.g. `import Nav from '@/sections/Nav'`.
- **Responsive:** mobile menu overlay, `use-mobile` hook, fluid type via Tailwind breakpoints.
- **Accessibility:** Radix primitives ship with focus management, keyboard navigation, and ARIA out of the box.

---

## Performance Notes

- Vite code-splits per-route dynamically imported pages where applicable and tree-shakes unused Radix packages.
- Lenis runs on a single `requestAnimationFrame` loop (cleaned up on unmount).
- `base: './'` in `vite.config.ts` makes the production build portable to any static host or subpath.
- `node_modules/`, `dist/`, and logs are excluded from git — the repository stays source-only.

---

## Deployment

The build is a static site in `dist/` — deploy anywhere:

**Netlify**

```bash
npm run build
# publish directory: dist
```

**Vercel**

```bash
npm i -g vercel
vercel --prod
# framework: Vite · build: npm run build · output: dist
```

**GitHub Pages / any static host**

```bash
npm run build
# upload the contents of dist/
```

Because `base` is `'./'`, relative asset paths work on GitHub Pages project sites without extra config.

---

## Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Commit your changes: `git commit -m "Add amazing feature"`
4. Push to the branch: `git push origin feature/amazing-feature`
5. Open a Pull Request

Please run `npm run lint` and `npm run build` before submitting.

---

## License

This project is released under the [MIT License](LICENSE).

---

**KERN®** — an independent digital design studio. Craft, not templates.

---

## Author

Built by Girish Lade — [ladestack.in](https://ladestack.in)
