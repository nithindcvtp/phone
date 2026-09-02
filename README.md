# Hospital Telephone Directory — GitHub Pages

## What changed for GitHub Pages

GitHub Pages only serves static files — it can't run `server_2_2.py`, so
`admin.html` can no longer `POST` changes to `/save`. Instead:

- Every add/edit/delete/reorder is now kept as a **draft in your browser's
  localStorage**, so you won't lose work while you're making several changes.
- When you're ready to publish, click **⬇ Download directory.json** in the
  admin panel's top bar. It downloads the updated file.
- Replace `directory.json` in this folder with the downloaded file, then
  commit and push. GitHub Pages will pick it up automatically.
- **↺ Discard Draft** clears your local browser draft and reloads the
  original `directory.json` from the site, if you want to start over.

`directory.html` (the public-facing directory) is unaffected — it just reads
`directory.json` and works as a plain static page.

## Deploying to GitHub Pages

1. Create a new GitHub repository (or use an existing one) and push these
   files to it: `directory.html`, `directory.json`, `login.html`,
   `admin.html`, `style.css`.
2. In the repo, go to **Settings → Pages**.
3. Under **Build and deployment → Source**, choose **Deploy from a branch**.
4. Pick your default branch (e.g. `main`) and the `/ (root)` folder, then
   **Save**.
5. GitHub will give you a URL like
   `https://<your-username>.github.io/<repo-name>/`. It can take a minute or
   two to go live.
6. The public directory is at that URL + `/directory.html`
   (or just `/` if you rename `directory.html` to `index.html`).
   The admin panel is at that URL + `/login.html`.

## ⚠️ Important security note

The admin username/password (`admin` / `hospital123`) is hard-coded in
`login.html`'s JavaScript. On a public GitHub Pages site, **anyone can view
that source and read the password** — this "login" only prevents casual
access, it is not real security. Don't rely on it to protect sensitive
information, and don't reuse this password anywhere else. If you need real
access control, consider:
- Making the repository **private** and using GitHub Pages with a private
  repo (available on paid GitHub plans), or
- Hosting the admin panel separately behind proper authentication, and only
  publishing the read-only `directory.html` + `directory.json` publicly.

## Mobile-friendliness changes

- Added the missing `<meta name="viewport">` tag to `directory.html` and
  `login.html` (this alone was the main reason those pages weren't scaling
  properly on phones).
- `directory.html`: the search bar and department filter now stack cleanly
  under the nav on narrow screens, with larger touch-friendly inputs.
- `login.html` / `style.css`: the login card and background animation now
  scale down and stay centered on small screens instead of overflowing.
- `admin.html`: the sidebar is now an off-canvas menu on phones/tablets
  (tap ☰ to open it), forms stack into single columns, the contact table
  scrolls horizontally instead of squeezing, and inputs use a 16px font on
  mobile to stop iOS from auto-zooming when you tap them.
