<p align="center">
  <picture><source media="(prefers-color-scheme: dark)" srcset="https://global.media.stux.dev/logo-light.png"><source media="(prefers-color-scheme: light)" srcset="https://global.media.stux.dev/logo-dark.png"><img src="https://global.media.stux.dev/logo-dark.png" height="80" alt="Stux.Dev Logo"></picture>
</p>

# Contributing to Status

Status is Stux.Dev's status page, [status.stux.dev](https://status.stux.dev), built with
GitHup, [a Stux.Group Service](https://services.stux.group). To report an outage, open an
Issue. Bugs or ideas for the status page software belong in
[StuxGroup/GitHup](https://github.com/StuxGroup/GitHup/issues).

## Local setup

You need Python 3.11+ and nothing else.

```bash
./dev-server.sh [--no-dev-mode] [port]   # or dev-server.bat on Windows
```

## Project conventions

- **Monitors live in `.githup.yml`.** Its syntax is documented in the
  [GitHup docs](https://githup.stux.group/docs/). Only add services Stux.Dev runs.
- **The status page itself is GitHup's.** Change how it looks or works in GitHup, not here.
  `site/` only holds the `/legal` pages, `/changelogs` and `404.html`, which share
  `site/assets/pages.css` and `pages.js`. Their header and footer are repeated in every page;
  change them all together.
- **Brand.** The Stux.Dev orange is `#fd6602` (the logo's colour). On light backgrounds links and
  buttons use the darker `#be4c02` so text stays readable; both are tokens in `pages.css`.
- **Legal pages.** Every page's footer links to **Boring Legal Stuff** at `/legal/`, which links
  to Privacy Policy, Terms and Ethics, Cookies Policy, Imprint, Disclaimer and Opt-Out
  Preferences. Keep them accurate.
- **Don't edit `data/` by hand.** It belongs to GitHup and the workflow.

## Versioning

This project uses [Date Versioning](https://datevers.ing). To release:

1. Add a `## vYY.MM.DD` entry at the top of `CHANGELOG.md`, with its sections in this order: Added, Changed, Fixed, Removed, Security, Deprecated.
2. Set `VERSION.md` to the same bare version (no `v`): today's **UTC** date as `YY.MM.DD`, or `YY.MM.DD-1`, `-2`… for later releases the same UTC day. Never a future date. Use UTC, not local time: just after midnight in the UK it is still the previous day in UTC.
3. Run `bash tests/version.sh`.
4. Run `./commit.sh` (or `commit.bat` on Windows). It checks the version, commits and tags `vYY.MM.DD`, and never pushes.
