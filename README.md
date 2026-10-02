# qsvt.com

Static archive of the **Queen's University Solar Vehicle Team (QSVT)** site. Plain
static HTML/CSS, no build step, no framework, no JS dependencies — deployed via
the Cloudflare Pages app's direct Git integration (no GitHub Actions, no manually
managed API tokens).

## Why this exists

The original site ran WordPress on a VPS. The content hasn't changed in years, so
there's no reason to keep paying for and patching a dynamic CMS for a page that's
effectively a historical record. This repo is a straight content/photo migration:
same pages, same photos, same information architecture, new static theme that
echoes the original's black header / gold (`#cc9900`) accent look.

All copy and images were pulled directly from the live `qsvt.com` WordPress site
(cross-checked against the Wayback Machine) on 2026-10-01.

## Structure

```
index.html                 Home
about.html                 About the Team
rayces.html                Rayces (race history)
vehicles.html               Vehicle List (grid + results table)
vehicles/*.html              One page per vehicle (Photomoto, SunQuest, ... Aurum)
assets/css/style.css         All site styling (single file, CSS custom properties)
assets/images/               All photos/logos, fetched at original resolution
404.html, robots.txt, sitemap.xml
```

To change copy: edit the relevant `.html` file directly. No templating/build step —
same rationale as `jonmash.com`: a handful of static pages doesn't need one.

## Deploy

Deployed through the **Cloudflare dashboard/app's Git integration** — connect
this repo as a Pages project and it builds and deploys automatically on every
push to `main`. No build command needed (static output directory: `/`, repo
root). No GitHub Actions workflow, no manually created API tokens.

**One-time setup still needed (not done by this repo):**

1. In the Cloudflare app/dashboard: Pages → Create project → Connect to Git →
   select `jonmash/qsvt.com`. Build output directory: `/` (root), no build
   command.
2. Once the first deploy succeeds, add the `qsvt.com` (and `www.qsvt.com` if
   used) custom domain to the Pages project.
3. Point DNS at Cloudflare Pages (update `octodns-config` — do not hand-edit
   DNS) and only then cancel the WordPress VPS.

## What was NOT migrated

- WordPress admin, comments, RSS feeds, search — none of that was in use.
- A handful of decorative/duplicate images referenced only via WordPress's
  auto-generated responsive `srcset` sizes (e.g. intermediate crop variants) were
  skipped where a usable full-size or thumbnail version already covers it; nothing
  user-visible on the original pages is missing.
- The original's sidebar widgets (QSVT @ Wikipedia link, Queen's University logo)
  are preserved as plain links in the footer instead of a literal sidebar.
