# Team

Read before dispatching any agent. Personal overrides go in `docs/TEAM.local.md` (gitignored), which wins over this file.

## Roles
| Role | Provider | Model ID | Effort | How dispatched (working command) |
|---|---|---|---|---|
| Orchestrator | | | | this session |
| Backend | | | | |
| Frontend | | | | |
| Researcher | | | | |
| Checker | | | | |
| Reviewer | | | | |

## Sides
| Side | Paths | Discipline | Skills |
|---|---|---|---|
| Backend | | Minimal: smallest complete change | |
| Frontend | | Design-led: follow DESIGN.md | |

<!-- If a skill auto-starts every session (e.g. ponytail), note how frontend lanes turn it off. -->

## Checks (Checker runs these once per gate, in order)
- typecheck: ``
- lint: ``
- test: ``
- build: ``
- secret scan: `` <!-- e.g. gitleaks, or psgs's pattern search on changed files -->
- dependency audit (when the lock file changed): `` <!-- e.g. pnpm audit --audit-level high; never a fix/force flag -->
<!-- add e2e or db checks if the project has them -->

Security: rules and sensitive paths in `docs/SECURITY.md`; pre-release `psgs audit` required.

## Token mode
strict | light. Web reads with oc: yes (version <pinned>) | no.

## Design
- Base: 
- Add-ons allowed: 
- Decorative (opt-in per screen): 
- Tools: 
- Mockups: asked for every task with a frontend lane.

## Git
- Branch model: `feat/*` → `<integration>` → `<main>`
- Commit locally at each passing gate. Ask before push or PR. Never merge. Never push to `<main>`.

## Project hard stops
<!-- e.g. production holds real user data: no fixtures; migrations additive only; show SQL + dry-run before apply. -->
- 
