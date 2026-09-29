# BunnyClock website

The marketing site for **BunnyClock**, an Android attendance app for young students. It is a
plain static site — HTML, one CSS file and a little vanilla JavaScript. No build step, no npm, no
trackers, no cookies, no analytics. The only external link on the page is the Google Play
listing.

```
index.html          the landing page (single page, all sections)
privacy.html        the privacy policy (use this URL in the Play Console)
404.html            friendly “page not found”, links back home
site.webmanifest    optional web app manifest (icons for “Add to home screen”)
.nojekyll           tells GitHub Pages to serve the files exactly as they are
assets/
  site.css          the whole stylesheet, brand tokens at the top
  fonts/            self-hosted Roboto 400 / 500 / 700 / 900 (OFL 1.1)
  icons/            logo + favicon + touch icons
  screens/          app screenshots, 720 px wide WebP
  video/            promo video (16:9 and 9:16 cuts) and their posters
  feature-graphic-1024x500.png   the Open Graph / Twitter card image
```

---

## Publish it on GitHub Pages

1. **Create the repository.** On GitHub, create a new repository (public, or private on a paid
   plan — Pages needs public repos on free accounts). Do not add a README, `.gitignore` or
   licence; you are uploading your own files.
2. **Push these files to `main`.** From inside this folder:

   ```bash
   git init -b main
   git add .
   git commit -m "BunnyClock website"
   git remote add origin git@github.com:YOUR-USER/YOUR-REPO.git
   git push -u origin main
   ```

   The files must sit at the **root** of the repository (`index.html` at the top level, not inside
   a sub-folder). Keep the `.nojekyll` file — without it, GitHub Pages skips some files.
3. **Turn Pages on.** Repository → **Settings** → **Pages** → *Build and deployment* → Source:
   **Deploy from a branch**, Branch: **main**, folder: **/ (root)**. Save.
4. **Wait for the URL.** A minute or two later the site is live at
   `https://YOUR-USER.github.io/YOUR-REPO/`. Reload the Pages settings page to see the link.
5. **Paste the privacy URL into Play Console.** Use
   `https://YOUR-USER.github.io/YOUR-REPO/privacy.html` as the *Privacy Policy URL* in the Google
   Play Console listing. (Until the app is published, the “Get it on Google Play” links show a
   “not found” message from Play — that is expected.)
6. **Optional: a custom domain.** In **Settings → Pages → Custom domain** add your domain. GitHub
   writes a `CNAME` file into the repo for you; keep it. Add the DNS records GitHub shows you, and
   tick *Enforce HTTPS* once DNS has propagated. If the site moves from
   `YOUR-USER.github.io/YOUR-REPO/` to the bare domain, the relative links keep working — no edits
   needed.

## Before you launch — check these values

Everything below is already filled in with real values. It is listed here so you can find and
change it quickly.

| What | Current value | Where |
|---|---|---|
| Support / contact email | `jpgdm24@gmail.com` | `index.html` (footer `mailto:`), `privacy.html` (Contact section and footer) |
| Publisher name | `John Paul Del Mundo` | `privacy.html` → “Contact” section |
| Google Play link | `https://play.google.com/store/apps/details?id=com.luapearth.bunnyclock` | `index.html` — header, mobile menu, hero, Free card, Pro card, final call to action (6 places) |
| Effective date of the policy | `September 29, 2026` | `privacy.html` — under the page title |
| Copyright year | `© 2026` | `index.html`, `privacy.html`, `404.html` footers |

If any of those should be a placeholder instead, replace the text in both files — the values are
plain text, not variables.

### Two things to edit after the first deploy

- **Canonical URL.** In the `<head>` of `index.html` there is a commented-out `<link
  rel="canonical">`. Uncomment it and put in your real URL, e.g.
  `https://YOUR-USER.github.io/YOUR-REPO/`.
- **Open Graph image.** The `og:image` / `twitter:image` tags use the **relative** path
  `assets/feature-graphic-1024x500.png` so the site works from any folder. Most social networks
  prefer an **absolute** URL: after the first deploy, change both tags to
  `https://YOUR-USER.github.io/YOUR-REPO/assets/feature-graphic-1024x500.png`. Then paste the page
  URL into the [Facebook sharing debugger](https://developers.facebook.com/tools/debug/) or
  [X card validator](https://cards-dev.twitter.com/validator) to refresh the cached preview.

## Other things worth knowing

- **Test locally.** Open `index.html` directly in a browser (it works from `file://`), or run a
  tiny server from this folder: `python3 -m http.server 8000` and visit
  <http://localhost:8000/>. Open the browser console — it should stay empty.
- **The video.** The `<video>` element uses `preload="none"`, so the ~10 MB file is only fetched
  when a visitor presses play. It never autoplays. On phones (under 700 px) the page swaps to the
  vertical 9:16 cut and the matching vertical poster; on wider screens it uses the 16:9 cut. Both
  files live in `assets/video/`.
- **Screenshots.** The eight app screens are WebP at 720 px wide (about 285 KB in total), each with
  `width`/`height` set so the layout does not jump while loading. To regenerate them, resize a
  `screens/*.png` to 720 px wide and save as WebP quality ~82.
- **`extras/store-screenshots/`** holds the eight ready-made 1080×1920 marketing slides from the
  original kit. Nothing on the page links to them — they are kept here because they are handy for
  the Play Store listing itself. Delete the folder if you don’t want it in the repo.
- **Placeholders that are intentionally left visible:** none. If you want a literal
  “fill this in” marker, add one where you need it and list it here.
- **Dark mode.** The page is light by default, like the app. If the visitor’s device asks for dark
  mode, the colours switch automatically (`prefers-color-scheme`). Nothing to configure.
- **Editing colours.** All brand colours, radii and shadows are CSS custom properties at the top of
  `assets/site.css`. Changing `--teal` there updates every button, link and accent on all three
  pages.

## Not included, on purpose

No analytics, no cookie banner (there are no cookies), no contact form (the contact link is a
`mailto:`), no newsletter, no chat widget. If you add any of these, they will be the first third
party to see your visitors — decide that deliberately.

## What was checked before handing this over

Measured on this build, served locally over http:

- **Lighthouse** — `index.html`: Performance **98**, Accessibility **100**, Best Practices **100**,
  SEO **100**. `privacy.html`: 98 / 100 / 100 / 100.
- **axe-core** (WCAG 2.0/2.1 A + AA) — **0 violations** on `index.html` (at 1280 px and 360 px),
  `privacy.html` and `404.html`.
- **Layout** — no horizontal scrolling at 320, 360, 768 or 1280 px; all 11 images load; no console
  errors or failed requests.
- **Video** — plays in both aspect-ratio modes with the matching poster; never autoplays.
- **Motion** — with `prefers-reduced-motion: reduce`, no content is left hidden.

Two things still worth a human eye:

1. **Captions for the promo video.** The video has an audio track and no subtitle track. If it
   contains narration or dialogue, WCAG 2.2 AA asks for captions: create a `captions.vtt` and add
   `<track kind="captions" src="assets/video/captions.vtt" srclang="en" label="English" default>`
   inside the `<video>`. If the audio is music only, this can stay as it is.
2. **Fonts when opened straight from `file://`.** Chrome and Firefox block local font files loaded
   from a `file://` page (a browser security rule, not a bug here), so on a double-clicked
   `index.html` the text falls back to your system font. Everything else — layout, images, video —
   works fine from `file://`. Preview over a local server if you want to see the real typography:

   ```bash
   python3 -m http.server 8000
   ```

   On the live GitHub Pages site this never happens.
