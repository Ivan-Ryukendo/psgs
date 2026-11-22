# Adopt: bring psgs into an existing repo

The repo has code, `AGENTS.md` or `CLAUDE.md`, but no `docs/TEAM.md`. Do not restructure existing docs. If there are no docs at all, read the stack, scripts and layout from package files, config and the top two folder levels instead.

## Steps

1. **Read lightly:** `AGENTS.md`, `CLAUDE.md`, the docs index files and the newest 2 or 3 task cards or plans if they exist. Search archives; never read them whole.
2. **Pre-fill `docs/TEAM.md`** from what you found:
   - roles and models (look for "Sonnet", "Haiku", "Opus", "Codex", "subagent", "lane" in recent cards)
   - sides, their paths and disciplines (for example a "skill split" section)
   - check commands (from `package.json` scripts, Makefile, CI config)
   - git model (branch names in docs and in `git branch -a`)
   - project hard stops (production data, migration rules)
   - token mode (if PROGRESS has a size cap or the docs are split into areas, propose strict)
3. **Confirm each item, one at a time** (`grill.md`). Show what you found and where. Recommend keeping what works.
4. **Write `docs/TEAM.md`.** Add one line to `AGENTS.md` (or the main agent file): "Team, models, checks and workflow: `docs/TEAM.md` (psgs)." Add `docs/TEAM.local.md` and `docs/security/private/` to `.gitignore`.
4b. **Security.** If there is no `docs/SECURITY.md`, pre-fill one from what the code shows (auth, database, payments, AI, uploads, sensitive paths, existing security or audit docs), then confirm the intake answers and H1 to H4 one at a time. If a security doc already exists, add only the missing sections, after asking. Run the supply-chain scan (`security.md`) on every installed skill and report the verdicts. If old review or audit files listing open weaknesses are committed, say so and ask whether to move them to `docs/security/private/`.
5. **CLAUDE.md:** if it is not a pointer to AGENTS.md, ask before changing it. If the user prefers to keep CLAUDE.md as the source, record that in TEAM.md and leave it.
6. **Missing pieces.** If there is no `AGENTS.md`, offer to write one from `templates/AGENTS.md`, filled from the code and any `CLAUDE.md`, with `CLAUDE.md` becoming the pointer (step 5). If PROGRESS has no "Active task:" line, add it. List any missing core docs (see `setup.md` step 10) and ask whether to create each one. Never rewrite an existing doc to match a template.
7. Continue with `task.md`, or `resume.md` if a task is in progress.
