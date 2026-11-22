# Task NN: <title> (<YYYY-MM-DD>)

Branch `<branch>` from `<base>`. Status: planning | approved | in progress | review | done.
Rules: `docs/ARCHITECTURE-ESSENTIALS.md` and `docs/TEAM.md` hard stops apply.

## Decisions (<who>, <date>)
1. 

## Phases
| Phase | Goal | Sides | Shippable alone? |
|---|---|---|---|
| 1 | | | |

## Lanes
| Lane | Role | Model, effort | Owns (only these) | Reads | Depends on |
|---|---|---|---|---|---|
| B1 | Backend | | | | none |
| F1 | Frontend | | | card §Contract, DESIGN.md | B1 contract |
| R1 | Researcher | | none | | none |

## Gates
| Gate | After | Checks | Extra |
|---|---|---|---|
| G1 | phase 1 | TEAM.md checks | break-ui, review-animations on changed screens |

## Hard stops
Production or shared-data change (SQL + dry-run first), push or PR, security or data-loss finding, gate failed twice, a fix round touching a security-sensitive path.

## Security
- Checklist areas touched: <e.g. 2 login, 3.1 ownership, 5.3 uploads>
- Sensitive paths changed: 
- Audit suggested after this task: <yes (adds payments/uploads/AI/auth/integration) | no>
- Review summary: <e.g. "3 fixed, 1 open (High, owner: user)"; details in docs/security/private/>

## Repeat on each environment
<!-- Every fix that changed data, a secret, env or config, or an allowlist. The card cannot close while any box is unticked. -->
| Step | Environment | Done |
|---|---|---|

## Mockups
Asked: <yes/no>. Approved: `docs/design/mockups/NN-<slug>/<file>` (<date>).

## Contract
<!-- Backend lanes write this per phase; frontend reads only this. One bullet per export:
- `path`: `signature`: behavior, errors, edge cases. -->
### Phase 1

## Status
<!-- Each lane, at every gate, at most 3 lines:
- B1 (<date>): done | doing | blocked. What changed. Next. -->

## Not in scope
- 
