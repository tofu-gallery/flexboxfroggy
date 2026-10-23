# Flexbox Froggy on Tofu

Flexbox Froggy is Thomas Park's game for learning CSS flexbox. Players write CSS to guide frogs onto their matching lilypads across 24 levels, with the original translations, difficulty settings, and colorblind mode. This copy retains the upstream name, artwork, favicon, and author credits.

## Running it

- **Tofu framework preset:** `static`.
- **Site root / output directory:** repository root (`.`), with `index.html` as the entry page.
- **Build command:** none. The repository is the finished static site.
- **How upstream builds and tests it:** it does not. The repository is the site, published as it is by GitHub Pages (hence the Jekyll `_config.yml`, `.nojekyll` and `CNAME` files upstream carries), with no build step, no test suite and no CI configuration. Upstream's `package.json` has no scripts: it and `package-lock.json` only named the two runtime libraries, jQuery 3.5.1 and Animate.css 3.4.0, which upstream committed under `node_modules/` so the page could load them from there. To try a change, serve the folder with any static file server and open `index.html`; nothing needs installing.
- **Environment variables / secrets:** none.
- **Database / server / sign-in:** none.
- **Saved progress:** browser `localStorage`, local to the site's origin and browser. It does not sync between devices; clearing browser data removes it.
- **Local server:** `python3 -I -m http.server 43873 --bind 127.0.0.1 --directory /absolute/path/to/flexboxfroggy`.

All runtime scripts, styles, fonts, and images are included. No install is needed when serving the published files. Upstream's committed `node_modules/` copy of the two libraries is still in the repository, but nothing loads it and the hosting importer leaves it out: the page uses the copies under `vendor/` instead.

## Adaptations and why

- Removed Google Analytics, Google AdSense, the advertising account metadata, and `ads.txt`, so a copy neither tracks visitors nor serves the upstream advertising account.
- Removed the upstream `CNAME` and original-site social URL/account metadata. Social images refer to this copy's local screenshot.
- Removed `_config.yml`, `package.json` and `package-lock.json`. Static hosting does not serve a Jekyll settings file and reads a root `package.json` or `package-lock.json` as build configuration, and this site has no build: the page already loads jQuery and Animate.css from `vendor/`, and nothing at runtime read those three files. The `.gitignore` line for npm's `node_modules/.package-lock.json` went with them, since there is no npm install left to check. The three files are unchanged on `main` and in the earlier tag `pin/2026-10-23`.
- Copied the exact jQuery 3.5.1 and Animate.css 3.4.0 runtime files that upstream's lockfile pinned into `vendor/`, with license notices, because hosting uploaders exclude `node_modules/`.
- Replaced the Google Fonts request with local copies of the same families: PT Sans, Fredoka One, and Source Code Pro. Fonts are unmodified WOFF2 files from `@fontsource/pt-sans@5.3.0`, `@fontsource/fredoka-one@5.3.0`, and `@fontsource/source-code-pro@5.3.1`, including all supplied normal-400 language subsets and their licenses. The CSS retains the font families and Unicode coverage.
- Removed unused Twitter widget initialization from the language-change handler, so it cannot initialize a third-party embed.

The original creator links and related-game links remain as ordinary links. They leave the app only when clicked. Core game logic, lesson content, translations, artwork, and the original `LICENSE` and `README.md` are unchanged. Some existing Chinese interface labels remain English, as in upstream.

## Verification

Re-verified locally on 2026-10-23 after removing the three files, without deploying. The first pin (`pin/2026-10-23`) was verified with `npm ci` against the lockfile; that step is gone with the lockfile.

```sh
rsync -a --exclude node_modules --exclude dist --exclude build --exclude target --exclude .cache --exclude .git /absolute/path/to/flexboxfroggy/ /absolute/path/to/flexboxfroggy-imported/
python3 -I -m http.server 47513 --bind 127.0.0.1 --directory /absolute/path/to/flexboxfroggy-imported
```

The copy holds what the GitHub import keeps: 49 files, because the import leaves out `node_modules/`. Tofu's static-site check on an archive of this branch reads it as a finished site, with no file refused and no safety findings. The entry page and the 20 files it loads (scripts, styles, images, the Latin font file of each family, and the favicon) all returned HTTP 200 from that copy, and none was missing or came from another host.

An Aside browser check through the gstack `/browse` skill, against that local server, loaded the page ("Level 1 of 24" with 24 level-menu entries), solved level 1 with `justify-content: flex-end;`, advanced with Next, solved level 2 with `justify-content: center;`, reloaded the page and found level 2, its answer and both solved marks restored, and switched the interface to Japanese. Browser console errors: `[]`. The app made no request to another host. This is a smoke check, not proof that every lesson, language, or browser has been tested.

## Source and licenses

- **Upstream:** https://github.com/thomaspark/flexboxfroggy
- **Upstream branch:** `main`
- **Upstream commit:** `9a6feab850a56cbe9ad90f3afcc95e88335bbec8`
- **Gallery fork:** https://github.com/tofu-gallery/flexboxfroggy
- **Adaptation branch:** `tofu`; `main` mirrors upstream without adaptation commits.
- **Pin tag:** `pin/2026-10-23.1`, created only after the verification above. It replaces `pin/2026-10-23`, which stays where it was and still carries the Jekyll and npm files.
- **Application code:** MIT, copyright Thomas Park; see the unchanged root `LICENSE` and `README.md`.
- **Images:** Creative Commons Attribution 3.0, as stated in the upstream `README.md`: https://creativecommons.org/licenses/by/3.0/legalcode.txt. Artwork is unchanged; keep the author attribution when redistributing.
- **jQuery:** MIT; see `vendor/jquery/LICENSE.txt` and its original file header.
- **Animate.css:** MIT, copyright Daniel Eden; see `vendor/animate.css/LICENSE` and its original file header.
- **Fonts:** SIL Open Font License 1.1; see each `vendor/fonts/<family>/LICENSE`. Keep those notices with redistributed fonts.
