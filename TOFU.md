# Flexbox Froggy on Tofu

Flexbox Froggy is Thomas Park's game for learning CSS flexbox. Players write CSS to guide frogs onto their matching lilypads across 24 levels, with the original translations, difficulty settings, and colorblind mode. This copy retains the upstream name, artwork, favicon, and author credits.

## Running it

- **Tofu framework preset:** `static`.
- **Site root / output directory:** repository root (`.`), with `index.html` as the entry page.
- **Build command:** none. The repository is the finished static site.
- **Dependency verification:** `npm ci --no-audit --no-fund`, using the upstream `package-lock.json`.
- **Environment variables / secrets:** none.
- **Database / server / sign-in:** none.
- **Saved progress:** browser `localStorage`, local to the site's origin and browser. It does not sync between devices; clearing browser data removes it.
- **Local server:** `python3 -I -m http.server 43873 --bind 127.0.0.1 --directory /absolute/path/to/flexboxfroggy`.

All runtime scripts, styles, fonts, and images are included. No install is needed when serving the published files. `node_modules/` may be omitted by the hosting importer: the page uses checked-in copies under `vendor/` instead. The upstream package manifests, lockfile, and tracked dependency tree remain available for upstream maintenance.

## Adaptations and why

- Removed Google Analytics, Google AdSense, the advertising account metadata, and `ads.txt`, so a copy neither tracks visitors nor serves the upstream advertising account.
- Removed the upstream `CNAME` and original-site social URL/account metadata. Social images refer to this copy's local screenshot.
- Copied the exact locked jQuery 3.5.1 and Animate.css 3.4.0 runtime files into `vendor/`, with license notices, because hosting uploaders exclude `node_modules/`.
- Replaced the Google Fonts request with local copies of the same families: PT Sans, Fredoka One, and Source Code Pro. Fonts are unmodified WOFF2 files from `@fontsource/pt-sans@5.3.0`, `@fontsource/fredoka-one@5.3.0`, and `@fontsource/source-code-pro@5.3.1`, including all supplied normal-400 language subsets and their licenses. The CSS retains the font families and Unicode coverage.
- Removed unused Twitter widget initialization from the language-change handler, so it cannot initialize a third-party embed.
- Ignored npm's generated `node_modules/.package-lock.json` to keep verification from adding an installation artifact.

The original creator links and related-game links remain as ordinary links. They leave the app only when clicked. Core game logic, lesson content, translations, artwork, and the original `LICENSE` and `README.md` are unchanged. Some existing Chinese interface labels remain English, as in upstream.

## Verification

Verified locally on 2026-10-23, without deploying:

```sh
npm --prefix /private/tmp/gallery-batch2/flexboxfroggy ci --no-audit --no-fund
python3 -I -m http.server 43873 --bind 127.0.0.1 --directory /private/tmp/gallery-batch2/flexboxfroggy
curl --fail --silent --show-error --output /private/tmp/gallery-batch2/flexboxfroggy/.git/tofu-verification/entry.html --write-out 'HTTP %{http_code}\n' http://127.0.0.1:43873/
```

The install succeeded (2 packages; npm's old-lockfile metadata notice only), and the entry page returned HTTP 200. A local HTML/CSS asset check confirmed all 36 referenced scripts, styles, images, and font subsets returned HTTP 200 and none required `node_modules/` or a remote host.

An Aside browser check through the gstack `/browse` skill verified all 24 level menu entries, solving levels 1 and 2, advancing with Next, restoring level 2 and its answer after navigation, switching to Simplified Chinese, and enabling colorblind mode. Browser console errors: `[]`. External runtime resource requests: `[]`. This is a smoke check, not proof that every lesson, language, or browser has been tested.

## Source and licenses

- **Upstream:** https://github.com/thomaspark/flexboxfroggy
- **Upstream branch:** `main`
- **Upstream commit:** `9a6feab850a56cbe9ad90f3afcc95e88335bbec8`
- **Gallery fork:** https://github.com/tofu-gallery/flexboxfroggy
- **Adaptation branch:** `tofu`; `main` mirrors upstream without adaptation commits.
- **Pin tag:** `pin/2026-10-23`, created only after local verification.
- **Application code:** MIT, copyright Thomas Park; see the unchanged root `LICENSE` and `README.md`.
- **Images:** Creative Commons Attribution 3.0, as stated in the upstream `README.md`: https://creativecommons.org/licenses/by/3.0/legalcode.txt. Artwork is unchanged; keep the author attribution when redistributing.
- **jQuery:** MIT; see `vendor/jquery/LICENSE.txt` and its original file header.
- **Animate.css:** MIT, copyright Daniel Eden; see `vendor/animate.css/LICENSE` and its original file header.
- **Fonts:** SIL Open Font License 1.1; see each `vendor/fonts/<family>/LICENSE`. Keep those notices with redistributed fonts.
