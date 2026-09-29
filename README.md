# BunnyClock website

A plain HTML/CSS website ready for GitHub Pages. There is no build step, framework, npm dependency, analytics, cookie or tracker. Roboto and every image/video are served locally. The small inline script only tidies the native mobile menu; navigation and FAQs also work without JavaScript.

## Publish on GitHub Pages

1. Create a GitHub repository. Copy **the contents of this folder**, including the empty `.nojekyll` file, into the repository root. Do not put the surrounding Website Kit or original assets into the published repository.
2. Commit and push these files to the `main` branch.
3. Open the repository’s **Settings › Pages**. Choose **Deploy from a branch**, then **main** and **/ (root)**. Save.
4. Wait for GitHub to show your published URL: `https://<user>.github.io/<repo>/`.
5. Use `https://<user>.github.io/<repo>/privacy.html` as the **Privacy Policy URL** in Google Play Console.
6. Fill in the placeholders below before launch. After deploying, check the published links, video and Google Play listing.
7. Optional: configure a custom domain in Settings › Pages, configure its DNS, and add a `CNAME` file at the repository root containing only your domain. Keep all page and asset links relative.

## Contact details and remaining placeholders

Support email is **jpgdm24@gmail.com**, including all footer links and the privacy-policy contact link. The privacy-policy publisher is **John Paul Del Mundo**. These details have been filled in.

| Placeholder | Where | What to change |
| --- | --- | --- |
| `[your site URL]` | — none left — | **Done.** The homepage carries `<link rel="canonical" href="https://luapearth.com/bunnyclock/">` and the policy `…/privacy.html`. The 404 page deliberately has **no** canonical: it is served with a 404 status, so a canonical would point at a URL that does not exist. It carries `<meta name="robots" content="noindex, follow">` instead, which is the directive that matters there. |
| `<user>`, `<repo>` | Example URLs in this README | Substitute your GitHub username/organization and repository name. |

The two social-image references in `index.html` (`og:image` and `twitter:image`) deliberately use `assets/feature-graphic-1024x500.png`. After the first deploy, replace both with the absolute image URL, for example `https://<user>.github.io/<repo>/assets/feature-graphic-1024x500.png`, so sharing crawlers can resolve them reliably. Those are deployment values, not third-party assets.

## What to review before launch

- All Google Play buttons point to `https://play.google.com/store/apps/details?id=com.luapearth.bunnyclock`. The link becomes useful once the app is published. Confirm the listing is live before announcing the site.
- Free stays free forever. Prices are in **Philippine pesos**: Pro is **₱149/month**, Ultimate is **₱219/month, Coming soon** (no purchase button). Billing runs through Google Play, which shows each buyer their own local currency — keep the Play Console price for the PH region in step with these figures. Cloud sync and backup are **not available**; keep that distinction explicit in any edits.
- The privacy policy was restyled from the supplied `assets/privacy.html`. Its sections and disclosures were retained, including the effective date, **September 29, 2026**, and the Google ML Kit diagnostic-data disclosure. The contact email is jpgdm24@gmail.com and the publisher is John Paul Del Mundo, as confirmed by the owner.
- Have the publisher check that the policy still describes the shipping app. In particular, reconcile the supplied “no tracking” product statement with the supplied disclosure that ML Kit may send Google limited device/app diagnostics. Do not silently remove that disclosure. This site does not perform those requests.
- All students in the screenshots are fictional. The camera screenshot remains masked exactly as provided.
- The privacy policy preserves two user-activated source links to Google’s ML Kit disclosure and Google’s privacy policy. They do not load external resources. All pages make zero external requests while being viewed; Google Play and policy reference pages open only when their links are activated.
- The supplied video is unchanged. It plays only after the visitor starts it, using native controls. Its poster is local and `preload="none"` avoids downloading the MP4 during normal page loading.

## Files and editing

- `index.html`: landing-page content, prices, FAQ, SEO/sharing tags, and the small mobile-menu script.
- `privacy.html`: privacy policy and publisher/contact details.
- `404.html`: friendly missing-page screen and relative home link.
- `assets/style.css`: shared styles, exact brand tokens, self-hosted font declarations and responsive layouts. Light theme only. Reduced-motion preferences are respected.
- `assets/screens/`: seven optimized WebP screenshots, 720 × 1607, preserving the original full screen. No unused PNG fallbacks.
- `assets/icons/`: only the supplied logo and favicons used by the pages.
- `assets/fonts/`: only the Roboto weights used (400, 700, 900).
- `assets/video/`: the landscape MP4 and a 1280 × 720 optimized poster. No unused vertical video.
- `assets/feature-graphic-1024x500.png`: original sharing graphic, optimized losslessly.
- `.nojekyll`: keep this empty file so GitHub Pages serves files as-is.

Keep internal links relative (`index.html`, `privacy.html`, `assets/…`), without a leading `/`, so repository subpaths and custom domains both work. Google Play, email, canonical and sharing URLs are the intentional exceptions.

GitHub serves `404.html` for missing URLs. Its relative links work for missing pages directly beneath the repository root; a missing URL in deeper, arbitrary folders resolves relative links there instead. This is a limitation of the required all-relative 404 page. Keep published links to these root-level pages and avoid inventing nested routes.

