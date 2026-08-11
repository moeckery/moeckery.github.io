# moeckery.github.io

A hub for the services run under the moeckery name. Jekyll, built and deployed
by GitHub Pages on push to `main` — there's no build workflow to maintain.

## Adding a service

Create one file in `_services/`. That's the whole job — the homepage and
`/services/` find it, sort it, and render a card for it automatically.

```markdown
---
title: Example
status: live          # live | beta | soon | retired
tagline: One line, shown on the card.
link: https://example.com    # or a local path like /example/
domain: example.com          # optional, shown under the name
repo: https://github.com/moeckery/example
launched: 2026
---
```

Services are **data, not pages** — the collection is `output: false`, so a card
links straight at the service itself. There's no `/services/<name>/`
description page sitting in front of the real thing. A service hosted on this
site gets a short top-level path of its own: `/boilerplater/`, not
`/services/boilerplater/`.

Leave `link` out entirely and the card renders as plain text instead of a dead
link — the right behaviour for something announced but not yet reachable.

### Status values

Defined in `_config.yml` under `statuses`, and that list is also the sort
order — `live` services appear above `beta`, `beta` above `soon`, and so on.
Changing a label or adding a status is an edit to that one list. A service
declaring a status that isn't in the list still renders, grouped under
"Other", so a typo shows up instead of silently dropping the service.

## Hosting a service on this site

Drop it in its own top-level directory — `boilerplater/index.html` serves at
`/boilerplater/`. Then point the service's `link` at that path.

**Self-contained apps must not have YAML front matter.** Without it Jekyll
treats the file as static and copies it verbatim; with it, Jekyll runs the file
through Liquid and any `{{ ... }}` in the app's own templating gets eaten.
Boilerplater is a Vue app with 74 such interpolations, which is exactly why
`boilerplater/index.html` starts straight at `<!DOCTYPE html>`.

## Layout

```
_config.yml          site settings + the status vocabulary
_services/           one file per service — the source of truth
_layouts/default.html the page shell
_includes/           head, header, footer, service-card, status
assets/css/main.scss all styling; light and dark via CSS custom properties
index.html           landing page — hero + every service
services/index.html  full listing, grouped by status
boilerplater/        the Boilerplater app, served verbatim at /boilerplater/
404.html
```

## Running it locally

```bash
bundle install
bundle exec jekyll serve   # http://localhost:4000
```

## Domains

The site itself is served at `moeckery.github.io`. If a service gets its own
domain, that domain points at wherever the service is hosted — **not** at this
repo. GitHub Pages allows exactly one custom domain per repository, so a
`CNAME` file here would move this whole hub onto that domain rather than
mapping it to a single service. A service needing its own domain needs its own
repo (or its own host).

## License

MIT. See [LICENSE](LICENSE).
