# SudoEarth — Public Legal Site

Static HTML hosted at https://sudoearth.app/{privacy,terms} for the
SudoEarth iOS app's required legal pages.

This repo is **public + tiny** so it can be served by free static hosts
(Vercel / Cloudflare Pages) without exposing the main SudoEarth-app
repo, which contains server logic, IAP / RevenueCat config, and
prompt templates that are intentionally private.

## Source of truth

The Markdown source lives in the private `SudoEarth-app` repo at
`docs/legal/{privacy,terms}.md`. The HTML in this repo is generated
by `tools/build-legal-site.py` over there. To update:

1. In the private repo, edit `docs/legal/{privacy,terms}.md`.
2. Re-run `python3 tools/build-legal-site.py` — outputs land in `site/`.
3. Copy the new `site/*` files here and push.

## Why two repos

The app's main repo is private. GitHub Pages on a private repo
needs a paid GitHub Pro plan; Vercel / Cloudflare Pages can serve
either, but pulling from a private repo via OAuth couples the
public site to the private repo's history. Splitting cleanly is
cheaper and reduces the blast radius of any future "oops, what
secret did I just push" incident.