## Preview and checks

Open `index.html` directly in a browser to use `file://`, or from this folder run:

```sh
python3 -m http.server 8765
```

Then open `http://localhost:8765/`. Python is only an optional local preview tool, not a deployment dependency.

Validation results from September 29, 2026:

- All three pages open through `file://` and a local HTTP server without console errors or failed local resource responses.
- Landing page visually checked at 360, 768 and 1280 CSS pixels; all three pages swept from 320 to 1440 pixels in 16-pixel increments with no horizontal overflow. All screenshots load, images have explicit dimensions, and each page has one H1. Menu/FAQ controls, keyboard Escape, reduced motion, 200% text enlargement and video playback were verified.
- Lighthouse **11.6.0** using installed Chrome for Testing **126**, mobile 360 × 800, local HTTP server: **Performance 95, Accessibility 100, Best Practices 100, SEO 100**. Scores are a local measurement, not a guarantee for other browsers, devices or hosting conditions. Re-run Chrome DevTools › Lighthouse against the deployed URL.
- Current assets plus HTML/CSS are under 1 MB excluding the video, below the requested ~1.5 MB budget. The MP4 is not downloaded until playback.

Font licensing information is included below. Original source assets remain outside this delivery folder in the Website Kit.

## Roboto license

The provided Roboto Latin fonts are self-hosted unchanged. [Official Roboto license source](https://github.com/googlefonts/roboto-3-classic/blob/main/OFL.txt).

```text
Copyright 2011 The Roboto Project Authors (https://github.com/googlefonts/roboto-classic)

This Font Software is licensed under the SIL Open Font License, Version 1.1.
This license is copied below, and is also available with a FAQ at:
https://openfontlicense.org


-----------------------------------------------------------
SIL OPEN FONT LICENSE Version 1.1 - 26 February 2007
-----------------------------------------------------------

PREAMBLE
The goals of the Open Font License (OFL) are to stimulate worldwide
development of collaborative font projects, to support the font creation
efforts of academic and linguistic communities, and to provide a free and
open framework in which fonts may be shared and improved in partnership
with others.

The OFL allows the licensed fonts to be used, studied, modified and
redistributed freely as long as they are not sold by themselves. The
fonts, including any derivative works, can be bundled, embedded, 
redistributed and/or sold with any software provided that any reserved
names are not used by derivative works. The fonts and derivatives,
however, cannot be released under any other type of license. The
requirement for fonts to remain under this license does not apply
to any document created using the fonts or their derivatives.

DEFINITIONS
"Font Software" refers to the set of files released by the Copyright
Holder(s) under this license and clearly marked as such. This may
include source files, build scripts and documentation.

"Reserved Font Name" refers to any names specified as such after the
copyright statement(s).

"Original Version" refers to the collection of Font Software components as
distributed by the Copyright Holder(s).

"Modified Version" refers to any derivative made by adding to, deleting,
or substituting -- in part or in whole -- any of the components of the
Original Version, by changing formats or by porting the Font Software to a
new environment.

"Author" refers to any designer, engineer, programmer, technical
writer or other person who contributed to the Font Software.

PERMISSION & CONDITIONS
Permission is hereby granted, free of charge, to any person obtaining
a copy of the Font Software, to use, study, copy, merge, embed, modify,
redistribute, and sell modified and unmodified copies of the Font
Software, subject to the following conditions:

1) Neither the Font Software nor any of its individual components,
in Original or Modified Versions, may be sold by itself.

2) Original or Modified Versions of the Font Software may be bundled,
redistributed and/or sold with any software, provided that each copy
contains the above copyright notice and this license. These can be
included either as stand-alone text files, human-readable headers or
in the appropriate machine-readable metadata fields within text or
binary files as long as those fields can be easily viewed by the user.

3) No Modified Version of the Font Software may use the Reserved Font
Name(s) unless explicit written permission is granted by the corresponding
Copyright Holder. This restriction only applies to the primary font name as
presented to the users.

4) The name(s) of the Copyright Holder(s) or the Author(s) of the Font
Software shall not be used to promote, endorse or advertise any
Modified Version, except to acknowledge the contribution(s) of the
Copyright Holder(s) and the Author(s) or with their explicit written
permission.

5) The Font Software, modified or unmodified, in part or in whole,
must be distributed entirely under this license, and must not be
distributed under any other license. The requirement for fonts to
remain under this license does not apply to any document created
using the Font Software.

TERMINATION
This license becomes null and void if any of the above conditions are
not met.

DISCLAIMER
THE FONT SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO ANY WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT
OF COPYRIGHT, PATENT, TRADEMARK, OR OTHER RIGHT. IN NO EVENT SHALL THE
COPYRIGHT HOLDER BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY,
INCLUDING ANY GENERAL, SPECIAL, INDIRECT, INCIDENTAL, OR CONSEQUENTIAL
DAMAGES, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING
FROM, OUT OF THE USE OR INABILITY TO USE THE FONT SOFTWARE OR FROM
OTHER DEALINGS IN THE FONT SOFTWARE.
```
