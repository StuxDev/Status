<p align="center">
  <picture><source media="(prefers-color-scheme: dark)" srcset="https://global.media.stux.dev/logo-light.png"><source media="(prefers-color-scheme: light)" srcset="https://global.media.stux.dev/logo-dark.png"><img src="https://global.media.stux.dev/logo-dark.png" height="80" alt="Stux.Dev Logo"></picture>
</p>

# Contributing to Stux.Dev Status

Stux.Dev Status is Stux.Dev's status page, [status.stux.dev](https://status.stux.dev), built with
GitHup, [a Stux.Group Service](https://services.stux.group). To report an outage, open an
Issue. Bugs or ideas for the status page software belong in
[StuxGroup/GitHup](https://github.com/StuxGroup/GitHup/issues).

## Local setup

You need Python 3.11+ and nothing else.

```bash
./dev-server.sh [--no-dev-mode] [--lan] [port]   # or dev-server.bat on Windows
```

## Project conventions

- **Monitors live in `.githup.yml`.** Its syntax is documented in the
  [GitHup docs](https://githup.stux.group/docs/). Only add services Stux.Dev runs.
- **The whole site is GitHup's.** Change how it looks or works in GitHup, not here. The status
  page, the legal pages, `404.html` and the sitemap are all generated from `.githup.yml`; nothing
  in this repo is hand-made HTML.
- **Brand.** The Stux.Dev orange, `#fd6602` (the logo's colour), is `site.accent` in `.githup.yml`.
  The logo and favicon are the Stux.Dev Status badge icon, served from services.stux.dev.
- **Legal pages.** GitHup builds the **Boring Legal Stuff** hub at `/legal/` (Privacy Policy, Terms
  and Ethics, Cookies Policy, Imprint, Disclaimer and Opt-Out Preferences) from the `legal:`
  section of `.githup.yml`. Keep those details accurate.
- **Don't edit `data/` by hand.** It belongs to GitHup and the workflow.

## Branches and going live

- **`main` is what's live.** Nothing is pushed to it directly: it only changes when a pull request from `staging` is merged. Merging into `main` puts a `.githup.yml` change live; the GitHup workflow only runs on `main`.
- **`staging` is the last check before live.** It only changes when a pull request from `test` is merged. CI runs on it, and nothing deploys from it.
- **Work happens on `test`**, or on a feature branch off `test` that's merged back into it. Releases are made on `test` too; `commit.sh` / `commit.bat` refuse to run on `staging` or `main`.
- **Going live:** push `test` with its tag (`git push origin test --tags`), open a pull request into staging (`gh pr create --base staging --head test`), check staging once it's merged, then open one from staging into main (`gh pr create --base main --head staging`). Both need CI to pass and are reviewed and merged by Leo.
- GitHup's workflow commits monitoring data straight to `main` (the one exception to the rule above), so merge `origin/main` into `test` before you start; `staging` picks it up through the next pull request.

## Versioning

This project uses [Date Versioning](https://datevers.ing). To release:

1. Add a `## vYY.MM.DD` entry at the top of `CHANGELOG.md`, with its sections in this order: Added, Changed, Fixed, Removed, Security, Deprecated.
2. Set `VERSION.md` to the same bare version (no `v`): today's **UTC** date as `YY.MM.DD`, or `YY.MM.DD-1`, `-2`… for later releases the same UTC day. Never a future date. Use UTC, not local time: just after midnight in the UK it is still the previous day in UTC.
3. Run `bash tests/version.sh`.
4. Run `./commit.sh` (or `commit.bat` on Windows). It checks the version, commits and tags `vYY.MM.DD`, and never pushes.
5. Push `test` with its tags (`git push origin test --tags`) and open a pull request into staging (`gh pr create --base staging --head test`). Once it's merged and staging is checked, open one from staging into main (`gh pr create --base main --head staging`).
