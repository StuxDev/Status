# Changelog

All notable changes to Stux.Dev's status page (status.stux.dev) are documented here. It
follows [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## v1.0.0

### Added

- status.stux.dev, a GitHup status page for Stux.Dev, checked every 5 minutes: the Stux.Dev website and media CDN, a **Services** group (Stuxs.Tools, Downl.one, Sm.lol) and a **Labs** group (Stux.Dev Labs, AutoScroll), each group with a combined status
- `.github/workflows/status.yml`: a GitHup `check` every 5 minutes with incident Issues, then a build into `_site`, deployed with `actions/deploy-pages` when a status changes, hourly and on pushes; it also keeps the README's status table up to date
- The **Boring Legal Stuff** hub at `/legal/` with Privacy Policy, Terms and Ethics, Cookies Policy, Imprint, Disclaimer and Opt-Out Preferences, and a `404.html`, in Stux.Dev orange (`#fd6602`, with darker shades where text needs the contrast) and in light and dark themes
- A **Changelogs** page at `/changelogs/` with tabs for this status page and for GitHup, sorted into the fixed section order with coloured type badges; `/changelog/` redirects there, and every footer starts with this repo's version, linking to it
- A live status badge and status table in the README, read from `data/summary.json`
- `dev-server.sh`/`dev-server.bat`, which build the page from generated example data into `.dev/public` and serve it locally with `DEV_MODE` on by default (`--no-dev-mode` to opt out)
- `commit.sh`/`commit.bat` release scripts that read `VERSION.md` and tag `vX.Y.Z`
