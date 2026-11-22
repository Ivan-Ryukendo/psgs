# psgs spec

Decisions from the design grill (Ivan, 2026-11-13), held in the repo of the app the workflow came from. The skill files implement this. Change this file first when a decision changes. Paths like `references/...` are inside `skills/psgs/`.

## Origin

Generalizes the workflow Ivan used to build a production web app: grill, then a task card, then lanes (Sonnet codes, Haiku researches and checks, Opus reviews), a backend contract, check gates, a review before production, and PROGRESS updated every session. Goal: a portable starter skill that sets up a new project and runs that workflow on any host and any models.

## Decisions

| # | Decision |
|---|---|
| Q1 | One trigger grills, writes the card, then dispatches |
| Q2 | Stop for the user's "go" after the plan; no agents before it |
| Q3 | Roles: Sonnet codes, Haiku researches and checks, Opus reviews before production, the orchestrator plans |
| Q5 | One feature branch, strict per-lane owned files, the orchestrator commits per gate; worktrees only on request |
| Q5+ | Universal: works across hosts and providers; asks which models to use for each role, with defaults or custom choices |
| Q6 | Not global for now. A starter skill: from an idea it writes AGENTS.md (with CLAUDE.md pointing to it), PRD, ESSENTIALS, ARCHITECTURE, ROADMAP, FILE-STRUCTURE and the rest, then runs the workflow |
| Q7 | One skill, mode detected automatically |
| Q8 | 6 roles (Orchestrator, Backend, Frontend, Researcher, Checker, Reviewer), each with a model and effort; presets Claude only, Codex only, Mixed |
| Q9 | Dispatch ladder: native subagent, then CLI or bridge, then handoff file; never a silent model swap |
| Q10 | Token rules: explain strict and light, and the user picks |
| Q11 | Core docs always, optional docs on need |
| Q12 | Ask whether to install ponytail and use it for everything or the backend only; frontend skill from a user link or the taste skill by default; **DESIGN.md always created**; ask mockups or apply directly |
| Q13 | Fail loop: 2 rounds, then ask; if the user says continue, loop until green |
| Q14 | Frontend chain: taste leads, Emil's `emil-design-eng` for motion, `prototype` for mockups, `break-ui` and `review-animations` at the frontend gate |
| Q15 | Commit freely; ask before push or PR; never merge, never push to main, never touch production without SQL and a dry-run |
| Q16 | Stack: Researcher checks versions, orchestrator proposes one stack with reasons, user confirms or swaps |
| Q17 | Setup ends by writing the waves and Wave 0 cards, then asks "Start Wave 0 now?" |
| Q18 | Three states (Setup, Resume, Task) plus Adopt; each lane writes a 3-line status into the card at every gate |
| Q19 | Grill one question at a time throughout; no batched intake |
| Q20 | Design system: show the tiers and pick per project; no default |
| Q21 | Offer `oc` for web reads in Setup |
| Q22 | Choices live in a separate `docs/TEAM.md`; personal overrides in gitignored `docs/TEAM.local.md` |
| Q23 | Adopt step for existing repos; the original app is the first test |
| Q24 | Name: `psgs` (project starter guide skill); to be published on GitHub or a skill registry |
| Q25 | Built in its own repo; an installed copy lives in the original app |
| Q26 | Reviewer has fresh context and runs at two points: before production for migration, auth or security changes, and on the final diff before push |
| Q27 | Mockup question asked for every task with a frontend lane |
| Q28 | (2026-11-23, publishing pass) Setup only for an empty repo; a repo with code, `AGENTS.md` or `CLAUDE.md` but no `docs/TEAM.md` goes to Adopt, which offers to write a missing `AGENTS.md`. Hermes Agent added to dispatch |

## Security decisions (Ivan, 2026-11-14)

Source: Mayank Shah, "Pre-Launch Security Audit" v2.0 (Nov 2026; 14 pages; 67 code checks in 13 areas, 18 human checks; written for Emergent: React, FastAPI, MongoDB, Expo). The PDF file was checked before use: no JavaScript, auto-actions, embedded files, forms or links; the text layer matches the visible pages; the only domains are its 6 citations. The UpGuard "16,326 Supabase databases" figure was not verified, so it is not repeated in psgs.

| # | Decision |
|---|---|
| S1 | Security is built in (Setup intake, card areas, lane rules, Reviewer per area) and there is an Audit mode |
| S2 | Hard rule: never weaken security to pass; a fix round that touches a sensitive path pauses for the user, even in the unlimited loop |
| S3 | Secrets: mask to 4 characters + location, never ask for one, never write one down, revoke and replace on leak, secret scan at every gate |
| S4 | 8 intake questions, one at a time; SECURITY.md becomes a core doc with the active areas and sensitive paths |
| S5 | The 13 areas rewritten for any stack, keeping the PDF's IDs, plus area 14 (agent workflow); stack notes per family, copied on match |
| S6 | Supply-chain scan before any skill or package install, with a verdict and a question; pinned versions; 7-day cooldown; no forced fixes; Adopt scans installed skills |
| S7 | Security finding details always go in the gitignored `docs/security/private/`; cards get a summary |
| S8 | Audit code pass: read-only lanes by area; the Reviewer model takes judgment areas, the light model takes mechanical ones; Confirmed / Suspected / CAN'T VERIFY |
| S9 | One severity-grouped approval question; risky fixes confirmed individually; re-test login, the main feature and payments |
| S10 | Human checks tracked in SECURITY.md; H1 to H4 at Setup, the rest at Audit; one at a time |
| S11 | "Repeat on each environment" blocks closing a card; allowlist domains live in DEPLOY.md; unseen settings are CAN'T VERIFY |
| S12 | Report-only list (headers, CSP, token storage, live CORS, auth swap, forced upgrades) becomes its own staged card |
| S13 | Audit required before each production release (waiver recorded), suggested on risky features, reminded every 3 months, on request |
| S14 | Private one-screen report; committed SECURITY.md holds the per-key incident plan and the security contact |
| S15 | `psgs audit` runs standalone on any repo with a minimal footprint |

