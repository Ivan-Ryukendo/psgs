# Stack notes: MongoDB and document databases

Copy into SECURITY.md when the project uses MongoDB or a similar document store.

- **Operator injection:** validate types with a schema library, so strings stay strings. A login with `{"password": {"$ne": null}}` must not match. Never pass raw request JSON as a filter or update.
- **No server-side JavaScript** with user input: `$where`, `$function`, `$accumulator`, mapReduce.
- **Ownership in every query:** `{ _id: id, user_id: currentUser.id }`, never `_id` alone.
- **Updates use allowlisted fields** (`$set` built from known keys), so privileged fields can't be mass-assigned.
- **Projections** exclude hashes, tokens and internal fields from responses.
- **ObjectIds are partly predictable** (timestamp plus counter). Use random UUIDs for public IDs (Low if ownership checks pass).
- **Network access list** is not `0.0.0.0/0`, and the database user has least privilege (no `root` for the app).
- **Connection string** is server-only.
