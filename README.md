# Japan 2026 · Family Itinerary

A clean, editable single-page itinerary for our Sep 4–15, 2026 trip (Tokyo · Osaka · Kyoto),
with an OpenStreetMap view, a booking checklist, per-day notes, backup export/import, and
optional cloud sync across devices.

**`index.html`** is the whole app — one self-contained file. `japan-itinerary.html` is the
same content without the page wrapper (used for the claude.ai preview); you can ignore it.

## Deploy (GitHub Pages)

1. Push this repo to GitHub (already done if you're reading this there).
2. **Settings → Pages → Source: Deploy from a branch → `main` / `root` → Save.**
3. Wait ~1 minute; your site goes live at `https://<username>.github.io/biginjapan/`.

The map (OpenStreetMap tiles) and cloud sync need a real host like this — they don't work
inside the claude.ai preview sandbox.

## Cloud sync across phones & laptops (optional)

Sync is off until you connect a free Firebase Realtime Database (uses your existing Google account).

1. [console.firebase.google.com](https://console.firebase.google.com) → **Add project** (skip Analytics).
2. **Build → Realtime Database → Create Database** → start in test mode.
3. Open the **Rules** tab and set (test mode expires after 30 days, this doesn't):
   ```json
   { "rules": { ".read": true, ".write": true } }
   ```
   Publish.
4. Copy the database URL (`https://<project>-default-rtdb.firebaseio.com`).
5. On the live site → **Cloud sync** panel → paste the URL + a trip code (e.g. `our-japan-trip`) → **Connect**.
   Enter the same URL + code on every device. Refresh a device to pull the latest.

The Firebase URL is entered in the running app and saved per-device — it is **not** stored in
this repo, so a public repo exposes no private data. Keep an **Export backup** as a safety net.

## Your data

Ticks, notes, and pins are saved in each browser (localStorage). Use **Export backup** to move
everything to another device, or turn on cloud sync above to keep them all in step automatically.
