# Architecture: <Project name>

How it is built. Index only; read the area file for the task's phase.

<!-- 3 to 5 lines: the shape of the system (client, server, data, external services). -->

| # | Area | Phase | File |
|---|---|---|---|
| 1 | System overview | P1 | `architecture/1-overview.md` |
| 2 | Environments and deploy flow | P1 | `architecture/2-environments.md` |
| 3 | Data model | P1 | `architecture/3-data-model.md` |
| 4 | Auth and permissions | P1 | `architecture/4-auth.md` |
| 5 | Testing | P1 | `architecture/5-testing.md` |
<!-- add areas as the grill finds them: search, images, maps, payments, offline, i18n, rate limits... -->

<!-- Area file format:
# <Area> (<phases>)
Neighbours: [index](../ARCHITECTURE.md)
Rules first, then the design, then open risks. Name exact files, functions and tables. No code blocks longer than a few lines.
Delete this comment. -->
