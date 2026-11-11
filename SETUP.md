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
3. Edit `index.html` in GitHub. Near the top of the `<script>`, set
   `var API_URL = 'https://script.google.com/macros/s/…/exec';`
4. Go to **Settings → Pages → Deploy from a branch**, then pick `main` and `/ (root)`. After about a minute it's live at `https://<your-username>.github.io/waypoint/`.

## 3. Devices
- **iPhone:** open the URL in Safari, tap **Share → Add to Home Screen**, then open it from the new icon and enter your key once. The home-screen app keeps its own storage, separate from Safari, so you enter the key there. Remove the old Apps Script icon.
- **Mac:** update the bookmark and enter the key once.

## Notes
- **Is the public repo safe?** Yes. Without the key the API URL returns nothing, so the repo exposes no app links.
- **Where are edits saved?** Edit/Save writes to the same list in Script Properties, and the old Apps Script page sees the same data.
- **When you change Code.gs later,** go to **Manage deployments → ✏️ → Version: New version**. That keeps the same `/exec` URL.
- **If you lose a key or a device,** run `createKey()` again. Every device will ask for the new key.
