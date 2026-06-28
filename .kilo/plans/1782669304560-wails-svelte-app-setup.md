# Wails + Svelte App Setup

## Context

The repo is empty except for `.gitignore`, `Agents.md`, and `rules/DESIGN.md`. This plan bootstraps a Wails v2 app with a Svelte 5 + Tailwind v4 frontend following the architecture and design rules defined in `Agents.md` and `DESIGN.md`.

## Decisions

| Decision | Choice | Rationale |
|---|---|---|
| Framework | Wails v2 | Per Agents.md tech stack |
| Frontend build | Svelte 5 + Vite (no SvelteKit) | Wails doesn't need SvelteKit; plain Svelte + Vite is sufficient |
| CSS | Tailwind v4 + global CSS | Per Agents.md; Tailwind v4 uses CSS-first `@theme` config |
| Fonts | Local `.woff2` files in `frontend/src/assets/fonts/` | User preference; offline-capable |
| App name | "Slate PM" | Per Agents.md |
| Router | None | Single page for now; routing added when needed |

## Tasks

### 1. Go / Wails Backend Scaffold

Create minimal Wails v2 Go files matching the `Agents.md` folder structure:

- **`main.go`** — Wails app entry point; registers the App binding, sets window defaults (title "Slate PM", 1200×800, min 900×600), embeds frontend dist
- **`wails.json`** — Wails project config: `name: "slate-pm"`, `frontend:install: "npm install"`, `frontend:build: "npm run build"`, `outputfilename: "slate-pm"`, `frontend:dist: "frontend/dist"`
- **`go.mod`** — Module `slate-pm`, require `github.com/wailsapp/wails/v2`
- **`backend/app.go`** — `package backend` with an `App` struct (empty for now, ready for future bindings)

Run `go mod tidy` to resolve dependencies.

### 2. Frontend Svelte 5 + Vite Setup

Initialize `frontend/` as a Vite + Svelte 5 project:

- **`frontend/package.json`** — devDependencies: `svelte`, `vite`, `@sveltejs/vite-plugin-svelte`, `tailwindcss`, `@tailwindcss/vite`. No runtime deps.
- **`frontend/vite.config.js`** — Svelte plugin + Tailwind v4 CSS plugin (`@tailwindcss/vite`)
- **`frontend/svelte.config.js`** — minimal Svelte config
- **`frontend/index.html`** — entry HTML that loads `/src/main.js`
- **`frontend/src/main.js`** — mounts `App.svelte` to `#app`
- **`frontend/src/App.svelte`** — imports `global.css`, renders `Home.svelte` from `pages/`

Create empty folder scaffolding:
- `frontend/src/components/base/`
- `frontend/src/components/composite/`
- `frontend/src/components/widgets/`
- `frontend/src/pages/`
- `frontend/src/stores/`
- `frontend/src/modules/`

Add placeholder `.gitkeep` files to empty folders.

### 3. Local Font Files

Download `.woff2` font files into `frontend/src/assets/fonts/`:

- **Geist** — regular (400), medium (500), semibold (600) weights
- **JetBrains Mono** — regular (400), medium (500) weights

Source: official GitHub releases or Google Fonts static builds.

### 4. Global CSS + Design Tokens

Create `frontend/src/styles/global.css`:

- `@import "tailwindcss"` — Tailwind v4 base
- `@theme` block — maps DESIGN.md tokens to Tailwind utilities:
  - **Colors**: all DESIGN.md `colors.*` values as `--color-*` custom properties
  - **Font families**: `--font-sans: 'Geist', sans-serif`, `--font-mono: 'JetBrains Mono', monospace`
  - **Spacing**: `--spacing-*` from DESIGN.md `spacing.*`
  - **Border radius**: `--radius-*` from DESIGN.md `rounded.*`
- `@font-face` declarations for Geist and JetBrains Mono loading from `../assets/fonts/`
- Base resets: `body` bg `--color-background`, text `--color-on-background`, font Geist, margin 0

### 5. Home Page

Create `frontend/src/pages/Home.svelte`:

- Centered layout (flexbox, full viewport height)
- Displays "Slate PM" using the `display-sm` typography token (Geist 30px/semibold)
- Uses `--color-primary` for the text color

### 6. Update `.gitignore`

Add frontend build artifacts:
- `frontend/node_modules/`
- `frontend/dist/`
- Built binary `slate-pm`

### 7. Verify

- `cd frontend && npm install && npm run build` — frontend compiles
- `go mod tidy` — Go dependencies resolve
- `wails dev` — app launches and shows "Slate PM" home page

## Open Questions

None. All decisions resolved.
