# Postgres Database

This page covers how you can set up your Postgres database for OpenCollective.

### MacOSX

The easiest way to start is to install `Postgres.app` that you can download here: [http://postgresapp.com](http://postgresapp.com). For managing the database, we recommend [Postico](https://eggerapps.at/postico/).

### Populating data

Ask on \#engineering slack channel for scrubbed data dump. \(Once we get a few more eyes on it, we'll share it here directly.\)

Import file in postgres \(replace `[DATE]` with real date of the dump\):

```text
psql opencollective_prod_snapshot_scrubbed < opencollective_prod_snapshot_scrubbed-[DATE].dmp
```

To use the database, run following in your `opencollective-api` directory:

```text
PG_DATABASE=opencollective_prod_snapshot_scrubbed npm run dev
```

Note that the database requires a user `opencollective`.

