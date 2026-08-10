# moeckery.github.io

A hub for the services run under the moeckery name. Jekyll, built and deployed
by GitHub Pages on push to `main` — there's no build workflow to maintain.

## Adding a service

Create one file in `_services/`. That's the whole job — the homepage and
`/services/` find it, sort it, and render a card for it automatically.

```markdown
---
title: example
domain: example.com
status: live          # live | beta | soon | retired
tagline: One line, shown on the card.
link: https://example.com    # omit while the service isn't serving yet
repo: https://github.com/moeckery/example
launched: 2026
---

Body copy for the service's own page at /services/example/.
```

The filename becomes the URL: `_services/moldbin.md` → `/services/moldbin/`.

### Status values

Defined in `_config.yml` under `statuses`, and that list is also the sort
order — `live` services appear above `beta`, `beta` above `soon`, and so on.
Changing a label or adding a status is an edit to that one list. A service
declaring a status that isn't in the list still renders, grouped under
"Other", so a typo shows up instead of silently dropping the service.

## Layout

```
_config.yml          site settings + the status vocabulary
_services/           one file per service — the source of truth
_layouts/            default (shell), service (a service's page)
_includes/           head, header, footer, service-card, status
assets/css/main.scss all styling; light and dark via CSS custom properties
index.html           landing page — hero + every service
services/index.html  full listing, grouped by status
404.html
```

## Running it locally

```bash
bundle install
bundle exec jekyll serve   # http://localhost:4000
```

## Domains

The site itself is served at `moeckery.github.io`. Service domains such as
`moldbin.com` point at wherever that service is hosted — they are not aliases
of this repo, so don't add a `CNAME` file for them here. A `CNAME` in this
repo would move this hub onto that domain, which isn't the intent.
