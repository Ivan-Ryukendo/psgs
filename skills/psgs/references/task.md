# Task: one feature, from idea to PR

## 1. Read

`AGENTS.md`, `docs/ARCHITECTURE-ESSENTIALS.md`, `docs/PROGRESS.md`, `docs/TEAM.md` (plus `docs/TEAM.local.md` if present; it overrides TEAM.md). Not the whole docs folder.

## 2. Grill

Follow `grill.md` on the user's new idea. Read only the PRD and ARCHITECTURE area files the idea touches. Send Researcher lanes for lookups (findings only) while you keep asking.

## 3. Card

Write `docs/tasks/NN-<slug>-<YYYY-MM-DD>.md` from `templates/task-card.md`. NN is the next free number. Fill in:
- decisions (with who and when)
- phases or slices, each shippable alone if possible
- lanes: role, model and effort (from TEAM.md), the files each lane owns, what it reads, what it depends on
- gates, hard stops, not in scope
- an empty Contract and Status section
- **Security:** the checklist areas this task touches, the sensitive paths it changes, and the "Repeat on each environment" section (empty until a fix needs it)

Add a line to `docs/TASKS.md`. If the task adds payments, uploads, AI calls, auth changes or a new third-party integration, say so and suggest a `psgs audit` after it (one question).

## 4. Mockups

If the card has any frontend lane, ask: "HTML mockups first, or apply directly?" (one question). If mockups: the first frontend lane builds variants behind a switcher (Emil's `prototype` skill if installed). The user picks one, it is saved under `docs/design/mockups/NN-<slug>/`, and the port must match it.

## 5. Plan gate

Show a short plan: lanes with their models, owned files, order, gates, hard stops. Ask for "go". Set the card to `Status: approved`. Nothing runs before this.

## 6. Branch

Create the branch from TEAM.md's git model (ask for the name if no pattern exists). Set PROGRESS: `Active task: docs/tasks/<card> (phase 1)`.

## 7. Dispatch

Follow `dispatch.md`. Order inside a phase:
1. The backend lane runs first and writes its exported names into the card's Contract section.
2. The frontend lane starts after the contract exists, on disjoint files. It reads the contract, never the backend source.
3. Researcher lanes can run at any time.
4. Lanes run in parallel only when their owned files do not overlap.

## 8. Gate (end of each phase)

Follow `gates.md`: the Checker runs once, then the fail loop if needed. When a gate passes:
- each lane writes its 3-line status into the card
- the orchestrator commits locally: `<type>: task NN <phase>`
- PROGRESS "Active task" moves to the next phase

## 9. Review

Follow `gates.md` Reviewer: before any production-apply request for migration, auth or security changes, and once on the full branch diff before step 11. The Reviewer checks the card's security areas against `security-checklist.md`. Security findings go to `docs/security/private/`, and the card gets the summary.

## 10. Production or shared-data changes

Show the SQL or the change plus a rolled-back dry-run result. Wait for the user. Never apply alone.

## 11. Close

1. Update PROGRESS: status line, a dated log line, `Active task: none`. Move history to `docs/archive/` if strict token rules cap it.
2. Card `Status: done`, but only when every "Repeat on each environment" step is ticked, and, for a release card, when an audit is done or its waiver is recorded in SECURITY.md. Tick it in TASKS.md.
3. Ask once: push and open a PR into the integration branch? Never merge.
4. Record any new durable decision in its owning doc (PRD, ARCHITECTURE, DESIGN, ESSENTIALS).
