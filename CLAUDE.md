# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Single-page marketing site for **Jollof & Jerk** — a West African / Caribbean restaurant at 2020 9th St NW, Washington DC. Owner & Chef: Mamadou Bah. Deployed on Vercel as a static site under team `team_nt4pW0uOQZNNe7TR9CF7PLwl` (project name `jollof-and-jerk`).

The upstairs tenant **Rendezvous Lounge** (`@rendezvous_lounge_`) has its own dedicated section here but is also a separate codebase + Vercel project — see "Sibling project" below.

## Architecture

There is no framework, build step, package manager, or test runner. The entire site is one self-contained file plus images:

- `index.html` — ~990 lines containing all markup, CSS (in a single `<style>` block), and JS (in a single `<script>` block at the bottom). All edits happen here.
- `assets/food/` and `assets/media/` — JPGs and GIFs referenced by relative path from `index.html`. Cached `immutable` for 1 year via `vercel.json` headers.
- `vercel.json` — static build config (`@vercel/static`) plus the asset cache-control header.

### Sections in `index.html` (anchor IDs, in document order)

`#hero` → `#flash` → `#location` → `#menu` → `#order` → `#catering` → `#story` → `#rendezvous` → `#alerts` → `#social`. The fixed nav and mobile nav link to these IDs; the cart button (`#cartBtn`) calls `scrollToOrder()`.

### Inline JS conventions (bottom of `index.html`)

- **Menu data** lives in the `menu` object (`{mains:[...], sides:[...]}`). Each item has `name`, `desc`, `origin` (nullable), `price`, `tag` (nullable, e.g. `"Signature"`, `"Premium"`), and — for mains — `sides:true` to render the "+ 2 sides" hint. `renderMenu(cat)` rebuilds `#menuList` from this object; tabs (`.tab[data-cat]`) drive category switching. To add/edit menu items, edit this object — there is no CMS.
- **Open/Closed status** is computed client-side in `getStatus()` from the user's local time. Kitchen opens at 14:00; closes at 03:00 Sun–Thu and 04:00 Fri & Sat. `updateStatus()` paints two badges (`#heroBadge`, `#statusBadge`) plus `#todayHours`. If hours change, update `getStatus()`, `updateStatus()`, **and** the static `.hr-row` markup in the `#location` section — they are not derived from a single source.
- **Flash-deal countdown** (`updateTimer`, 1s interval) counts down to local midnight.
- **Forms** (`submitOrder`, `submitCatering`, `submitSMS`) are stubs — they swap button text on click and do not POST anywhere. There is no backend yet.
- **Cart** is a counter only (`cartCount`); `addToCart` just increments and flashes the button. No items, no checkout.

## Common tasks

```bash
# Local preview — no build, just open the file
open index.html

# Deploy to the Rich Off Tech Vercel team
vercel --team team_nt4pW0uOQZNNe7TR9CF7PLwl --name jollof-and-jerk           # preview
vercel --team team_nt4pW0uOQZNNe7TR9CF7PLwl --name jollof-and-jerk --prod    # production
```

CLI is registered to `richofftechllc@gmail.com`. `DEPLOY.md` documents the dashboard and GitHub-integration paths as alternatives.

## Sibling project: Rendezvous Lounge

The upstairs business has its own static site, repo, and Vercel project. **Do not edit it from this repo, and do not copy assets between them — Mamadou's J&J photos are not Rendezvous's, and vice versa.**

- **Local checkout:** `~/Desktop/rendezvous-lounge` (sibling to this repo)
- **GitHub:** https://github.com/richofftechllc-dot/rendezvous-lounge (auto-deploys on push to `main`)
- **Vercel:** `rotech/rendezvous-lounge` → https://rendezvous-lounge.vercel.app
- **Shape:** same single-file static pattern as this repo (`index.html` + `vercel.json` + `assets/`).
- **Cross-links:** the Rendezvous site links here (its `#food` section points at `https://jollof-and-jerk-chi.vercel.app`). This site's `#rendezvous` section currently only links to `@rendezvous_lounge_` on Instagram — when the Rendezvous domain or canonical URL is finalized, add a link to it here too.

## Known stubs / outstanding integrations

These are deliberate placeholders — verify before claiming a feature is "wired up":

- Online ordering form posts nowhere; "Order Now" CTAs scroll to the lead-capture form.
- SMS alerts form is client-side only; no Twilio/etc. integration.
- Uber Eats `store_id` is not set; the live-ordering link is not connected.
- No custom domain attached; deploy currently lives on a `*.vercel.app` URL.
- Three `.rnv-photo` slots in `#rendezvous` are placeholder divs ("Bar photo") — real images haven't been provided.
