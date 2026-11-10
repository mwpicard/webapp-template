# Project Instructions

<!-- FILL IN: one paragraph on what this app is and who uses it. -->

- Production URL: https://EXAMPLE.org (GitHub Pages, deploys from `main`)
- Supabase project ref: `FILL_ME`
- DB password env var: `SUPABASE_DB_PASSWORD_FILL_ME` (in ~/.zshrc)

## Git Workflow

**Test exhaustively, then push automatically** (Martin, 2026-11-10; replaces "never push without asking"). Pushes to `main` go live straight away. So test thoroughly first, preferably live in the browser with real clicks. Then push, watch the deploy, check the live site, and report what went live. Work in small, verified slices.

**Coordinate with the other Claude sessions** sharing this tree. Message them before committing or pushing. Commit only your own hunks. Run `git fetch && git log origin/main..main` before a push. Agree on one pusher per batch, and push in sequence.

**Always ask before deleting code or data**, such as files, functions, features or UI, or DB rows, tables or storage. Say exactly what would go and why, then wait for a yes.

## Feature Protection

Before every commit, review `features.md` for features touching the files you
modified and verify the *behavior* is preserved, not just the code structure.
Add new features to `features.md` as they land.

## Database Rules

- Read `database/CURRENT-SCHEMA.sql` before writing or modifying ANY query.
  Never assume table or column names.
- Schema changes go in `supabase/migrations/`, then run
  `./database/regenerate-schema-snapshot.sh` to refresh the snapshot.
- Every table has RLS enabled and policies written the moment it is created.

## Supabase Edge Functions

```bash
/opt/homebrew/bin/supabase functions deploy <name>
/opt/homebrew/bin/supabase functions logs <name>
```
Deploy automatically after creating or modifying a function in `supabase/functions/`.

## Verification

Serve locally with `python3 -m http.server 8080` and drive the browser
(Playwright MCP / Chrome extension) to verify each feature before committing.
