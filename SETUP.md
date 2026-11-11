# Waypoint → GitHub Pages (hybrid)

**How it works:** the page lives on GitHub Pages, so your iPhone opens it with no Google sign-in. Apps Script stays on as the back end: it stores the app list and reads each sheet's `App!A1` link. The page shows the last-known list right away, then refreshes it in the background, so it still opens when you're offline.

## 1. Apps Script (about 3 min)
1. Open the Waypoint script project. Replace **Code.gs** with the new one. Leave **Index.html** as it is, because the old page keeps working.
2. Choose **createKey** from the function dropdown, click **Run**, and approve the permissions prompt. Copy the key from the Execution log.
3. Go to **Deploy → New deployment → Web app**:
   - Execute as: **Me**
   - Who has access: **Anyone**
   Then copy the `/exec` URL.

## 2. GitHub (about 3 min)
1. Create a new repo named `waypoint` under your personal account. It has to be **Public** for free GitHub Pages.
2. Upload everything in the `github/` folder: `index.html`, `manifest.webmanifest`, `icon.svg`, `icon-192.png`, `icon-512.png`, `apple-touch-icon.png`.
3. `API_URL` and `API_KEY` are already set near the top of the `<script>` in `index.html`.
4. Go to **Settings → Pages → Deploy from a branch**, then pick `main` and `/ (root)`. After about a minute it's live at `https://<your-username>.github.io/waypoint/`.

## 3. Devices
- **iPhone:** open the URL in Safari, tap **Share → Add to Home Screen**, and remove the old Apps Script icon. No key to enter.
- **Mac:** update the bookmark.

## Notes
- **Trade-off of the built-in key:** the key sits in the public repo, so anyone who finds it could read the app list or edit it. Your apps keep their own access settings. If the list ever gets changed, run `resetToSeed()` or fix it in Edit.
- **Where are edits saved?** Edit/Save writes to the same list in Script Properties, and the old Apps Script page sees the same data.
- **When you change Code.gs later,** go to **Manage deployments → ✏️ → Version: New version**. That keeps the same `/exec` URL.
- **To change the key,** run `createKey()` again and paste the new key into `API_KEY` in `index.html`.
