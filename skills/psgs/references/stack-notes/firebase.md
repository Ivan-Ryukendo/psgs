# Stack notes: Firebase

Copy into SECURITY.md when the project uses Firestore, Realtime Database or Firebase Storage.

- **No test-mode rules** (`allow read, write: if true` or rules that expire on a date) in any database or bucket.
- **Rules check identity and ownership:** `request.auth != null` and `request.auth.uid == resource.data.ownerId` (or the path's user ID). Validate the fields and types written (`request.resource.data`).
- **Privileged fields** (role, plan, credits) can't be written by clients. Set them with custom claims or server code only.
- **Admin SDK credentials are server-only.** The Admin SDK bypasses rules.
- **Test rules with the emulator** in CI. Ship rules from the repo, never edit them only in the console.
- **App Check** on the database, storage and callable functions, to limit abuse from outside the app.
- **Storage:** limit size and content type in rules, and keep paths scoped to the user.
- **Callable and HTTP functions** check `context.auth` and validate input, like any other API.
