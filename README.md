# maidenyeg.ca

MAIDEN's public marketing site — boutique, eco-committed residential cleaning based in South West Edmonton, Alberta.

Built as plain static HTML/CSS/JS (no framework, no build step), deployed to GitHub Pages on the custom domain `maidenyeg.ca`. Currently parked at GoDaddy with a "coming soon" page — this repo is what replaces that once DNS is repointed (see **Deployment** below).

---
## What this site is (and is not)

- **Is:** the public marketing site — services, pricing estimator, quote requests, and the "Join Our Team" line.
- **Is not:** a booking backend. Quote and team-inquiry forms currently open a pre-filled email to `hello.maidenyeg@gmail.com` rather than submitting to a server — there is no database and nothing is stored
client-side beyond the current page session.

---
## How the site is structured

There's no templating and no content collection — copy changes mean editing `index.html` directly. Given the size of the file, search for the section comment (`<!-- HERO -->`, `<!-- PRICING + ESTIMATOR -->`,`<!-- BOOKING -->`, etc.) rather than scrolling.

---
## Public repo — safety checklist

This repo is **public**, to keep hosting free on GitHub Pages. Nothing that counts as client intel or proprietary business intelligence should ever be committed here. Current state, as a standing checklist to re-verify before every push:

- [x] No real client names, addresses, or photos anywhere in the repo
- [x] No internal per-unit pricing formula published (the public pageshows only a final estimate; the underlying rate card lives in project knowledge, not in this repo)
- [x] No Senior Home / Event / Private Office rates published (those stay quote-only, by design)
- [x] Only Alberta Business ID / GST number in the footer, never commit anything containing SIN, banking ,or registration application details
- [x] Contact info shown (phone, business Gmail) is intentionally public

---
## Deployment

### Subsequent deploys
Push to `main`. GitHub Pages redeploys automatically within a minute or two — no build, no Action to babysit.
---

## Design system reference
All design tokens live inline in `index.html`'s `<style>` block, under `:root`:

| Token | Value | Use |
|---|---|---|
| `--pine` | `#0F6B5C` | Primary brand teal |
| `--pine-deep` | `#0A4A40` | Headlines, hover states, dark UI |
| `--sage` | `#DCE8E1` | Soft backgrounds, service card fill |
| `--sage-deep` | `#B9D0C4` | Inner accents |
| `--cream` | `#FBFAF5` | Page background |
| `--ink` | `#16211D` | Body text |
| `--ink-soft` | `#54645D` | Secondary text, captions |
| `--line` | `#D8E1DC` | Hairlines, borders |

Typography: **Fraunces** (variable serif, display) + **Nunito**
(rounded sans, body/UI). Both loaded from Google Fonts via `<link>` in `<head>` — no local font files to manage for the live site. (Note: the separately-generated marketing banners in `cover-banners/` embed these same fonts directly since they're rendered offline as images, not HTML.)

*Last updated: July 2026.*
