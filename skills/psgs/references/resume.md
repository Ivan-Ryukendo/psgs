# Resume: continue an unfinished card

No grill. The card is the ledger.

0. If "Active task" is `audit <date>`, follow `audit.md` → Resume instead.
1. Read `docs/PROGRESS.md` and find "Active task". Read that card in full (Decisions, Lanes, Contract, Status). Read `docs/TEAM.md`.
2. Check the repo against the card: `git status`, `git log --oneline -10`, current branch. The last commit should match the last passed gate in the card.
3. If they disagree (uncommitted changes, a missing commit, a different branch), show the difference and ask what to do. Never discard work.
4. Read back in two lines: "Done: <lanes and gates>. Next: <lanes>." Ask one question: continue as planned?
5. Re-dispatch only the unfinished lanes (`dispatch.md`). Every lane prompt includes the card's current Contract and its own last Status line.
6. Continue `task.md` from the step where the card stopped.
