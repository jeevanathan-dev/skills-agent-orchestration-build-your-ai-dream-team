# Mona's Project Pulse — Implementation Plan

## Summary
Project Pulse is a small, single-page frontend dashboard that displays project cards with status badges, priority indicators, and a responsive layout. This plan breaks the work into clear, ordered steps that Designers and Coders can execute in parallel where possible. It includes explicit file ownership, a starter data schema and sample entries for `app/project-data.json`, and a deterministic VS Code launch configuration requirement to open `app/index.html` with the working directory set to `${workspaceFolder}/app`.

Deliverables are small, low-dependency artifacts so the team can ship quickly and iterate.

---

## Ordered implementation steps

1. Project setup & scaffolding
2. Design deliverables and tokens
3. Data schema & sample data (project-data.json)
4. Static HTML structure and semantic markup
5. CSS system, components, and responsive layout
6. Client-side rendering (fetch JSON -> render cards)
7. Accessibility, keyboard interactions, and focus states
8. Visual polish, animations, and micro-interactions
9. Automated checks and manual validation
10. Final integration, launch configuration, and handoff

Each step below includes file assignments, validation expectations, and dependencies.

---

## File assignments for each step

Note: list indicates exact files each specialist should create or modify.

Step 1 — Project setup & scaffolding (Coder)
- Create/modify:
  - app/index.html (skeleton)
  - app/styles.css (empty or minimal)
  - app/main.js (entrypoint for client-side rendering)
  - app/project-data.json (initial file — base schema + examples as provided below)
  - .vscode/launch.json (deterministic launch config; see requirement below)
  - app/assets/ (directory for images / SVGs)
  - docs/README-project-pulse.md (basic run instructions)
- Validation:
  - Confirm folder layout exists and VS Code launch configuration opens the app.

