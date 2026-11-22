# Security

Core doc, committed. Describes the security model and plans, **never open weaknesses**; those live in `docs/security/private/` (gitignored). Rules for agents: the psgs `security.md` reference.

Last audit: never. Next audit: before the first production release.
<!-- Waivers: YYYY-MM-DD: release <x> shipped without audit. Reason: <why>. Decided by: <who>. -->

## Profile (intake)
| Question | Answer |
|---|---|
| Product type | |
| Real user data / live date | |
| User countries | |
| Users under 18 possible | |
| Repo visibility | |
| Payments / AI calls / uploads | |
| Borrowed code, templates, skills | |
| Admins and MFA | |

Active checklist areas: <e.g. 1-6, 9-12, 14>. Skipped: <area: reason>.
Stack notes: <copied below from psgs stack-notes, or none>.

## Model
<!-- who can do what; where each rule is enforced (database policies, server checks); default deny. -->

## Security-sensitive paths
<!-- a fix round touching any of these pauses for the user. -->
- 

## Stack notes
<!-- paste the matching psgs stack-notes here and adapt them to this project. -->

## Human checks
| ID | Check | Status | Date |
|---|---|---|---|
| H1 | Keys ever pasted into a chat, ticket or message rotated | open | |
| H2 | Spending caps or budget alerts on every paid service | open | |
| H3 | Repo visibility known; any pushed secret revoked | open | |
| H4 | 2FA on every dashboard | open | |
<!-- H5 to H18 are added by the first audit; mark n/a when not applicable. -->

## Incident plan
| Key or secret | Revoke at | Update at | Also used by |
|---|---|---|---|

- Who acts: 
- How affected users are told: 
- Security contact: <`/.well-known/security.txt` or an email>
