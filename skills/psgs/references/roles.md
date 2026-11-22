# Roles and presets

Six roles. Each gets a provider, a model and an effort level. Record them in `docs/TEAM.md`.

| Role | Does | Never |
|---|---|---|
| Orchestrator | The session the user talks to. Grills, writes cards and the core docs, dispatches, integrates, commits, fixes small review findings | Starts agents before "go"; merges |
| Backend | Backend lanes: data, server, API, auth, scripts. Writes the Contract | Edits files it does not own |
| Frontend | UI lanes and mockups. Builds against the Contract | Reads backend source; edits files it does not own |
| Researcher | Codebase lookups, inventories, web research, version checks | Edits files; returns file dumps |
| Checker | Runs TEAM.md checks once per gate; reports errors only | Fixes code |
| Reviewer | Fresh-context review of risky changes and the final diff | Shares context with the coders |

## Presets

Offer these in Setup. The user accepts one, then can change any single role.

| Role | Claude only | Codex only | Mixed |
|---|---|---|---|
| Orchestrator | Opus, high | top GPT coding model, high | Opus, high |
| Backend | Sonnet, medium | top GPT coding model, medium | top GPT coding model, medium |
| Frontend | Sonnet, low or medium | top GPT coding model, medium | Sonnet, medium |
| Researcher | Haiku, low | small GPT model, low | Haiku, low |
| Checker | Haiku, low | small GPT model, low | Haiku, low |
| Reviewer | Opus, high | top GPT coding model, high | a different provider from the coders, high |

Model names change. At Setup, check what the host offers (its model list, `--help`, or ask the user) and record exact IDs in TEAM.md. For reference, as of 2026-11: Claude `claude-opus-5-5`, `claude-sonnet-5-5`, `claude-haiku-5-5`. For Codex, ask the user for the current top and small model names.

## Effort

- low: mechanical work with a clear spec (checks, lookups, small UI tweaks)
- medium: normal feature code
- high: planning, review, security, data migrations, anything hard to undo

If a host has no effort setting, write "n/a" and pick the model by weight instead.

## Why this split

The expensive model plans and reviews, where judgment matters. The mid model writes code against a clear card. The small model does work where the answer is checkable (a check passes or fails; a file exists or not). A reviewer with no prior context is not biased by the coders' reasoning.