Step 2 — Design deliverables and tokens (Designer)
- Create/modify:
  - docs/design-spec.md (visual spec, tokens, spacing scale, breakpoints)
  - app/assets/logo.svg
  - app/assets/icons/*.svg (status icons, priority icons)
  - app/assets/mockups/*.png or .fig (hi-fi mockups / screenshots)
- Validation:
  - Designer provides annotated screenshots and a CSS token table.

Step 3 — Data schema & sample data (Coder + Designer)
- Create/modify:
  - app/project-data.json (finalized schema + example dataset — required contents shown below)
- Validation:
  - JSON parses; sample entries render correctly in the UI.

Step 4 — Static HTML structure and semantic markup (Coder)
- Create/modify:
  - app/index.html (header, search/filter placeholders, cards container, accessible ARIA landmarks)
- Validation:
  - Static page renders in browser without JavaScript errors.

Step 5 — CSS system, components, and responsive layout (Coder + Designer)
- Create/modify:
  - app/styles.css (global tokens, grid system, card styles, badges, priority chips, responsive breakpoints)
  - app/index.html (class names / semantics as required by the CSS)
- Validation:
  - Visual spec matches Designer tokens; layout responds at given breakpoints.

Step 6 — Client-side rendering (Coder)
- Create/modify:
  - app/main.js (fetch `project-data.json`, build DOM for project cards, update counts)
  - app/index.html (include script tag)
- Validation:
  - Dynamic rendering works; data updates are reflected on reload.

Step 7 — Accessibility & keyboard interactions (Coder + Designer)
- Create/modify:
  - app/index.html (ARIA attributes, role, semantic tags)
  - app/styles.css (visible focus styles)
  - app/main.js (keyboard handlers where cards are interactive)
- Validation:
  - Keyboard-only navigation, screen reader announcements, and contrast checks pass.

Step 8 — Visual polish & micro-interactions (Designer + Coder)
- Create/modify:
  - app/styles.css (transitions, hover effects)
  - app/main.js (small animations that do not interfere with accessibility)
- Validation:
  - Animations are subtle, accessible; user experience is smooth.

Step 9 — Automated checks & manual test scripts (Coder)
- Create/modify:
  - docs/tests.md (manual test checklist)
  - optionally tests/ (Playwright or Cypress E2E scripts) — recommended
- Validation:
  - Automated tests run and pass; manual checklist completed.

Step 10 — Final integration & launch config (Coder)
- Create/modify:
  - .vscode/launch.json (deterministic config to open `app/index.html` with cwd `${workspaceFolder}/app`)
  - docs/README-project-pulse.md (final run & dev notes)
- Validation:
  - Launch in VS Code opens app root and page successfully.

Required files called out explicitly (must exist):
- app/index.html — Coder: create & own
- app/styles.css — Coder: create & own (Designer to provide tokens)
- app/project-data.json — Coder to create; Designer to review content
- .vscode/launch.json — Coder: create (exact requirement below)

---

## Required content: app/project-data.json (schema + example entries)

Suggested schema (JSON Schema-like structure described in human + example data to drive UI):

Schema (human-readable summary)
- id: string (unique)
- title: string
- description: string
- owner: { name: string, avatar: string (path to asset or null) }
- status: enum ["on-track", "at-risk", "off-track", "complete", "backlog"]
- priority: enum ["low", "medium", "high", "urgent"]
- progress: number (0-100)
- dueDate: ISO-8601 date string or null
- tags: array of strings
- lastUpdated: ISO-8601 date string

Example app/project-data.json (replace asset paths with entries under app/assets):

```json
[
  {
    "id": "proj-001",
    "title": "Website Redesign",
    "description": "Revamp landing pages and mobile experience.",
    "owner": { "name": "Mona A.", "avatar": "assets/mona.svg" },
    "status": "at-risk",
    "priority": "high",
    "progress": 62,
    "dueDate": "2026-08-15",
    "tags": ["web", "ux", "frontend"],
    "lastUpdated": "2026-05-28T10:12:00Z"
  },
  {
    "id": "proj-002",
    "title": "Analytics Migration",
    "description": "Move analytics to GA4 and implement new dashboards.",
    "owner": { "name": "Samir P.", "avatar": "assets/samir.svg" },
    "status": "on-track",
    "priority": "medium",
    "progress": 28,
    "dueDate": "2026-09-01",
    "tags": ["backend", "analytics"],
    "lastUpdated": "2026-05-27T14:00:00Z"
  },
  {
    "id": "proj-003",
    "title": "Mobile App Bugfix Sprint",
    "description": "Resolve critical crashes and performance issues.",
    "owner": { "name": "Tao L.", "avatar": null },
    "status": "urgent",
    "priority": "urgent",
    "progress": 12,
    "dueDate": "2026-06-10",
    "tags": ["mobile", "bugfix"],
    "lastUpdated": "2026-05-29T08:45:00Z"
  }
]
```

Notes:
- "status" maps to visual badges with color tokens provided by Designer.
- "progress" drives a progress bar in the card.
- Avatars are optional; show initials fallback when missing.

---

## Required content: .vscode/launch.json requirement

Make this deterministic configuration explicit:
- Launch configuration must open `app/index.html` in the default browser or the VS Code Live Server extension (if used) with `cwd` set to `${workspaceFolder}/app`. This ensures consistent behavior across developer machines.

Suggested minimal properties to include (deliverable: coder must provide a JSON file at this path that sets the cwd as required and opens index.html):
- File path to create: `.vscode/launch.json`
- Must set: `"cwd": "${workspaceFolder}/app"`
- Must create a launch or debug configuration that opens `app/index.html` (or runs a simple static server with the working directory set to the app folder).

(Implementer: create the final JSON configuration matching your team's preferred VS Code approach; ensure the cwd property above is present and correct.)

---

## Dependencies between steps

- Step 1 (scaffolding) must complete before Steps 4–6 (HTML/CSS/JS) because files and directories are required.
- Step 2 (Design) should start immediately and must finish or provide interim tokens before Step 5 (CSS) and Step 8 (polish).
- Step 3 (data schema) must be finalized before Step 6 (rendering).
- Step 4 (markup) should be completed before Step 6 (rendering) — renderer relies on expected DOM container hooks.
- Step 5 (CSS) is a dependency for Step 7 (accessibility visual focus styling) and Step 8 (animations).
- Step 9 (tests) depends on Steps 4–8 being implemented.
- Step 10 (launch config) depends on Step 1 and Step 6 — app must be runnable.

---

## Which work can run in parallel and which must be sequential (with rationale)

Parallelizable work
- Designer (Step 2) can work in parallel with Coder Step 1 (scaffolding). Rationale: scaffolding doesn't require final visuals.
- Designer finalizing tokens and producing assets can run while Coder builds static HTML structure (Step 4). Rationale: HTML structure and class names can be agreed by a short spec.
- Coder Step 5 (baseline CSS system using tokens) can start with a provisional token file from Designer; Designer can refine tokens in parallel.
- Coder Step 6 (client rendering) can proceed in parallel with CSS refinements as long as class names & container IDs are stable.
- Automated test authoring (Step 9) can start once a minimal render path exists.

Sequential work
- Data schema (Step 3) must be finalized before rendering code (Step 6) because the renderer expects specific fields.
- HTML container creation (Step 4) → renderer injection (Step 6).
- Accessibility testing (Step 7) should follow initial UI implementation (Steps 4–6).
- Final launch config (Step 10) must be applied after the app is runnable.

---

## Designer responsibilities (detailed)

Produce the visual, interaction, and accessibility design deliverables. Deliverables should be committed to `docs/` and `app/assets/`:

1. Visual spec (docs/design-spec.md)
   - Color palette with hex values and usage rules (primary, neutral, status colors for `on-track`, `at-risk`, `off-track`, `complete`, `backlog`).
   - Typography (font family, sizes, line heights, weight scale).
   - Spacing scale (4px baseline: spacing tokens like s-4, s-8,...).
   - Elevation/shadow tokens for cards.
   - Shadow and border radius tokens.

2. Component specification
   - Card layout (thumbnail/avatar position, title, description, status badge, priority chip, progress bar, due date, tags).
   - Status badge designs (color, icon, text patterns).
   - Priority chip variants (low/medium/high/urgent) and their color semantics.
   - Empty states and placeholders for missing avatar or data.

3. Breakpoints & responsive rules
   - Mobile (<= 600px), Tablet (601–1024px), Desktop (>=1025px).
   - For each breakpoint, show how the grid collapses and how many columns.

4. Interaction design
   - Hover, focus, active states for cards and buttons (contrast and accessible size).
   - Micro-interactions (progress bar animation on load, subtle card hover elevation).
   - Motion reduction option (prefers-reduced-motion support).

5. Accessibility constraints
   - Contrast checks for badges and chips (WCAG AA minimum).
   - Keyboard order and focus state visuals.
   - Screen reader labels and phrasing for status and progress.

6. Assets
   - Provide SVG icons and logos in `app/assets/`.
   - Provide at least 3 avatar placeholders.
   - Provide sample screenshots for the README and for reference.

Timing: deliver a first pass (tokens + 1 example card) within 1–2 days so Coders can proceed.

---

## Coder responsibilities (detailed)

Implement, test, and document the UI using lightweight, maintainable code. Preferred stack is vanilla HTML/CSS/JS unless the team chooses a framework.

1. Scaffolding & run instructions
   - Create `app/index.html`, `app/styles.css`, `app/main.js`, `app/project-data.json`, and `.vscode/launch.json`.
   - Provide `docs/README-project-pulse.md` with run instructions (how to open index.html in VS Code via config).

2. Semantic markup
   - Build accessible HTML with landmarks (header, main).
   - Cards should use article/figure semantics where appropriate.
   - Add data-* attributes or class hooks to support rendering.

3. Styling
   - Implement CSS using tokens provided by Designer.
   - Provide responsive grid: 1 column mobile, 2 columns tablet, 3–4 columns desktop (adjust to Designer spec).
   - Implement badges, chips, progress bars, and avatars with fallbacks (initials).

4. Data & rendering
   - Use `fetch('/project-data.json')` to load JSON (path relative to `app/`).
   - Defensive parsing and fallbacks on missing fields (e.g., missing dueDate or avatar).
   - Render progress bars, compute relative due date labels (e.g., "Due in 5 days" or "Overdue").

5. Accessibility & keyboard
   - Implement visible focus states and ensure interactive cards are keyboard operable.
   - Ensure progress bars have accessible text (e.g., aria-valuenow / role="progressbar").
   - Provide ARIA labels that include project title and status.

6. Testing & automation
   - Add basic unit test(s) or snapshot test(s) for the renderer if the team has a test runner. If not, provide Playwright or Cypress E2E scripts that assert at least one card renders for sample JSON.
   - Run Lighthouse (or provide instructions) and fix critical issues.

7. Performance & robustness
   - Minimize main CSS; avoid blocking resources where possible.
   - Provide graceful handling of slow network (loading state) and JSON parse errors (error state and retry).

---

## Edge cases and risks

- Malformed JSON
  - Risk: Fetch or parse fails → UI blank or crashes.
  - Mitigation: Add try/catch, show an error UI with a retry button.

- Missing fields (avatars, dueDate, tags)
  - Mitigation: Provide sensible fallbacks: initials for avatar, "No due date" label, omit tags area.

- Very long text (title/description)
  - Mitigation: Limit lines with ellipsis; provide full text on hover or via accessible expand dialog.

- Timezone and date formatting
  - Risk: Dates inconsistent across users.
  - Mitigation: Use ISO dates in data and format in UI using Intl.DateTimeFormat.

- Color contrast & accessibility
  - Risk: Designer colors may fail WCAG.
  - Mitigation: Add tests/checks; provide alternative accessible variants.

- Browser support
  - Risk: Use of modern CSS/JS features may break older browsers.
  - Mitigation: Target evergreen browsers; avoid cutting-edge features or provide fallbacks.

- Performance with large datasets
  - Mitigation: Implement simple virtualization or pagination if >100 cards expected.

- Motion/animation causing motion sickness or accessibility complaints
  - Mitigation: Respect prefers-reduced-motion.

- Naming & token mismatches between Designer and Coder
  - Mitigation: Agree on token names in docs/design-spec.md.

---

## Validation and testing expectations

For each step indicate manual and automated verification.

Step 1 — Scaffolding
- Manual:
  - Open workspace in VS Code, run launch config, load `app/index.html`.
- Automated:
  - None required.

Step 2 — Design deliverables
- Manual:
  - Review design spec against mockups; confirm tokens exist for colors, spacing, breakpoints.
- Automated:
  - Contrast checks using tools (axe, Color contrast checkers).

Step 3 — project-data.json
- Manual:
  - Validate JSON with a linter or `jq`/`node` parsing command.
- Automated:
  - Add a basic schema test to ensure required fields exist for each entry.

Step 4 — Static HTML
- Manual:
  - Open index.html; check header, container, and placeholders display.
- Automated:
  - HTML validation (W3C validator or linter).

Step 5 — CSS & responsiveness
- Manual:
  - Resize viewport to breakpoints; verify grid and card behavior matches spec.
- Automated:
  - Visual regression snapshots (Percy or Playwright snapshots).

Step 6 — Client rendering
- Manual:
  - Confirm cards render using sample `project-data.json`.
  - Verify progress bar values and badges match data.
- Automated:
  - Unit test for renderer: given sample JSON, ensure DOM contains x cards with expected content.
  - E2E test that loads page and asserts presence of card with a known title.

Step 7 — Accessibility
- Manual:
  - Keyboard-only navigation through cards and controls.
  - Screen reader spot checks (NVDA/VoiceOver).
- Automated:
  - Axe or lighthouse accessibility checks; expect no critical failures.

Step 8 — Visual polish
- Manual:
  - Confirm hover/focus states, animations.
- Automated:
  - Snapshots for key states (hovered card, focused card).

Step 9 — Full integration
- Manual:
  - End-to-end flow: open page, load data, interact with cards, view empty/ error state.
- Automated:
  - Run E2E tests in CI (if available). Lighthouse performance/accessibility score report (suggest thresholds).

Step 10 — Launch
- Manual:
  - Use `.vscode/launch.json` to open the app; confirm correct cwd and that the app loads.
- Automated:
  - CI job that uses a static server serving `app/` and runs accessibility and rendering tests.

Suggested minimal acceptance criteria for merge:
- App loads in a browser and renders sample data.
- Cards display title, owner, status badge, priority chip, progress bar, due date (or fallback).
- Layout matches Designer's breakpoints and tokens.
- Keyboard navigation works; key aria attributes present.
- project-data.json is valid and included.

---

## Work that can run in parallel vs must be sequential (summary)

Can run in parallel:
- Designer producing tokens & assets ↔ Coder scaffolding and static HTML skeleton.
- CSS baseline implementation using provisional tokens ↔ Client-side rendering implementation.
- Test authoring ↔ finishing details of CSS & markup (tests can reference selectors agreed early).

Must be sequential:
- Data schema finalization → renderer implementation.
- HTML container creation → renderer injection.
- Accessibility verification → after interactive behaviors are implemented.

Rationale: parallelism reduces idle time while sequence preserves contract dependencies.

---

## Open questions and assumptions

Open questions to resolve before or early during implementation:
1. Preferred stack: vanilla HTML/CSS/JS or a framework (React, Vue, Svelte)? This affects file layout and test tooling.
2. Will the JSON file remain a local static file, or will it be replaced by an API endpoint? If API, do we need authentication or CORS handling?
3. Browser support & minimum supported versions (affects CSS capabilities).
4. Expected maximum number of projects (affects whether virtualization/pagination required).
5. Should we support dark mode? If yes, Designer should provide dark tokens.
6. Are there required analytics or telemetry events to emit when users interact with cards?
7. Localization/internationalization needs (dates, language); if needed, plan for i18n early.
8. Exact mapping between status text and desired badge colors/icons — Designer to confirm.

Assumptions:
- Project will be implemented as a static single-page app served from the `app/` folder.
- Team has access to basic tools: modern browser, VS Code, ability to run a static file server locally if needed.
- Accessibility is a priority — WCAG AA targeted.

---

End of plan.
