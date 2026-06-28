# Slate PM

Slate PM is a simple and intuitive project management app for hobbyists to handle their projects.

It follows a Go-first architecture, where the backend contains all business logic and the frontend is a thin UI layer connected through Wails.

---

## Tech Stack
- Backend: Go (Wails v2)
- Frontend: Svelte 5 with Runes
- Styling: Tailwind CSS
- Database: SQLite (configured with WAL mode enabled)

---

## Code Style

- Prefer plain JavaScript over TypeScript
  - Note: You may utilize the automatically generated TypeScript bindings/types provided by Wails for IDE intelligence.
- Use 2 spaces for indentation
- Use JSDoc-Notation for documentation. 
- Code should speak for itself. Only use inline comments if necessary
- Minimize dependencies:
  - Avoid third-party dependencies unless absolutely necessary
  - Use Go modules with explicit version pinning
  - always ask before adding new dependencies

---

## Architecture

The system is strictly layered:

- **Go (Core System)**
  - All business logic lives here
  - All validation happens here
  - All data access happens here
  - This is the source of truth

- **Wails Bridge (Contract Layer)**
  - Exposes Go functions to the frontend
  - No business logic allowed here
  - Only data transfer and orchestration

- **Frontend (UI Layer)**
  - Frontend must never implement logic that can affect application state validity
  - Handles UI state and rendering using Svelte 5 Runes
  - Calls backend functions via Wails only
  - holds no domain or business rules
  - Backend remains the final source of truth for all data
  - Frontend validation exists for UX feedback only
  - Backend validation is always authoritative and must re-validate all inputs

### Rules
- Keep components under 200 lines (soft rule, prioritize readability)
- Prefer clarity over abstraction
- Keep logic in Go, not in the frontend

### Folder Structure
slate-pm/
├─ db/
│   - database config (SQLite, WAL mode, migrations)
│
├─ backend/
│   - Go + Wails core system (source of truth)
│   ├─ domain/
│   │   - business logic + rules
│   │
│   ├─ wails/
│   │   - exposed bridge functions (no logic)
│   │
│   └─ internal/
│       - services + repository + utilities
│       - all backend implementation details
│
├─ frontend/
│   - Svelte UI layer (presentation + interaction logic)
│   ├─ components/
│   │   - base (reusable UI primitives)
│   │   - composite (feature-aware components)
│   │   - widgets (page sections)
│   │
│   ├─ pages/
│   │   - route-level screens
│   │
│   ├─ stores/
│   │   - UI state + cached backend data
│   │
│   └─ modules/
│       - UI logic helpers
│       - formatting (dates, labels)
│       - visualization/data transformation
│       - validation helpers (UX only)
│
└─ rules/
    └─ DESIGN.md

---

## Design Rules

- Frontend design and UI decisions must follow `./rules/DESIGN.md`
- This includes layout, spacing, styling patterns, and visual consistency rules
- If there is a conflict between implementation preference and `DESIGN.md`, the design file takes priority for frontend-related decisions
- Backend logic and architecture are not affected by this file

---

## Testing

Testing follows system layers:

- Go backend:
  - Use Go built-in `testing` package
  - Unit test all business logic

- Frontend:
  - Use Vitest for component and UI logic
  - Use Playwright for end-to-end flows

Rules:
- Focus on meaningful coverage (80% target is a guideline, not a goal to optimize blindly)
- Test business logic in Go, not in the UI layer

---

## Security

- Never commit API keys or secrets
- Validate all user inputs in the Go backend
- Use parameterized queries for database access
- Treat frontend as untrusted (backend is authoritative)

---

## AI Behavior

- Be brief and direct
- Prefer actionable output over explanations
- Do not restate user input unless required for clarity
- Avoid filler, introductions, and conclusions

### Code Changes

- Prefer minimal diffs over full rewrites
- Do not refactor unrelated code
- Follow existing patterns in the codebase
- Do not introduce new abstractions unless clearly justified by reduced complexity
- Preserve architecture unless explicitly asked to change it

### Decision Making

- If unclear, ask a question instead of guessing
- Prefer clarity → simplicity → rule compliance (in that order)
- Do not make architectural changes without explicit request or strong justification

### Scope Control

- Stay strictly within the requested task
- Do not “improve” unrelated parts of the system
- Do not add features, dependencies, or refactors unless asked

### Communication

- Assume the user prefers precision over explanation
- Only explain when explicitly requested
---