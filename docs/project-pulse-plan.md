## 1) Summary
Build a small static “Project Pulse” dashboard for Mona that is runnable from VS Code, shows project cards from JSON data, and presents a polished, accessible UI.  
The Orchestrator should sequence work so Designer and Coder stay file-conflict-free, with clear handoffs and validation gates before final integration.

## 1.1) Project Pulse goal
Deliver a runnable, polished, and accessible dashboard that reads project data from JSON and clearly communicates project status, activity, and priority for Mona's team.

## 1.2) Implementation phases
1. Planning and contract definition: Confirm scope, define data/UI contract, and identify dependencies.
2. Data and structure build: Create project data and implement dashboard markup/behavior.
3. Visual design and UX polish: Apply styling system, badges, hierarchy, and responsive behavior.
4. Run/debug setup: Add deterministic VS Code launch configuration for reliable dashboard startup.
5. Validation and integration: Verify syntax, rendering, UX quality, and launch behavior.

## 2) Ordered implementation steps
1. Confirm scope and acceptance criteria from the project brief and step requirements.
2. Define a UI/data contract:
   - Required visible fields: name, owner, status, recentActivity, priority.
   - Required UI hooks: dashboard container and project-card card class.
   - Badge/status mapping rules and responsive behavior targets.
3. Create project data source in app/project-data.json using top-level projects array and complete object fields.
4. Build dashboard markup/behavior in app/index.html:
   - Exact page title: Project Pulse.
   - Link styles.css.
   - Load/read project-data.json and render visible project cards.
   - Show status, recentActivity, and priority per card.
5. Implement visual system in app/styles.css:
   - Add .dashboard and .project-card selectors.
   - Add polished card styling (including border-radius and box-shadow).
   - Add status badge styling and responsive layout behavior.
6. Create runnable debug setup in .vscode/launch.json:
   - Strict JSON (no comments).
   - Launch config name: Run Project Pulse Dashboard.
   - Command: python3 -m http.server 5500.
   - Serve from app directory and open http://localhost:%s/index.html via serverReadyAction.
7. Run validation checks (structure, rendering, UX, launch behavior), fix gaps, then finalize handoff.

## 3) File assignments
| File | Primary owner | Responsibilities | Done criteria |
|---|---|---|---|
| app/project-data.json | Coder | Define canonical projects dataset and schema-compliant records | Valid JSON, top-level projects key, each item has name/owner/status/recentActivity/priority |
| app/index.html | Coder | Implement semantic layout, data loading, and project-card rendering | Title is Project Pulse, links styles.css, references project-data.json, renders visible project-card entries with required fields |
| app/styles.css | Designer | Implement polished visual design, hierarchy, badges, spacing, responsive behavior | Contains .dashboard and .project-card, includes border-radius + box-shadow, readable and responsive UI |
| .vscode/launch.json | Coder | Add deterministic VS Code launch config for dashboard run/debug | Valid strict JSON, includes Run Project Pulse Dashboard, serves app/, opens index.html URL |

## 4) Agent responsibilities
- Orchestrator:
  - Own sequencing, dependency enforcement, and integration gates.
  - Ensure no overlapping file edits and resolve handoff blockers quickly.
- Planner:
  - Translate requirements into step order, file ownership, and verification criteria.
  - Track risks and unresolved questions.
- Designer:
  - Own app/styles.css and define visual/accessibility standards.
  - Provide class/state styling contract early so Coder can align markup.
- Coder:
  - Own app/index.html, app/project-data.json, .vscode/launch.json.
  - Implement deterministic behavior, data wiring, and runnable configuration.

## 5) Dependencies between steps/files
1. app/project-data.json schema must be finalized before index rendering logic is completed.
2. Designer’s class/styling contract must be known before final HTML class structure is locked.
3. app/index.html depends on both:
   - Data contract from app/project-data.json.
   - Selector contract from app/styles.css (at least .dashboard and .project-card).
4. .vscode/launch.json depends on final app entry path decision (app/index.html) and server command.
5. Final validation depends on all four files existing and passing syntax + runtime checks.

## 6) Parallel work decisions
### Can run in parallel
1. Designer starts app/styles.css visual system while Coder builds app/project-data.json.
2. Coder can draft .vscode/launch.json while Designer refines responsive polish.
Rationale: Different files, low coupling, no merge conflict risk.

### Must be sequential
1. Data schema agreement before completing index rendering.
2. Selector/class contract agreement before final HTML structure freeze.
3. Launch verification after index file exists and app/ serving path is confirmed.
Rationale: Prevents broken rendering, missing selectors, and incorrect launch target.

## 7) Validation expectations
1. File presence:
   - app/index.html
   - app/styles.css
   - app/project-data.json
   - .vscode/launch.json
2. Syntax correctness:
   - app/project-data.json parses as JSON.
   - .vscode/launch.json parses as strict JSON (no comments).
3. Functional correctness:
   - index title is exactly Project Pulse.
   - index links styles.css and references/loads project-data.json.
   - UI renders multiple project-card elements with status, recentActivity, priority visible.
4. UX/accessibility:
   - Clear visual hierarchy, readable spacing, status distinction, keyboard-readable semantic structure.
   - Responsive behavior works on narrow and wide viewport widths.
5. Runnable setup:
   - VS Code Run and Debug shows Run Project Pulse Dashboard.
   - Launch opens http://localhost:%s/index.html and displays dashboard UI (not directory listing).

## 8) Open questions/risks
1. Data loading method in static HTML:
   - Risk: If opened via file://, JSON fetch may fail; must rely on launch/server flow.
2. Status/priority taxonomy:
   - Open question: Exact allowed values and color mapping rules for badges.
3. Empty/invalid dataset behavior:
   - Risk: UI may break without fallback messaging if projects is empty or malformed.
4. Scope boundaries:
   - Open question: Whether “short contributor-friendly summary” is per card field or page-level intro text.
5. Port and command assumptions:
   - Risk: Port 5500 conflicts in some environments; fallback behavior should be defined if occupied.
