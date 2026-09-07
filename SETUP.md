# SETUP — Wingman GitHub Wiring (current verified state)

## Status (verified)
- `index.html` exists at the repo root of `ageonz/wingman` (branch `main`).
- GitHub Pages serves the app at `https://ageonz.github.io/wingman/`.
- The Q admin publish pipeline works (commit stamp `v3.1-b…` lands on each publish).
- Known caching behavior: Pages HTML is served with `max-age=600` — always verify
  with a cache-buster: `https://ageonz.github.io/wingman/?cb=<random>`.

## 1. Pages settings (verify once)
Repo → Settings → Pages → Source: "Deploy from a branch" → Branch: **main** → Folder: **/ (root)** → Save.

## 2. Fine-grained PAT (renew every 90 days)
GitHub → Settings → Developer settings → Fine-grained personal access tokens → Generate:
- Name: `wingman-deploy` · Repository access: **Only select repositories → wingman**
- Permissions → Repository permissions → **Contents: Read and write** (nothing else)
- Copy `github_pat_…` into a password manager. Never commit it anywhere.

## 3. Connect the Q admin build (local file only — keep it OFF GitHub)
1. Open `admin/wingman-Q-admin.html` locally.
2. Sign in with an email whose local part contains **"admin"** or **"q"**
   (e.g. `admin@asaptickets.com`, any 6+ char password) → ADMIN chip appears.
3. Settings & Billing → **GitHub Publishing (Admin)** card:
   Owner `ageonz` · Repo `wingman` · Branch `main` · Target path `index.html` · PAT.
4. **Save Config** → **Test Connection** → expect green "Connected to ageonz/wingman".

## 4. Publish ritual (every update, ~30 seconds)
1. **Backup Now** (repo snapshot + local download).
2. **Select public wingman.html to publish** (Rule A — pick the PUBLIC file, never the Q file).
3. Confirmation modal → check File / Size KB / Title / stamp → **Confirm & Publish**.
4. Auto-verify runs after 3s → chip turns green: "Repo verified v3.1-b…".
5. **Open live site (cache-busted)** → login → footer shows the SAME `build v3.1-b…` stamp.
   (The footer stamp now changes on every publish — Defect A fixed via `ensureBuildStamp`.)

## 5. Rollback
Repo → `backups/` → open last good `wingman-backup-<ts>.html` → publish it through the
picker (or revert the commit on GitHub). Pages re-serves within ~1–2 minutes.

## 6. Roster refresh
Team Roster → Upload / Update Agent List → paste or upload the full backoffice
"Agent List (New)" export → parser skips junk lines, dedupes by agent email →
toast: "Imported N agents · M supervisors". Roster is per-browser (localStorage).

## Troubleshooting
| Symptom | Fix |
|---|---|
| 401 / 403 | Regenerate PAT: Contents Read & write, scoped to `wingman` only |
| 404 on publish | Owner/repo/path typo — path must be exactly `index.html` |
| 409 | Auto-retries once with fresh SHA; click Publish again if it persists |
| 422 | You pressed Publish without selecting the public file (Rule A) |
| Site shows old content | Use `?cb=<random>`, Ctrl+Shift+R, or Incognito; wait ≤10 min |
| Pages 404 | Settings → Pages → main / root; toggle to force rebuild |
| Footer stamp unchanged | Apply the `ensureBuildStamp` patch (block [1]) and republish once |
