# Setup: a new project from an idea

Goal: an idea in, a documented project with a team and a first build plan out. Every step uses `grill.md`, one question at a time.

## Steps

0. **Keep the idea.** Save the user's idea word for word to `docs/reference/idea.md`. Later docs cite it as "idea §N".
1. **Product grill.** Problem, users, the first release's scope, what is out of scope, success signal, demo or acceptance criteria, deadline. Feeds `PRD.md`.
2. **Platform and sides.** What is being built (web app, mobile app, API, CLI, extension and so on). Which sides it has (backend, frontend, mobile, infra) and which paths each side owns. Feeds `skills-and-design.md` and `FILE-STRUCTURE.md`.
2b. **Security intake.** Ask the 8 intake questions in `security.md`, one at a time. Then ask the early human checks H1 to H4. List the security-sensitive paths for this project's layout. Feeds `docs/SECURITY.md`.
3. **Stack.** Send a Researcher to check the current stable versions and known issues of the candidates (findings only). Propose one stack with a one-line reason for each choice. The user confirms or swaps any item. Feeds `AGENTS.md` and `ARCHITECTURE.md`.
4. **Team.** Follow `roles.md`: pick a preset, then confirm or change each role's model and effort. Record how each role is dispatched on this host. Feeds `docs/TEAM.md`.
5. **Skills per side.** Follow `skills-and-design.md`: whether to use ponytail and where, the frontend skill (a link from the user, or the taste skill), Emil's skills. Before each install, run the supply-chain scan in `security.md` and show the verdict. Install nothing without a yes for each item.
6. **Design.** `DESIGN.md` is always created. Ask: HTML mockups first, or apply directly? Ask for the style direction (`skills-and-design.md`). Present the design-system tiers and let the user pick each one for this project. If mockups: build variants behind a switcher under `docs/design/mockups/`, and lock DESIGN.md only after the user approves one.
7. **Token rules.** Follow `token-rules.md`: explain strict and light, and the user picks. Offer `oc` for web reads.
8. **Git.** Branch model (default: `feat/*` into `dev`, then `dev` into `main`), and the main branch name. Commit policy: commit locally at each passing gate, ask before push.
9. **Project hard stops.** Anything specific: production data, paid APIs, legal limits, deadlines. These go into `TEAM.md` and `ARCHITECTURE-ESSENTIALS.md`. If the project will be hosted, ask for every real domain (production, custom, preview pattern) for `DEPLOY.md`; allowlists use them.
10. **Write the docs** from `templates/`:
    - Core, always: `AGENTS.md`, `CLAUDE.md` (pointer only), `docs/ARCHITECTURE-ESSENTIALS.md`, `docs/PRD.md` + `docs/prd/`, `docs/ARCHITECTURE.md` + `docs/architecture/`, `docs/DESIGN.md`, `docs/SECURITY.md` (with the matching `stack-notes/` copied in), `docs/FILE-STRUCTURE.md`, `docs/ROADMAP.md`, `docs/TASKS.md` + `docs/tasks/`, `docs/PROGRESS.md`, `docs/TEAM.md`, `docs/archive/`, `docs/reference/`.
    - Optional, only when the grill showed a need: `docs/DEPLOY.md` (hosting), `docs/DATA-GUIDE.md` (database or seed data).
    - Split long docs into an index plus area files: one area per file, named `N-<area>.md`.
    - Add to `.gitignore`: `docs/TEAM.local.md` (personal model overrides), `docs/security/private/` (security findings), `.env*` except an example file.
    - A Researcher or doc-writing lane may draft area files in parallel. The orchestrator writes AGENTS.md, ESSENTIALS and TEAM.md itself.
11. **Read back.** A short summary of every doc and decision. The user confirms or corrects.
12. **Build plan.** Write the waves into `docs/TASKS.md` in dependency order: foundations, data and backend, features, frontend once DESIGN.md is locked, release. The release wave always ends with a `psgs audit` task. Write one card per Wave 0 task from `templates/task-card.md`, with `Status: planning`.
13. **Ask:** "Start Wave 0 now?" If yes, continue with `task.md` from step 3 (the card exists, so grill only its open questions). If no, set PROGRESS "Active task: none" and stop.

## Notes

- If the repo is not a git repo, ask before running `git init`.
- If the idea is tiny (one script, one page), say so, offer a cut-down setup (AGENTS.md, PRD, TASKS, PROGRESS, TEAM only), and let the user choose.
