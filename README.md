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

## Cloud sync across phones & laptops (Google sign-in)

The plan syncs automatically once you **Sign in with Google** — nothing to type per device.
Access is locked by Firebase security rules to specific accounts, so the public page can't
expose your data. This repo is already wired to the `big-in-japan` Firebase project.

One-time setup in the [Firebase console](https://console.firebase.google.com) (done per project):

1. **Authentication → Sign-in method →** enable **Google**.
2. **Authentication → Settings → Authorized domains →** add your Pages domain
   (`codilechasseur.github.io`).
3. **Realtime Database → Rules →** lock the trip to your accounts, then Publish:
   ```json
   {
     "rules": {
       "japan": {
         "trip": {
           ".read":  "auth != null && (auth.token.email == 'codilechasseur@gmail.com' || auth.token.email == 'jpovarchook@gmail.com')",
           ".write": "auth != null && (auth.token.email == 'codilechasseur@gmail.com' || auth.token.email == 'jpovarchook@gmail.com')"
         }
       }
     }
   }
   ```
4. On the live site → **Cloud sync** panel → **Sign in with Google** on each device. The first
   sign-in from the device that has the plan seeds the shared `japan/trip` node.

The Firebase **web config** (including the API key) is committed in `index.html` — that's expected.
A Firebase web API key is a **public identifier, not a secret**; the security boundary is the rules
above plus the authorized-domains list. GitHub's secret scanner may flag it as a "secret" — that's a
false positive you can dismiss. For good measure, restrict the key in
**Google Cloud Console → Credentials → HTTP referrers** to your domain. To point the app at a
different Firebase project, edit `FIREBASE_CONFIG` near the bottom of `index.html`.

Keep an **Export backup** as an offline safety net regardless.

## Your data

Ticks, notes, and pins are saved in each browser (localStorage). Use **Export backup** to move
everything to another device, or turn on cloud sync above to keep them all in step automatically.
