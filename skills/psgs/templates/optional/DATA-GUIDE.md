# Data guide

Created only when the project has a database or seed data.

## Rules
- Schema changes only through migration files, written by hand, never edited after they are applied.
- <additive-only rule if production holds real data>
- One lane at a time applies migrations and regenerates types.
- Test fixtures never touch production. Checks on production run inside rolled-back transactions.

## Seed and import
<!-- where seed data lives, how it is loaded, who may run it. -->

## Generated files
<!-- e.g. database types: command, owner lane, never hand-merged. -->
