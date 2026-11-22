# Changelog

## 0.1.0 (2026-11-23)

First public release.

- **Five modes**, picked automatically:
  - **Setup:** idea to docs to a wave plan.
  - **Adopt:** an existing repo.
  - **Task:** grill, card, "go", lanes, gates, review.
  - **Resume:** finish an unfinished card.
  - **Audit:** `psgs audit`, on any repo.
- **Six roles**, each with its own model and effort level: Orchestrator, Backend, Frontend, Researcher, Checker, Reviewer.
- **Presets:** Claude only, Codex only, Mixed.
- **Dispatch ladder:** native subagent, then provider CLI, then handoff file. Covers Claude Code, Codex, OpenCode, Hermes Agent and T3 Code.
- **Security built in:**
  - agent rules and a sensitive-path guard
  - a secret scan at every gate
  - supply-chain vetting before installs
  - private findings
  - a 14-area pre-release audit with human checks
  - stack notes for Postgres/Supabase, Firebase, MongoDB, SQL with an ORM, and Expo
- **Design:**
  - a style-direction question
  - design-system tiers: shadcn on Base UI or Radix, or Astryx (beta); add-ons; decorative; tools
  - mockups behind a variant switcher
  - `DESIGN.md` always created
- **Token rules (strict or light)** and optional `oc` web reads.
- **Vetting:** every recommended skill was checked on 2026-11-23 (notes in `SPEC.md`).
