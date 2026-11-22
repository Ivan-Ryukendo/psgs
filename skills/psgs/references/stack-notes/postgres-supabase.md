# Stack notes: Postgres and Supabase

Copy into SECURITY.md when the project uses Postgres directly or through Supabase (or a similar Postgres API layer).

- **RLS on every exposed table**, default deny. Policies check the caller (`(select auth.uid())`, which is evaluated once per query), never just "authenticated".
- **Grants are minimal.** Never fix `42501 permission denied` by granting everything to `anon` or `authenticated`. Grant only the columns and actions a role needs.
- **The `service_role` (or superuser) key is server-only.** Code using it bypasses RLS, so it needs its own ownership checks.
- **SECURITY DEFINER functions** set `search_path = ''`, use fully qualified names, check the caller themselves, and revoke `EXECUTE` from `public` and `anon` unless they are meant to be public.
- **Views bypass RLS by default.** Use `security_invoker = true` (Postgres 15+), or keep views out of exposed schemas.
- **Storage buckets** have their own policies: private by default, with paths scoped to the owner.
- **Privileged columns** (role, plan, balance) are protected by column grants or a trigger, so a user cannot update them on their own row.
- **Migrations** are hand-written and append-only. On shared or production data, run checks in a rolled-back transaction and show the SQL plus the dry-run result before applying.
- **Run the platform's advisor** (Supabase: Dashboard > Advisors > Security) before each release (H8).
- Rate limits and caps that matter go in the database (triggers or functions), not only in one server's memory.
