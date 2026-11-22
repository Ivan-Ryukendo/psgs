# Tasks

Who builds what, in which order. One card per task in `tasks/`. Status lives in each card and in PROGRESS, not here.

| # | Card | Wave | Depends on | Done |
|---|---|---|---|---|
| 01 | `tasks/01-<slug>-<date>.md` | 0 | none | [ ] |

## Rules for parallel lanes
- A lane edits only the files its card says it owns.
- Shared hot spots (generated types, lockfiles, migrations, router or middleware config) have one owner per task.
- One lane at a time touches the shared database.
- Frontend builds against the card's Contract, never backend source.
