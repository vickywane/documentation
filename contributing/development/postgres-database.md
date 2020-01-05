---
description: This page describes how to interact with the Postgres database
---

# Postgres Database

When developing on the API locally, you'll often have to make change to the database. This page describes how to achieve that.

## Create a migration

This will create a file in `migrations/` where you'll be able to put your migration and rollback procedures:

```bash
# The name of the migration should use snake case
npm run db:migration:create -- --name name-of-your-migration
```

## Run migrations

This will run all the migrations in `migrations/`:

```bash
npm run db:migrate
```

## Rollback last migration

```bash
npm run db:migrate:undo
```

