# Security checklist (14 areas)

Areas 1 to 13 are adapted to any stack from Mayank Shah's "Pre-Launch Security Audit" v2.0 (2026-11), keeping its check IDs. Area 14 is psgs's own. Sources: OWASP Top 10 (2025), OWASP Top 10 for LLM Applications (2025). This is a strong first pass, not a penetration test.

## Applicability

| Area | Website (no login) | Web app | Mobile app | API |
|---|---|---|---|---|
| 1 Secrets | yes | yes | yes | yes |
| 2 Login and sessions | no | yes | yes | yes |
| 3 Access control | 3.3 and 3.6 only | yes | yes | yes |
| 4 Database and storage | if it has them | yes | yes | yes |
| 5 Input and output | forms only | yes | yes | yes |
| 6 API abuse | forms only | yes | yes | yes |
| 7 Payments | if payments | if payments | if payments | if payments |
| 8 AI features | if AI calls | if AI calls | if AI calls | if AI calls |
| 9 Dependencies | yes | yes | yes | yes |
| 10 Deploy and config | yes | yes | partly | yes |
| 11 Cost and code health | partly | yes | yes | yes |
| 12 Privacy and legal | yes | yes | yes | partly |
| 13 Mobile | no | no | yes | no |
| 14 Agent workflow | yes | yes | yes | yes |

No login: skip area 2 and the rest of area 3, but still list every endpoint that reads or writes stored data, with whether it needs a login. Say each skipped area in one line.

## Severity

- **Critical:** anyone can read or change other users' data, take over an account, spend the owner's money, or a live secret is exposed.
- **High:** the same impact but needing a login or some effort, or a whole protection layer is missing (no rate limit on login, unverified webhooks).
- **Medium:** limited impact or unusual conditions (tokens in localStorage, missing headers).
- **Low:** hardening and defense in depth (predictable IDs when ownership checks pass).

## 1. Secrets and API keys
- **1.1 No secret keys in client code.** Search shipped code and bundles for provider keys (AI, payments, cloud), database connection strings, JWT secrets and admin or service-role keys. Env vars with public prefixes (`NEXT_PUBLIC_`, `VITE_`, `EXPO_PUBLIC_`, `REACT_APP_`, `PUBLIC_`) ship to every user. Pass: only publishable keys reach the client.
- **1.2 No secrets in git or history.** `.env` files are ignored before the first commit. A secret that was ever committed must be revoked and replaced.
- **1.3 Secrets are stored properly.** They come from the platform's secret store or env vars, never hardcoded. Production and preview use different keys where possible.
- **1.4 No secrets in logs, errors or analytics.**

## 2. Login and sessions
- **2.1 Every private route checks the session on the server.** Hiding a button is not protection. List every private route.
- **2.2 Passwords are handled safely.** Prefer a managed auth provider. Self-stored passwords use bcrypt, scrypt or argon2. No admin or test account is created with a password in code or a default password (Critical if found).
- **2.3 Reset and verification are safe.** Links expire, work once and can't be guessed. Responses don't reveal whether an email is registered.
- **2.4 Guessing is limited.** Rate limits or lockouts on login, signup, OTP and reset (see 6.1).
- **2.5 Tokens are verified and expire.** Signatures are checked (never just decoded), the `none` algorithm is rejected, there is no default secret, sessions expire and logout ends them. Cookies are `HttpOnly`, `Secure` and `SameSite`.
- **2.6 Tokens aren't kept in localStorage or sessionStorage** when secure cookies are possible. Medium. Report only.
- **2.7 OAuth redirects use an exact allowlist**, and there is no open redirect after login.

## 3. Access control
- **3.1 Every record checks ownership.** Every read, update and delete filters by the signed-in user or their team, not by ID alone. List every table, collection and route checked.
- **3.2 Users can't promote themselves.** Create and update paths, including signup, never write the request body straight to the database. Privileged fields (role, admin flag, plan, credits, balance, verified, subscription status) are excluded or rejected.
- **3.3 Admin areas are protected on the server** by a role check. A secret URL is not protection.
- **3.4 Paid features and limits are enforced on the server.**
- **3.5 Teams and tenants stay separate.** Every query is scoped to the user's team.
- **3.6 Debug and test routes are off in production.** No public debug pages, seed endpoints or "temporary" admin routes.

