# gainx-backups

Automated weekly Postgres backups for the GAINX project.

This repo intentionally contains **no application code** — only a GitHub Actions workflow that runs `pg_dump` against the production Supabase database every Sunday and uploads the dump as a workflow artifact.

The workflow file lives at `.github/workflows/db-backup.yml`.

## Manual restore

1. Open the [Actions tab](../../actions) and find a successful run.
2. Download the artifact (`gainx-YYYY-MM-DD_HHMM.zip`).
3. Unzip; you get a `.sql.gz` file.
4. Restore against a new database:

```bash
gunzip gainx-YYYY-MM-DD_HHMM.sql.gz
psql "$YOUR_NEW_DB_URL" < gainx-YYYY-MM-DD_HHMM.sql
```

## Required secrets

- `DATABASE_URL` — Supabase Session Pooler connection string (port 5432, not the Transaction Pooler 6543).
