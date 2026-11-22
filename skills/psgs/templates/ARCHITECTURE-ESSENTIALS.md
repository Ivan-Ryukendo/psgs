# Architecture Essentials

Read every session. These rules hold unless the user overrides one in the current session. Strict token mode: keep this under ~8 KB.

## Doc precedence
When docs disagree, the higher one wins. Fix the lower doc in the same session, or flag it.
1. The user's explicit instruction in the current session
2. This file: rules
3. `docs/PRD.md`: scope
4. `docs/ARCHITECTURE.md`: how
5. `docs/DESIGN.md`: visual
6. `docs/FILE-STRUCTURE.md`: where
7. `docs/ROADMAP.md`: when
8. `docs/TASKS.md` and its cards: who builds what
9. `docs/PROGRESS.md`: status only, never a rule
10. `docs/reference/idea.md`: reference only

## Session protocol
1. `AGENTS.md`, then this file, then `docs/PROGRESS.md`
2. Only the PRD and ARCHITECTURE area files the task touches
3. `docs/FILE-STRUCTURE.md` before creating any file; `docs/DESIGN.md` before frontend work
4. Work in phases: finish a layer, then one check pass, then commit
5. Session end: update PROGRESS (status line, one dated log line). A new decision goes into its owning doc plus the PROGRESS decision log.

## Sides
<!-- table: side | discipline in plain words | paths. Same as TEAM.md. -->
| Side | Discipline | Paths |
|---|---|---|
| | | |

Cross-side task: backend part first, then frontend. Never both in one pass.

## Non-negotiable rules
<!-- security model, data rules, auth, privacy, performance budgets, accessibility floors. One line each. -->
- 

## Safety
- Ask before push, PR, dependency or skill install, paid tier, deploy, or any shared or production data change. Show SQL + a rolled-back dry-run first.
- Never merge, never push to the main branch, never run fixtures against production data.
- Security and data-loss findings go to the user first.
- Never weaken security to make an error or check go away. Enforce every rule on the server, never only in the UI.
- Secrets: never in client code, the repo, docs or logs; show only the first 4 characters; never ask anyone to paste one; a leaked one is revoked and replaced.
- Security findings live only in `docs/security/private/` (gitignored). Model, sensitive paths and incident plan: `docs/SECURITY.md`.
- Vet every skill or package before installing; pin versions; no releases newer than 7 days without approval.

## Definition of done
<!-- what every task must pass: checks from TEAM.md, tests for new logic, docs updated, contract written. -->
- 
