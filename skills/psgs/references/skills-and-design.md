# Sides, skills and design system

## Sides

Ask which sides the project has (backend, frontend, mobile, infra and so on) and which paths each one owns. Every path belongs to exactly one side. Write the table into `docs/TEAM.md` and `docs/ARCHITECTURE-ESSENTIALS.md`.

Each side gets a discipline, written in **plain words** in ESSENTIALS, so an agent without the skill still follows it:

- **Minimal** (backend default): smallest complete change; reuse what exists before adding; no speculative abstractions or options. Never cut validation at trust boundaries, error handling that prevents data loss, security or accessibility.
- **Design-led** (frontend default): never minimal on UI. Follow DESIGN.md. Mobile-first ergonomics, accessibility floors (contrast, 44 to 48 px touch targets, reduced motion), real states (loading, empty, error).
- A cross-side task does the backend part first, then the frontend part, never both in one pass.

## Skill questions (one at a time)

1. **ponytail?** Minimal-code discipline. Ask: install it? Use it for everything, or only the backend? Source: `DietrichGebert/ponytail` (Claude Code: `/plugin marketplace add DietrichGebert/ponytail` then `/plugin install ponytail@ponytail`; Codex: `codex plugin marketplace add DietrichGebert/ponytail` then `codex plugin add ponytail@ponytail`; other hosts: its INSTALL.md). It runs hooks every session (a codebase map, a mode tracker, a local cost log under `~/.config/ponytail/`) and suggests a status-line edit: say so before install, and pin a release tag (v5.3.3 checked 2026-11-23). Because it auto-starts, frontend lanes must begin with "stop ponytail".
2. **Frontend skill.** Ask for a link to the user's preferred skill. Default: the taste skill, `npx skills add Leonxlnx/taste-skill`, which ships one skill, `design-taste-frontend` (v2.5). Say before install that it adds a Stop hook: once a page is armed, a headless-Chrome quality gate runs before the agent may stop.
3. **Emil Kowalski's skills** (`npx skills add emilkowalski/skills`, or `--skill <name>` for one): `emil-design-eng` for motion and design detail, `prototype` for mockups with a variant switcher, `break-ui` and `review-animations` at the frontend gate, `mobile-native` for phone-first web apps, `pick-ui-library` when choosing a library (it only runs when invoked by name, so lane prompts must name it).
4. **Mobile projects** (Expo or React Native): offer `appllama-app-design-skill` (`npx skills add Appllama/appllama-skills --skill appllama-app-design-skill`, MIT): native iOS rules, HIG, native controls, Reanimated motion, a simulator check loop. Its sibling `appllama-usage` needs a paid Appllama account and sends queries to a remote MCP server, so offer it only if the user asks for app research. Emil's `apple-design` and `animate-expo` also fit here.
5. **Backend helpers**, if the stack has them (for example the database vendor's own skills). Suggest, never assume.

Before each install, run the supply-chain scan in `security.md` (hidden instructions, install scripts, source, release age of at least 7 days) and show its 3-line verdict. Install each skill only after a yes for that item. Prefer `npx skills add`, which writes to `.agents/skills/` and a lock file that most hosts read. Record installed skills and their side in TEAM.md.

## Design system: tiers (pick per project, no default)

Show the tiers and let the user pick each one. Facts checked 2026-11-13; re-check versions at Setup.

| Tier | Options | Notes |
|---|---|---|
| 1. Base | shadcn/ui on **Base UI** (shadcn's default since 2026-07) or on **Radix** (older, steadier; still supported); or **Astryx** (`meta/astryx`, beta); or none | shadcn: MIT, accessible primitives, Tailwind, `npx shadcn add`. Astryx: MIT, Meta, 150+ React 19+ components, a CLI and 7 themes; React web only, instead of shadcn and never beside it. Install `@astryxdesign/core`, a `@astryxdesign/theme-*` and `@stylexjs/stylex`, plus `@astryxdesign/cli` as a dev dependency, then `npx @astryxdesign/cli init` (it writes agent notes into AGENTS.md or CLAUDE.md: review the diff). Pin exact versions. The bare `astryx` npm package is a lookalike, never install it. Its agent skill: `/plugin marketplace add meta/astryx`, then `/plugin install astryx`; skip its global CLI install |
| 2. Add-ons, added only when a task needs one | Sonner (toasts), cmdk (command menu), NumberFlow (animated numbers, respects reduced motion), input-otp, motion, dnd kit, Virtuoso, zustand, clsx + cva, next-themes | Emil's `pick-ui-library` list |
| 3. Decorative, opt-in per screen | Magic UI, Aceternity UI, RareUI, 21st.dev, Beautiful UI | Landing and marketing screens only. Check reduced motion. Paid tiers (Aceternity Pro, Magic UI Pro, 21st.dev membership) need a yes. Check each component's license |
| 4. Tools, opt-in | `stageshow` (`npx skills add benjitaylor/skills --skill stageshow`): fake product UI for heroes and demos; it ships a code kit that needs `npm install`. `cook` (`Leonxlnx/cook`): long build-and-critique loop to match reference images; runs for many hours, so set its BRIEF.md permissions to no push and no publish | Marketing visuals, not the app's design system |

**Never use Vaul** (drawer): its README marks it unmaintained. Check that no generated component pulls it in.

## Style direction

Ask for the look before any mockup: links or screenshots the user likes, or a pick from a short list (minimal, editorial, bold or brutalist, playful, premium dark, native mobile), plus what to avoid. Record it in DESIGN.md "Direction". With Astryx as the base, map the direction to a theme (neutral or stone for minimal, gothic or y2k for bold, butter, matcha or chocolate for playful and warm). If mockups are on, build 2 or 3 directions as variants behind the switcher, and the user picks one.

## Mockups

Setup asks once for DESIGN.md: mockups first, or apply directly? Task mode asks again for **every task with a frontend lane**. Mockups are HTML, mobile-first, with a variant switcher. Approved ones are saved under `docs/design/mockups/`, and the port must match.
