# <Project name>

<!-- One paragraph: what it is, for whom, the first release and its deadline. -->

**Every session:** read `docs/ARCHITECTURE-ESSENTIALS.md` (rules), then `docs/PROGRESS.md` (status). Update PROGRESS before you finish. Team, models, checks and workflow: `docs/TEAM.md`. To plan or build: run the `psgs` skill.

## Stack
<!-- One line, items separated by " · ". Exact versions live in package files, not here. -->

## Architecture
<!-- 5 to 8 bullets: the rules an agent must not break (data flow, auth, where logic lives, security model). Details: docs/ARCHITECTURE.md. -->
- 

## Build and run
<!-- install, dev, build; then checks (same commands as TEAM.md). Schema/migration workflow if any. -->
- 

## Sides (critical)
<!-- One line per side: paths and discipline. Full table in docs/TEAM.md. -->
- **Backend** (<discipline>): <paths>
- **Frontend** (<discipline>): <paths>

## Repo
```
<!-- target tree, top two levels, one comment per line. Full tree: docs/FILE-STRUCTURE.md -->
```

## Doc map
| File | Read when |
|---|---|
| `docs/ARCHITECTURE-ESSENTIALS.md` | Every session, first |
| `docs/PROGRESS.md` | Every session, second; update at the end |
| `docs/TEAM.md` | Before dispatching any agent |
| `docs/PRD.md` + `docs/prd/` | Scope; read only the relevant area |
| `docs/ARCHITECTURE.md` + `docs/architecture/` | How; read only the relevant area |
| `docs/DESIGN.md` | Before any frontend work |
| `docs/SECURITY.md` | Before touching auth, data, payments, uploads, AI or config; before release (`psgs audit`) |
| `docs/FILE-STRUCTURE.md` | Before creating files or folders |
| `docs/ROADMAP.md` | Phase planning |
| `docs/TASKS.md` + `docs/tasks/` | Task cards |
| `docs/reference/idea.md` | Only when a doc cites "idea §N" |
