# crestline-database

Supabase schema migrations and synthetic seed data for the Crestline Insurance partner demo.

Each partner provisions their own Supabase project and applies these migrations to bring the schema and demo data up. The core app expects every table here to exist.

## Prereqs

- A Supabase project (SaaS — no local Docker required)
- Node 20+ and npm

## Apply schema

The migrations in `supabase/migrations/` are plain SQL. Apply each in filename order via your Supabase project's **SQL Editor**:

1. Open your project at https://supabase.com/dashboard
2. Sidebar → **SQL Editor** → **New query**
3. Open `supabase/migrations/20260426000000_agents.sql` from this repo, paste contents, click **Run**
4. Repeat for any future migrations in filename order

## Seed demo data

After the schema is in place, populate it with a small fixed set of demo records.

```bash
cp .env.example .env       # then fill in SUPABASE_URL and SERVICE_ROLE_KEY
npm install
npm run seed:agents        # creates 5 demo CSR agents
```

The service role key is found in the Supabase dashboard → **Project Settings** → **API** → `service_role`. Never commit `.env` — it's gitignored.

### Demo agent credentials (after `npm run seed:agents`)

All 5 share the same password for the demo: `DemoPass123!`

| Email | Name | Role |
|---|---|---|
| alice@crestline.com | Alice Anderson | csr |
| bob@crestline.com | Bob Bennett | csr |
| carol@crestline.com | Carol Chen | csr |
| dave@crestline.com | Dave Davis | csr |
| erin@crestline.com | Erin Evans | supervisor |

To rotate a password before sharing the demo with your team, run from the `core/` repo:

```bash
npm run admin:set-password alice@crestline.com NewPassword123
```

## Repo layout

```
supabase/migrations/        # versioned SQL — apply in filename order
seed/                       # TypeScript scripts that populate demo data
.env.example                # template — copy to .env, never commit
```
