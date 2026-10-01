# Changelog

All notable changes to Stux.Dev's status page (status.stux.dev) are documented here. It
follows [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## v1.2.0

### Added

- A `legal:` block in `.githup.yml` (operator, company, contact, host, effective date): GitHup generates the **Boring Legal Stuff** hub at `/legal/` and its six sub-pages, a themed 404 page, `sitemap.xml`, `robots.txt` and `/sitemap/`, all in the status page's own template (needs GitHup v1.6.0, picked up through `StuxGroup/GitHup@v1`)
- The sitemap's base URL comes from `site.url: https://status.stux.dev/`

### Changed

- The status page comes entirely from GitHup's template, with one version and one changelog: the footer shows only **Powered by GitHup vX.Y.Z**, linking to GitHup's changelog
- `dev-server.sh`/`.bat` and the workflow no longer copy `site/`, `CHANGELOG.md` or `VERSION.md` into the page; the dev server still builds with the local GitHup checkout, so the new pages show locally

### Removed

- The hand-made `site/` folder: the legal hub and sub-pages, the `/changelogs/` page (and `/changelog/` redirect), the 404 page and their shared assets. This repo keeps its own `CHANGELOG.md`, `VERSION.md` and tags
- `site.changelog` (and `site.legal`) from `.githup.yml`; `site.changelog` is deprecated in GitHup v1.6.0

## v1.1.0

### Added

- A **Created with** line in the footer of the hand-made pages (`/legal/`, `/changelogs/`, the 404 page): a heart, code brackets and a coffee mug, by Stux.Dev

### Changed

- The dev-mode banner on the hand-made pages is the shared Stux site banner: a muted strip in the page's colours with a label chip and a faint icon pattern, replacing the yellow hazard stripes. It stays at the top and pushes the page down by its exact height, so it never covers anything, including on phones. In dev mode, `?banner=soon,maintenance,site` previews the other banner styles
- The dev banner is switched on by `dev-server.sh`/`.bat` (they write `assets/dev-mode.js` into the local build) instead of by looking at the hostname, so `--no-dev-mode` now hides it everywhere; the old `?nodev=1` is gone
- The footer's **Powered by GitHup** and service links are muted until hovered or focused, and footer logos are 28px and fade in without the hover glitch (the same filter functions in every state)
- `dev-server.sh`/`.bat` use a local GitHup checkout (`../GitHup` or `../../Stux.Group/GitHup`) when there is one, so local previews show the newest GitHup
- Needs GitHup v1.5.0 for the status page's own new banner and muted footer (it's picked up through `StuxGroup/GitHup@v1`)

## v1.0.0

### Added

- status.stux.dev, a GitHup status page for Stux.Dev, checked every 5 minutes: the Stux.Dev website and media CDN, a **Services** group (Stuxs.Tools, Downl.one, Sm.lol) and a **Labs** group (Stux.Dev Labs, AutoScroll), each group with a combined status
- `.github/workflows/status.yml`: a GitHup `check` every 5 minutes with incident Issues, then a build into `_site`, deployed with `actions/deploy-pages` when a status changes, hourly and on pushes; it also keeps the README's status table up to date
- The **Boring Legal Stuff** hub at `/legal/` with Privacy Policy, Terms and Ethics, Cookies Policy, Imprint, Disclaimer and Opt-Out Preferences, and a `404.html`, in Stux.Dev orange (`#fd6602`, with darker shades where text needs the contrast) and in light and dark themes
- A **Changelogs** page at `/changelogs/` with tabs for this status page and for GitHup, sorted into the fixed section order with coloured type badges; `/changelog/` redirects there, and every footer starts with this repo's version, linking to it
- A live status badge and status table in the README, read from `data/summary.json`
- `dev-server.sh`/`dev-server.bat`, which build the page from generated example data into `.dev/public` and serve it locally with `DEV_MODE` on by default (`--no-dev-mode` to opt out)
- `commit.sh`/`commit.bat` release scripts that read `VERSION.md` and tag `vX.Y.Z`