## Sources checked (2026-11-13)

- **Emil Kowalski's skills** (`emilkowalski/skills`): `pick-ui-library` prefers Base UI for primitives, then Sonner, cmdk, input-otp, motion, NumberFlow, dnd kit, Virtuoso, zustand, clsx and cva, next-themes. It only runs when invoked by name. `prototype` builds variants behind a switcher.
- **stageshow** (`benjitaylor/skills`): fake product UI for marketing heroes and demos. Opt-in, not part of the app's design system.
- **cook** (`Leonxlnx/cook`, MIT): a long build-and-critique loop that matches reference images. Borrowed: run state kept in project files for resume, and critics with no prior context. Too heavy as a default (8 h floor for demos).
- **oc** (`only-cli/oc`, MIT, actively maintained): a web page becomes a few hundred tokens. Researcher option.
- **ponytail** (`DietrichGebert/ponytail`): plugin installs for Claude Code and Codex; INSTALL.md for other hosts.
- **taste-skill** (`Leonxlnx/taste-skill`): `design-taste-frontend`, installed with `npx skills add`.
- **Library survey** (Haiku Researcher):
  - shadcn/ui has defaulted to Base UI since 2026-07, and Radix is still supported.
  - Base UI 1.9 and Radix 1.8 are both MIT.
  - Sonner 2.0.8, cmdk 1.1.1 and NumberFlow 0.6.2 are healthy.
  - **Vaul is unmaintained.**
  - Magic UI, Aceternity, RareUI, 21st.dev and Beautiful UI are decorative. They have paid tiers (Aceternity Pro $169 to $1,590, Magic UI Pro), and 21st.dev limits free copies to 2 per day. Aceternity's and Beautiful UI's licenses were not read.

## Skill vetting (2026-11-23, before publishing)

Each recommended repo was cloned and read without running anything: manifests, hooks, scripts, network calls, credential access, hidden Unicode and injected instructions. For oc, the npm tarball was compared with the repo. No backdoor or exfiltration was found in any of them.

| Repo | Verdict | Notes |
|---|---|---|
| DietrichGebert/ponytail | Caution | MIT, v5.3.3. Hooks run every session (codebase map, mode tracker, local cost log in `~/.config/ponytail/`); suggests a status-line edit; optional webhook off by default |
| Leonxlnx/taste-skill | Caution | MIT, v2.5.1. Now one skill, `design-taste-frontend` (`brandkit` and `high-end-visual-design` are gone). A Stop hook runs a headless-Chrome gate once a page is armed; fetches photos and icons from Wikimedia, Picsum and icon CDNs |
| Leonxlnx/cook | Clean | MIT. No scripts that auto-run; runs 8 h+ unattended, so its BRIEF.md permissions should say no push and no publish |
| emilkowalski/skills | Clean | MIT. Markdown only; all six cited skills exist |
| benjitaylor/skills (stageshow) | Clean for stageshow | stageshow is MIT (no root license); a code kit that needs `npm install` |
| only-cli/oc | Caution | MIT; npm matches the repo, with provenance. Pin a release at least 7 days old; the optional `impers` dependency downloads a native libcurl without a checksum (`IMPER_DOWNLOAD_LIBCURL=0` stops it) |
| meta/astryx | Clean | MIT, verified Meta org, beta v0.7.x (newest release under 7 days old on the day of checking, so pin). Postinstall only prints a hint. The bare npm `astryx` is a lookalike; the real scope is `@astryxdesign/*`. Added as a Tier 1 base alternative for React web |
| Appllama/appllama-skills | Clean / caution | MIT, trademarked name. `appllama-app-design-skill` is clean (Expo/iOS). `appllama-usage` needs a paid account and a remote MCP server. Mobile add-on only; not a style picker |

Added from this pass: a style-direction question before mockups, a mobile add-on question, a pinned oc version, and install disclosures for ponytail and taste-skill.

## Open items for the refinement session

1. ~~Confirm the CLI flags~~ Checked against each tool's docs on 2026-11-23 (`claude -p --model`, `codex exec -m`, `opencode run -m`, `hermes chat -q -m --oneshot`); still run `--help` on a real install. Codex's current model names are still open.
2. Run Adopt on the original app and fix whatever it gets wrong.
3. Run Setup on a toy idea end to end with each preset.
4. Check the `npx skills add` layout and metadata for publishing (skills.sh), then push to GitHub.
5. Consider evals: a fixed idea in, then check that every core doc exists with no template text left.
6. Run `psgs audit` standalone on a small public repo and on the original app; tune the lane split and the secret-scan patterns.
7. Ask Mayank Shah whether adapting his checklist (areas 1 to 13) in a published MIT skill is fine; the credit is in the README.
