# Stack notes: SQL databases with an ORM or query builder

Copy into SECURITY.md when the project uses Postgres, MySQL or SQLite through an ORM (Prisma, Drizzle, SQLAlchemy, Django, ActiveRecord, Eloquent and so on).

- **Parameterized queries only.** Find every raw-query escape hatch (`$queryRawUnsafe`, `sql.raw`, `text()`, `.extra()`, `whereRaw`) and confirm that no user input is concatenated into it.
- **Mass assignment:** create and update from an explicit allowlist of fields (DTO or schema), never `Model.create(req.body)`.
- **Ownership** is in the `where` clause of every read, update and delete, or in a scoped repository or tenant middleware.
- **The app's database user has least privilege:** no superuser, no DDL rights at runtime. Migrations run with a separate role.
- **Migrations** are reviewed SQL, append-only on shared data, and dry-run before production.
- **Connection string** is server-only. TLS is on for remote databases.
- **N+1 and unbounded queries** have limits (area 6.4 pagination, area 11 cost).