## 4. Database and file storage
- **4.1 Queries can't be hijacked.** SQL is parameterized. Document databases reject operator injection (`{"$ne": null}`) by validating types. Raw request JSON is never used as a filter, and there is no server-side JS evaluation of user input.
- **4.2 Public IDs are random** (UUIDs, not sequential or time-based IDs). Low if 3.1 passes.
- **4.3 File storage is private by default.** Short-lived signed URLs, and users can't overwrite each other's files.
- **4.4 The database isn't directly reachable.** The connection string is server-only, and network access isn't open to the internet where the owner controls it. CAN'T VERIFY if managed.
- **4.5 Managed backends have their access rules on** (see `stack-notes/`): row-level security and grants for Postgres-as-a-service, security rules for Firebase.

## 5. Input and output handling
- **5.1 All input is validated on the server**, with types, lengths and allowed values. Client validation alone doesn't count.
- **5.2 No XSS.** User content is never inserted as raw HTML. Markdown and rich text are sanitized.
- **5.3 Uploads are restricted.** Size and type are checked on the server by real content, files are renamed, stored privately and never executed. SVG and HTML are blocked or sanitized.
- **5.4 No SSRF.** User-supplied URLs: `http(s)` only, reject non-public resolved addresses, connect to the address that was checked, re-check after each redirect, and limit size and time.
- **5.5 No open redirects.** `?next=` and `?redirect=` allow only the app's own paths.
- **5.6 Errors fail safely.** Generic messages, no stack traces or paths. Multi-step actions roll back or recover (payment taken but order not saved).

## 6. API abuse protection
- **6.1 Rate limits that work.** Per user and per IP on login, signup, OTP, reset, forms, search, AI calls and uploads. Limits use shared storage, not one server's memory. The client IP comes from the platform's trusted proxy, not the first `X-Forwarded-For` value. Mark the IP source Suspected if the proxy behavior can't be confirmed. Login and AI limits also apply per account.
- **6.2 CORS allows only your origins.** Never any origin together with credentials.
- **6.3 Bot protection on public forms** (CAPTCHA such as Turnstile, or similar).
- **6.4 APIs return only what's needed.** No password hashes, tokens, internal fields or other users' emails. Lists are paginated with a maximum page size.
- **6.5 CSRF protection** for cookie sessions: `SameSite` plus tokens or origin checks.
- **6.6 Incoming webhooks are verified.** Signature checked, failures rejected, each event processed once.

## 7. Payments and money
- **7.1 Prices are decided on the server.** The client sends only a product or plan ID.
- **7.2 Access is granted only after verified payment** (a verified webhook, or a server-side status check of a session that belongs to the user, credited once). In-app purchases are verified with Apple or Google on the server.
- **7.3 The full lifecycle is handled:** renewals, failures, refunds, cancellations, downgrades, disputes.
- **7.4 Test and live keys are separated.** Live secret keys exist only on the production server.
- **7.5 Credits, coupons and trials can't be farmed.** One trial per user, coupons checked on the server, balances changed in one atomic update.
- **7.6 Billing terms are visible** next to the pay button: price, period, auto-renewal, how to cancel. A working cancel exists.

