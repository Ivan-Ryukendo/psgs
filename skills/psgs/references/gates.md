# Gates and review

## Checker (once per phase gate)

Prompt: "Run these commands in order and stop at none: <TEAM.md checks>. Report errors only, as `file:line: message`, grouped by command, at most 40 lines, then one line per command: pass or fail. Do not fix anything. Do not paste passing output."

- Frontend gate: if installed, also run Emil's `break-ui` (worst-case data) and `review-animations` on the changed screens. Findings only.
- **Secret scan, every gate.** Use a scanner if one is installed (for example gitleaks); otherwise search the files changed since the last gate for private keys, provider secret-key patterns, connection strings with passwords, JWT or service-role secrets, secret-looking names behind public env prefixes (`NEXT_PUBLIC_`, `VITE_`, `EXPO_PUBLIC_`, `REACT_APP_`, `PUBLIC_`), and `.env` files that are not ignored. Report masked: first 4 characters + `file:line`.
- **Dependency audit** when the lock file changed since the last gate: the ecosystem's audit tool, Critical and High only, never with a fix or force flag.
- One pass per gate. Lanes run only their changed-file tests while working; the full suite is the Checker's job.

## Fail loop

1. Send the error list to the lane that owns the failing files. Continue the same agent if the host allows it.
2. Re-run the Checker. At most **2 fix rounds**.
3. Still failing: stop. Show the user the errors with a one-line diagnosis for each, and ask: continue or change course?
4. If the user says continue, loop until everything is green, with no round cap. Report every 3 rounds in one line.
5. An error in a file no lane owns: the orchestrator fixes it if it is small, otherwise it asks.
6. **Sensitive-path guard, every round:** run `git diff --stat` against the last gate. If a fix touched a path listed in SECURITY.md's security-sensitive paths, pause, show that part of the diff, and ask, even in the unlimited loop. A fix that loosens security to pass is rejected and sent back (`security.md`, agent rule 1).
7. A secret found by the scan is never "fixed" by deleting it alone. Tell the user it must be revoked and replaced, and add the steps to "Repeat on each environment".

## Reviewer

Runs with **no prior context**: a new agent, not one that wrote the code. Two fixed points, never per edit:

1. **Before any production-apply request** for migration, auth, permission or security changes. Scope: those files only.
2. **Once on the full branch diff** before asking to push.

Prompt: "Review only. Read AGENTS.md, ESSENTIALS, docs/SECURITY.md, and the card's Decisions, Contract and Security sections. Then review `git diff <base>...HEAD -- <paths>`. Look for correctness, data loss and contract mismatches, and run the checks in `security-checklist.md` for the card's security areas, plus the matching stack notes. Label every finding Confirmed or Suspected, and anything you cannot see as CAN'T VERIFY. List every route, table or file you checked. Never call the code secure. Mask secrets. Write code findings to `docs/tasks/NN-review-<scope>.md` (`templates/review.md`) and security findings to `docs/security/private/NN-<scope>-<date>.md` (`templates/security-finding.md`). Report the verdict and the counts by severity in 5 lines."

Handling findings:
- Security or data loss: to the user first, always. The card gets only the summary.
- Report-only findings (`security.md`) become their own card, never part of this fix round.
- Small and local: the orchestrator fixes them.
- Larger: back to the owning lane, then the Checker runs again.
- Record each finding's outcome (fixed, skipped with reason) in the review file.
