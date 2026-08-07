# Green Horizon Farm Manager

A self-contained farm management app for Poultry, Bees, Goats, Sheep, and Oxen —
livestock inventory, production, feed, income & expenses, health records, and
Profit & Loss reports (monthly / yearly / year-to-date).

No account, no server, no internet required after the first load. Your data is
stored only on the device you're using, in the browser's local storage.

## Quickest way to use it (no setup)

Just double-click **index.html** and it opens in your browser, fully working.
This is enough for day-to-day use on a PC. It also works if you copy the whole
folder onto your phone and open `index.html` in Chrome/Safari.

## Installing it as a real app (home screen icon, full-screen, offline)

To get the "installable app" experience — an icon on your home screen /
desktop, opening full-screen with no browser address bar, and working
offline — the files need to be served over `http://` or `https://` (a
security rule browsers enforce for installable apps; it won't work by just
double-clicking the file for this part, though the app itself still will).

The easiest free options, in order of simplicity:

### Option A — GitHub Pages (free, matches your existing GitHub workflow)
1. Create a new GitHub repo (e.g. `green-horizon-farm-app`).
2. Push these files to it:
   ```
   git init
   git add .
   git commit -m "Green Horizon Farm Manager"
   git branch -M main
   git remote add origin https://github.com/<you>/green-horizon-farm-app.git
   git push -u origin main
   ```
3. In the repo on GitHub: **Settings → Pages → Source: main branch → Save**.
4. After a minute, your app is live at `https://<you>.github.io/green-horizon-farm-app/`.
5. Open that link on your phone → browser menu → **Add to Home Screen** (or
   **Install app** on Android Chrome). On desktop Chrome/Edge, click the
   install icon (⊕) in the address bar.

### Option B — Render (since you already deploy there)
1. New **Static Site** on Render, pointed at a repo containing these files.
2. Build command: (none needed) · Publish directory: `.`
3. Once deployed, open the Render URL on your phone and install it the same way.

### Option C — Quick local test (no hosting)
From this folder, run:
```
python3 -m http.server 8080
```
Then open `http://localhost:8080` on the same device to test the installable
behavior before deciding on A or B.

## Your data & backups

- Data lives in this browser's local storage on this device only — it does
  **not** sync automatically between your phone and PC, unless you set up
  Google Drive Sync (below).
- Go to **Setup → Backup & Restore** any time to:
  - **Export backup (.json)** — downloads a file with everything (livestock,
    production, feed, income/expenses, health records, categories).
  - **Import backup (.json)** — restores from a previously exported file.

## Google Drive Sync (optional, live sync)

For automatic, live syncing to your own Google Drive (instead of manual
export/import), the app has a built-in **Google Drive Sync** panel under
**Setup**. This requires a one-time setup on your part — it's free, but it
does take about 10–15 minutes and needs a Google account:

1. Go to [console.cloud.google.com](https://console.cloud.google.com/) and
   create a new project (any name, e.g. "Green Horizon Farm App").
2. **APIs & Services → Library** → search **Google Drive API** → **Enable**.
3. **APIs & Services → OAuth consent screen**:
   - User type: **External**
   - Fill in app name and your email
   - Add scope: `.../auth/drive.file`
   - Add your own Gmail address as a **test user**
   - Save, and leave the app in **Testing** status (fine indefinitely for
     personal use — you don't need Google's full verification review)
4. **Credentials → Create Credentials → OAuth client ID**:
   - Application type: **Web application**
   - Authorized JavaScript origins: add your GitHub Pages URL, e.g.
     `https://henokj2000-prog.github.io`
5. Copy the generated **Client ID**.
6. In the app: **Setup → Google Drive Sync** → paste the Client ID → **Save**
   → **Connect to Google Drive**.

The first time you connect, Google will show an **"unverified app"** warning
— this is expected for your own personal app (it hasn't gone through
Google's public app review, which isn't necessary here). Click
**Advanced → Go to (app name)** to continue.

**What to expect:**
- Once connected, the app can push/pull a single `green-horizon-farm-data.json`
  file in your Drive.
- Turn on **Auto-sync every change** to have every add/edit/delete pushed to
  Drive automatically, or leave it off and use **Sync now** manually.
- The Google sign-in session expires after roughly an hour of inactivity —
  when it does, just tap **Connect** again. There's no way around this
  without a paid backend server, so treat Drive Sync as a convenience layer
  on top of local storage, not a replacement for it — your data is always
  safe on-device regardless of sync status.


## Files in this folder

| File | Purpose |
|---|---|
| `index.html` | The entire app (structure, styling, logic) |
| `manifest.json` | Tells the browser how to install it as an app (name, icon, colors) |
| `sw.js` | Service worker — caches the app so it works offline once installed |
| `icon-192.png`, `icon-512.png`, `icon-512-maskable.png` | App icons |
| `README.md` | This file |
