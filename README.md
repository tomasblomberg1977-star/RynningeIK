# Rynninge IK – Coach App

React/Vite app för tränarplanering. Deploy via GitHub → Vercel.

## Supabase (delad data mellan enheter)

Appen stödjer delad data via Supabase (gratis tier).  
Utan Supabase fungerar appen lokalt med localStorage.

### Sätt upp Supabase (5 min)

1. Skapa konto på [supabase.com](https://supabase.com) → New project
2. Gå till **SQL Editor** och kör:

```sql
create table rik_kv (
  key text primary key,
  value jsonb not null,
  updated_at timestamptz default now()
);
alter table rik_kv enable row level security;
create policy "allow all" on rik_kv for all using (true) with check (true);
```

3. Gå till **Settings → API** och kopiera:
   - **Project URL** → `VITE_SUPABASE_URL`
   - **anon public key** → `VITE_SUPABASE_KEY`

4. I Vercel: **Settings → Environment Variables**, lägg till:
   - `VITE_SUPABASE_URL` = din project URL
   - `VITE_SUPABASE_KEY` = din anon key

5. Redeploy – alla ändringar synkas nu mellan alla enheter i realtid!

## Lokal utveckling

```bash
npm install
npm run dev
```

Lägg till en `.env`-fil för Supabase lokalt:
```
VITE_SUPABASE_URL=https://xxx.supabase.co
VITE_SUPABASE_KEY=eyJ...
```
