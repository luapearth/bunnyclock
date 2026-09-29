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

## How this repo is published

**Live:** <https://luapearth.com/bunnyclock/>

The custom domain `luapearth.com` is set on the account's user site (`luapearth/luapearth.github.io`),
so **every** `luapearth.github.io` URL redirects there — including this project site.
`https://luapearth.github.io/bunnyclock/` therefore 301-redirects to
`https://luapearth.com/bunnyclock/`, and that custom-domain address is the one to use everywhere
(canonical tag, Play Console, social posts).

| Thing | Value |
|---|---|
| Repository | `luapearth/bunnyclock` (public) |
| Push remote | `git@github-bunnyclock:luapearth/bunnyclock.git` |
| Access | repo-scoped SSH **deploy key** with write access enabled |
| Pages source | **`gh-pages` branch** — see the warning below |
| Privacy policy URL | `https://luapearth.com/bunnyclock/privacy.html` |

⚠️ **Pages is built from `gh-pages`, not `main`.** Pushing a `gh-pages` branch is what switched
Pages on for this repo. It matters because GitHub's web editor ("Edit this file") edits `main`, the
default branch — so a web-editor change will **not** appear on the site. Until this is switched,
every update must be pushed to **both** branches.

**Recommended once**, in the repo: **Settings → Pages → Build and deployment → Source: Deploy from
a branch → Branch: `main` / `/ (root)` → Save.** After that, `main` alone publishes the site and
the `gh-pages` branch can be deleted so there is only one place to edit.

### Publishing an update

```bash
cd bunnyclock            # this folder
git add -A && git commit -m "Describe the change"
git push origin main
git push origin main:gh-pages   # not needed once the source is main/(root)
```

GitHub rebuilds in about 30–60 seconds. Pages caches assets for up to 10 minutes, so a
hard-refresh (or `?v=2` on the URL) may be needed to see a change.

### Installing the deploy key on a new machine

The key lives outside the repo and is never committed. On another machine: generate a new keypair,
`ssh-keygen -t ed25519`, paste the `.pub` into **Settings → Deploy keys → Add deploy key** with
*Allow write access* ticked, and add a `Host` alias in `~/.ssh/config` pointing at it.

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

### Already done after the first deploy

- **Canonical URL.** `index.html` carries `<link rel="canonical" href="https://luapearth.com/bunnyclock/" />`.
  Change it if the site ever moves to a different address.
- **Open Graph image.** `og:image` and `twitter:image` now use the **absolute** URL
  `https://luapearth.com/bunnyclock/assets/feature-graphic-1024x500.png`, so social networks can
  fetch it. If you change the feature graphic, paste the page URL into the
  [Facebook sharing debugger](https://developers.facebook.com/tools/debug/) or the
  [LinkedIn Post Inspector](https://www.linkedin.com/post-inspector/) to refresh the cached preview.

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
- **Cloudflare rewrites the HTML (worth knowing).** `luapearth.com` sits behind Cloudflare, and its
  *Scrape Shield → Email Address Obfuscation* setting rewrites every `mailto:` link on the page
  into a `/cdn-cgi/l/email-protection#…` link and injects Cloudflare's own
  `/cdn-cgi/scripts/…/email-decode.min.js` into each page. The page is designed to be script-free,
  and without JavaScript the Contact link shows `[email protected]` and goes nowhere. To keep the
  shipped HTML exactly as it is in this repo, turn that setting off in the Cloudflare dashboard.
- **HTTPS.** `https://luapearth.github.io/bunnyclock/` redirects to `http://luapearth.com/bunnyclock/`
  — the redirect lands on plain HTTP. HTTPS itself works on the custom domain (Cloudflare's
  certificate is valid), so the fix is a Cloudflare setting: **SSL/TLS → Edge Certificates → Always
  Use HTTPS = on**. Also tick *Enforce HTTPS* on the Pages custom-domain screen if it is offered.

## Not included, on purpose

No analytics, no cookie banner (there are no cookies), no contact form (the contact link is a
`mailto:`), no newsletter, no chat widget. If you add any of these, they will be the first third
party to see your visitors — decide that deliberately.

## What was checked before handing this over

Measured on this build — first locally over http, then again on the deployed site — and re-measured
after the video poster and canonical changes:

- **Lighthouse** — `index.html`: Performance **98**, Accessibility **100**, Best Practices **100**,
  SEO **100**. `privacy.html`: 98 / 100 / 100 / 100.
- **axe-core** (WCAG 2.0/2.1 A + AA) — **0 violations** on `index.html` (at 1280 px and 360 px),
  `privacy.html` and `404.html`.
- **Layout** — no horizontal scrolling at 320, 360, 768 or 1280 px; all 11 images load; no console
  errors or failed requests.
- **Video** — plays in both aspect-ratio modes with the matching poster; never autoplays.
- **Motion** — with `prefers-reduced-motion: reduce`, no content is left hidden.
- **Deployed site** — the same checks run against `https://luapearth.com/bunnyclock/`: 320/360/768/1280 px
  clean, all images and fonts load, the video picks the 16:9 or 9:16 cut per breakpoint, no console
  errors. The only network artifact is a cancelled request for the 16:9 poster on phones (the
  poster is swapped for the vertical one as the page loads).

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