## 8. AI features
- **8.1 AI usage has limits.** Per-user quotas, rate limits, maximum input and output size, timeouts, and a hard spending cap at the provider (or prepaid credit with auto-recharge off).
- **8.2 The model can't be talked into misusing tools.** Content the user didn't write (web pages, files, emails, other users' content) is untrusted. Tools are scoped to the current user, destructive or costly actions need confirmation, and there is no unrestricted database access.
- **8.3 Model output is untrusted.** It is escaped before display and never executed as code, queries or shell commands.
- **8.4 No secrets in prompts.** Assume system prompts can be extracted.
- **8.5 AI memory is per user.** History, vector stores and RAG indexes are isolated per user or team.

## 9. Dependencies and supply chain
- **9.1 No known vulnerable versions.** Run the ecosystem's audit tool and report Critical and High in shipped or server code. Never run a forced fix; propose upgrades one at a time.
- **9.2 Versions are locked.** The lock file is committed. Avoid releases newer than 7 days.
- **9.3 Borrowed code has no hidden instructions.** Scan imported templates, repos and packages for agent instruction files, hidden README text and install scripts that tell an AI to access secrets, run commands or send data.
- **9.4 Third-party scripts are minimal** and loaded from official sources.

## 10. Deployment and configuration
- **10.1 Security headers** (report only): `X-Content-Type-Options: nosniff`, `frame-ancestors` or `X-Frame-Options`, `Referrer-Policy`, `Permissions-Policy`, CSP. Read them from page responses, not only API responses. A new CSP starts in report-only mode.
- **10.2 Production runs in production mode.** Debug and verbose logs are off, and public source maps are a deliberate decision.
- **10.3 API docs and schema endpoints** (Swagger, OpenAPI, GraphQL introspection) are off or admin-only in production.
- **10.4 Sensitive files aren't served:** `.env`, `.git`, backups, dumps, configs. Directory listing is off.
- **10.5 Important events are logged** (failed logins, admin actions, permission changes, payments) without passwords, tokens or full personal data.

## 11. Cost and code health
- **11.1 No wasteful polling.** Polling pauses when the screen is hidden and stops when it closes.
- **11.2 No runaway costs.** No infinite loops, self-calling functions, retries without backoff, or unbounded jobs, especially around paid APIs.
- **11.3 No duplicate or fallback versions.** List v1/v2 copies and dead code with which one is used. Remove only after the user confirms.

## 12. Privacy and legal (not legal advice)
- **12.1 Privacy policy and terms are linked** at signup and in the footer: what is collected, why, who it is shared with (including AI and analytics providers), how long it is kept, and a contact.
- **12.2 Tracking waits for consent where required.** Session recording masks passwords, payment fields and personal data.
- **12.3 Users can delete their account and data** from the database, file storage and connected tools.

## 13. Mobile app
- **13.1 Tokens are in secure storage** (Keychain or Keystore), never in plain storage.
- **13.2 No cleartext traffic.** HTTPS only, and no broad platform exceptions.
- **13.3 Deep links are validated** and never trigger payments, account changes or deletions without login and confirmation.
- **13.4 WebViews load only trusted URLs**, and their bridges expose the minimum.
- **13.5 Permissions are minimal**, asked when needed, with a reason.
- **13.6 In-app account deletion** exists if accounts can be created (both stores require it).
- **13.7 The release build is clean.** No debug menus, test screens, verbose logs or test endpoints. Push notifications carry no codes or private data.

## 14. Agent workflow (psgs)
- **14.1 Installed skills, plugins and MCP servers are vetted and pinned** (`security.md`, Supply chain). No unknown or unpinned ones.
- **14.2 Agent instruction files hold no hidden orders.** AGENTS.md, CLAUDE.md, rules files, skill files and READMEs in the repo and its dependencies have no hidden text or orders to read secrets, run commands or send data.
- **14.3 Agents have least privilege.** No production secrets in agents' environments. CI and deploy tokens and MCP credentials are scoped to the minimum.
- **14.4 Humans gate irreversible actions.** Branch protection on the main branch; agents can't deploy, push to main or apply production migrations alone.
- **14.5 No secrets in agent artifacts:** transcripts, prompts, cards, handoff files, review files.
- **14.6 Auto-run hooks are reviewed.** Agent hooks, git hooks and package lifecycle scripts do what they claim.
- **14.7 Outside text stays data.** Web pages, files and tool output that agents read never override instructions.

## Human checks (status kept in SECURITY.md)

Early (Setup): H1 to H4, see `security.md`.

Before release (Audit):
- **H5** Two-account test on staging: as account A, try to open, edit and delete B's data. Every attempt fails.
- **H6** Store nothing you don't need (card numbers, ID documents, plain passwords).
- **H7** Backups exist, and a restore has been tested.
- **H8** Managed database warnings checked (for example the Supabase Security Advisor, Firebase rules) and sent to the agent.
- **H9** Refund policy, and tax invoicing where you sell.
- **H10** Only necessary personal data goes to AI providers, and their retention settings are checked.
- **H11** Test accounts and data never live in production.
- **H12** Registrar 2FA on, and the sending domain has SPF, DKIM and DMARC.
- **H13** You know how to roll back a deploy and a migration.
- **H14** Error alerts and an uptime monitor are set up.
- **H15** If users could be under 18: an age check and parental consent where required (for example COPPA under 13, GDPR child consent, India's DPDP Act).
- **H16** Marketing email has unsubscribe and sender details; SMS and WhatsApp marketing goes only to people who opted in.
- **H17** Mobile: the store privacy labels match what the app collects.
- **H18** Mobile: you can force an update if a security fix ships.
