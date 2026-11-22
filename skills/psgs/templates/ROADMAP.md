# Roadmap

When things happen. Scope is in PRD; tasks are in TASKS.

## Phases
| Phase | Goal | Gate to leave it | Target date |
|---|---|---|---|
| P1 | <first release> | <acceptance from prd/4> | |
| P2 | | | |

## Waves (P1)
<!-- dependency order: foundations -> data/backend -> features -> frontend (after DESIGN.md is locked) -> release. -->
| Wave | Contains | Depends on |
|---|---|---|
| 0 | Foundations: repo, tooling, CI, env | none |
| 1 | Data and backend | 0 |
| 2 | Features | 1 |
| 3 | Frontend | 2 + DESIGN.md locked |
| 4 | Release | 3 |

## Git and deploy cycle
<!-- branch -> PR -> preview -> merge -> release. Who approves. -->

## Risks
| Risk | Watch for | Plan |
|---|---|---|
