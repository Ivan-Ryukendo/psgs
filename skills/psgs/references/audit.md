# Audit: security pass before release or on request

Read `security.md` and `security-checklist.md`, plus only the stack notes in `stack-notes/` that match the project. The audit is read-only until the user approves fixes.

## 0. Footprint

- **psgs project** (`docs/TEAM.md` exists): use the TEAM.md models. Set PROGRESS: `Active task: audit <YYYY-MM-DD>`.
- **Standalone** (no AGENTS.md or TEAM.md): use this host's own model for both tiers unless the user picks others. Write only `docs/security/private/` and, after asking, a minimal `docs/SECURITY.md`. Create no other docs.
- Before writing anything: add `docs/security/private/` to `.gitignore` and confirm with `git check-ignore`.

## 1. Intake

Read the project (manifests, config, entry points, routes, schema; not every file). Tell the user in a short list what you detected: product type, frontend, backend, database, login, payments, AI calls, uploads, mobile. Ask them to confirm. Then ask the intake questions from `security.md` that SECURITY.md does not answer yet, one at a time. Set the active areas from the applicability table.

## 2. Code pass (parallel, read-only lanes)

| Tier | Model | Areas |
|---|---|---|
| Judgment | Reviewer, fresh context | 2 Login and sessions, 3 Access control, 4 Database and storage, 5 Input and output, 6 API abuse, 7 Payments, 8 AI features, 14 Agent workflow |
| Mechanical | Researcher or Checker | 1 Secrets, 9 Dependencies, 10 Deploy and config, 11 Cost and code health, 12 Privacy, 13 Mobile |

Each lane gets: its areas from `security-checklist.md`, the matching stack notes, the security-sensitive paths, and the rules in `security.md`. Each lane writes one entry per check to `docs/security/private/audit-<date>-findings.md` (format: `templates/security-finding.md`), and returns only counts plus its failures, at most 3 lines each.

Run nothing destructive. Run dependency audits with the project's own tool (`npm audit`, `pnpm audit`, `pip-audit` and so on), never with `--force` or fix flags.

## 3. Results and one approval question

The orchestrator merges the lanes, removes duplicates and sets severity (`security-checklist.md`, Severity). Send one message:
- one counts line: "41 passed, 6 failed, 3 need you, 4 n/a"
- failures grouped by severity, each at most 3 lines in plain words: what is wrong, what could happen, the fix
- report-only findings in their own short list, each with "becomes its own card"
- one question: "Which should I fix: all Critical and High, everything, or pick by number?"

## 4. Fix round

- Fix only what was approved, Critical first. Each fix goes to the lane that owns the file (or the orchestrator, when standalone).
- Before applying any fix that changes data, a secret, or a security-sensitive path, show it and confirm it on its own.
- Use the smallest change that fixes the root cause, enforced on the server, never only in the UI. Leave no v2 copies or fallbacks. If a mobile app is already live, keep the old API working until users have updated.
- After each fix: re-run that check and record the evidence. If it cannot be verified, say so.
- After the round: the Checker runs the TEAM.md checks. Re-test login, the main feature and any payment flow (on preview or staging), and record the result.
- Every data, secret, config or allowlist fix gets its steps under "Repeat on each environment".

## 5. Human checks

Ask the open, applicable H items from SECURITY.md one at a time (H5 to H18 here; H1 to H4 if still open). Update their status.

## 6. Report

- Write `docs/security/private/audit-<date>-report.md` from `templates/audit-report.md`.
- Show the user the one-screen version.
- Update SECURITY.md: "Last audit" and "Next audit" (3 months on), the human-check statuses and the incident plan, with no weaknesses described.
- Add a clean summary line to PROGRESS and, if there is one, the release card. Set `Active task: none`.
- Ask once: keep the details of fixed findings locally, or delete them?

## 7. Release gate

A release card closes only when the audit report says no Critical issues are open, or when the user waives the gate. Record the waiver in SECURITY.md with the date, the reason and who decided.

## Resume

If PROGRESS says `Active task: audit <date>`, read that date's findings file, then continue from the first step without a recorded result.
