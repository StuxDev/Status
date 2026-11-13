# Changelog

All notable changes to Stux.Dev Status (status.stux.dev) are documented here. Each release's sections come in this
order: Added, Changed, Fixed, Removed, Security, Deprecated.

Since v26.10.23 this project uses [Date Versioning](https://datevers.ing) (`YY.MM.DD`, the UTC release date, with `-1`, `-2`… for later releases the same day); earlier releases used Semantic Versioning.

## v26.11.13

### Changed

- The status page's Imprint (`legal.company` in `.githup.yml`) gives Stux Group Ltd's new registered office, 124 City Road, London, EC1V 2NX, England, United Kingdom, instead of 82a James Carter Road, Mildenhall, England, IP28 7DE. The company number (13160574) and "registered in England and Wales" are unchanged.

## v26.11.08

### Changed

- The site description says the services are "checked regularly" instead of "checked every 5 minutes". GitHub runs the 5-minute schedule best-effort and often far less often, so the copy no longer promises 5 minutes; the status page shows the real check rhythm. The `.githup.yml` comment, the README and CONTRIBUTING say the same.

## v26.11.06-2

### Added

- Monitors for every live Stux.Dev site that wasn't checked yet: **Stux.Dev Services** (services.stux.dev), and a new **Templates** group with Stux.Dev Soonpage, Maintenancepage, Servicepage and GitHub Pages Redirect. The README's list matches.
- A `test` branch. Work happens on `test`, and changes reach `main` only through a pull request from `test`, which needs CI to pass and is reviewed and merged by Leo; release commits and tags are made on `test` and go live when it's merged. CONTRIBUTING has a Branches section, its release steps end by pushing `test` and opening that pull request, and the README's Versioning section says so.
- `.github/workflows/ci.yml`, which runs `tests/version.sh` on pushes to `main` and `test` and on pull requests.

## v26.11.06-1

### Changed

- CONTRIBUTING calls the page by its full name, Stux.Dev Status, and no longer describes a `site/` folder of hand-made
  legal pages sharing `pages.css`: GitHup generates the legal pages, 404 and sitemap from `.githup.yml`, and the brand
  colour is its `site.accent`.
- This changelog's intro no longer says the project follows Semantic Versioning; it moved to Date Versioning at v26.10.23.

## v26.11.06

### Changed

- The page's logo and favicon are now its own badge icon, Stux.Dev Status (the Stux.Dev mark with a heartbeat badge),
  served from services.stux.dev, instead of the plain Stux.Dev icon. The README's header shows the same icon and the
  full name, Stux.Dev Status, as do the commit and dev-server scripts.

## v26.10.23

### Added

- `tests/version.sh`, which checks that `VERSION.md` is a valid Date Version, a real calendar date not in the future, and the same as the newest entry in this changelog

### Changed

- Switched from Semantic Versioning to [Date Versioning](https://datevers.ing): releases are numbered by their UTC release date as `YY.MM.DD`, with `-1`, `-2`… for later releases the same day. This release follows v1.2.10
- `commit.sh` and `commit.bat` refuse a `VERSION.md` that isn't a valid Date Version or is dated in the future (UTC), and warn when it's dated before today
- `README.md` and `CONTRIBUTING.md` describe Date Versioning and the release steps

## v1.2.10

### Changed

- The logos and icons in the Markdown docs (README and the like) follow GitHub's light or dark theme, using each brand's `logo-light`/`logo-dark` and `icon-light`/`icon-dark` files

## v1.2.9

### Changed

- The logos and icons in the Markdown docs (README and the like) follow GitHub's light or dark theme, using each brand's `logo-light`/`logo-dark` and `icon-light`/`icon-dark` files

## v1.2.8

### Changed

- The tiny1 certificate check uses the server's new `stuxedo.net` name (`tiny1.servers.uk.stuxedo.net`) instead of `stux.cloud`; its name, slug and history are unchanged

## v1.2.7

### Changed

- The Downl.one monitor checks the app's health endpoint (`/api/health.php`, which fails when yt-dlp, storage or PHP break) instead of the home page; Downl.one now runs on down1

## v1.2.6

### Added

- A "Sm.lol Certificates" monitor: tiny1, Sm.lol's server, checks daily that every certificate it uses (Let's Encrypt and Sm.lol's Cloudflare Origin Certificate) has more than 21 days left and publishes `certificates-ok.txt` while they do, so an expiring certificate shows as down and opens an incident Issue

## v1.2.5

### Changed

- `max_response_time` raised to 15 seconds (GitHup's new default), so a slow but working site is no longer shown as degraded

## v1.2.4

### Fixed

- A double blank line in `CHANGELOG.md`, and the README status table's empty Group cells (regenerated with GitHup v1.8.1), so the Markdown files pass markdownlint

## v1.2.3

### Changed

- Opted in to GitHup v1.8.0's `fill-gaps` option (`repeat: 4`, `repeat-interval: 300`): when GitHub runs the 5-minute schedule late, a run now checks up to 4 times, 5 minutes apart, instead of once. A run that is on time still checks once. GitHub often runs the 5-minute schedule only every few hours. The check job's timeout is now 25 minutes

## v1.2.2

### Removed

- The copyright line in the status page footer: `site.copyright` is no longer set, as status pages don't need one

## v1.2.1

### Added

- A copyright line in the footer (Copyright © START–CURRENT HOLDER), from the new `site.copyright` setting in `.githup.yml`; it needs GitHup 1.7.0 or later

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
