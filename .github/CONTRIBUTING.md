# Contributing to psgs

Thanks for helping. psgs is a skill, which means it's mostly carefully worded Markdown, so small, precise changes are the most useful kind.

## Good first contributions
- **Host reports.** Run psgs on a host that hasn't been tested yet (Codex, OpenCode, Hermes Agent, Cursor, Gemini CLI). Open an issue with the "Host report" template.
- **Wrong flags or paths.** If a CLI flag or skill folder changed, send a PR that fixes `skills/psgs/references/dispatch.md` or the README install table, and link the docs page.
- **Stack notes.** Security notes for a stack that isn't covered yet, as a new file in `skills/psgs/references/stack-notes/`.

## How to change the skill
Read [`AGENTS.md`](../AGENTS.md) first. In short:
1. Record the decision in `SPEC.md`.
2. Edit the smallest file that owns the behavior.
3. Run the checks listed in `AGENTS.md`.
4. Update the README if a table or number changed.
5. Add a line to `CHANGELOG.md`.

You can do all of this with an agent: open the repo in your host, and it will read `AGENTS.md` (or `CLAUDE.md`).

## Rules for pull requests
- One topic per PR.
- No host-only syntax in the rules, and no personal data, keys or private project names.
- To recommend a new skill or library, include the vetting notes described in `AGENTS.md`.
- Don't weaken a security rule. If you think one is wrong, open an issue first.

By contributing, you agree that your contribution is licensed under the MIT License.
