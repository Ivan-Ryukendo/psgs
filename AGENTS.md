# psgs: maintainer guide

This repo publishes the `psgs` agent skill. This file explains how to change it. If you are *using* psgs in another project, you don't need this file: install `skills/psgs/` (see README).

## Layout
```
skills/psgs/        THE SKILL (the only folder users install)
  SKILL.md          router: hard rules, mode table, file map; keep under ~6 KB
  references/       one file per mode or topic, loaded only by the modes that list it
  templates/        docs psgs writes into user projects; <placeholders> + <!-- guidance -->
  LICENSE           copy of the root LICENSE (installed copies must carry it)
SPEC.md             every decision (Q1..., S1...), sources, vetting notes, open items
README.md           public page; numbers and tables mirror the skill
CHANGELOG.md        one entry per release
CITATION.cff        version and date must match the release
assets/*.svg        README images (hand-written SVG)
.github/            contributing, security policy, issue and PR templates
```

## How to change psgs
1. **Decision first.** Add or edit the row in `SPEC.md` (next free Q or S number, with the date). Never change behavior without a SPEC row.
2. **Edit the smallest owner.** A rule that applies to every mode goes in `SKILL.md` hard rules. A mode step goes in that mode's reference. A topic (security, dispatch, design) goes in its topic file. Doc shape goes in `templates/`.
3. **Keep the load map true.** If you add a reference file, list it in `SKILL.md` ("Pick the mode" reading list and "Files in this skill").
4. **Write for any host.** No host-only syntax in the rules. Host-specific commands live only in `references/dispatch.md` (the host table) and `README.md` (install table).
5. **Style.** Plain words, short lines, one idea per bullet, no hype. Questions to the user are always one at a time with a recommendation first.
6. **Run the checks below**, then update `README.md` if a table, number or command changed, and add a `CHANGELOG.md` line.

## Checks (run before every commit)
- Every path a skill file mentions exists (prints nothing when all is well):
  ```sh
  cd skills/psgs && grep -rhoE '`(references|templates)/[A-Za-z0-9_./-]+`' . | tr -d '`' | sort -u | while read f; do [ -e "$f" ] || echo "MISSING $f"; done
  ```
- No hidden Unicode (zero-width or bidi) and no URLs in `skills/psgs/references/` except in `skills-and-design.md`.
- `SKILL.md` frontmatter: `name: psgs` and a `description` under 1024 characters.
- No personal data, private project names, real domains, keys or emails anywhere in `skills/psgs/`.
- If a mode's reading list or file sizes changed, re-measure and update the README "Why it is efficient" table and `assets/token-budget.svg`:
  `cd skills/psgs && cat SKILL.md references/task.md references/grill.md references/security.md references/dispatch.md references/gates.md | wc -c` (Task; see SKILL.md for the other modes).

## Adding a recommended skill or library
Vet it first and record the result in `SPEC.md` ("Skill vetting"):
- Clone it read-only and run nothing.
- Read its manifests, hooks, scripts and package lifecycle scripts.
- List its network domains and any env or credential reads.
- Check for hidden Unicode and injected instructions.
- Check the release age (7-day cooldown) and the license.
- Confirm the owner, and look for lookalike package names.

Then add it to `references/skills-and-design.md` with an exact, pinned install command, and to the README tables with its verdict.

## Local copies
If you keep an installed copy in a project (for example `<project>/.agents/skills/psgs/`), it mirrors `skills/psgs/` exactly. After a change, replace that folder's contents with `skills/psgs/`, then run `diff -rq skills/psgs <copy>`. Never edit the copy directly.

## Releasing
1. Bump the version in `CITATION.cff`, the README badge and `CHANGELOG.md`.
2. Commit on a branch, open a PR, merge, then tag `vX.Y.Z` and run `gh release create vX.Y.Z --notes-from-tag`.
3. Never force-push `main`.
