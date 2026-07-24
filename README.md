# maidenyeg.ca

MAIDEN's public marketing site — boutique, eco-committed residential
cleaning based in South West Edmonton, Alberta.

Built as plain static HTML/CSS/JS (no framework, no build step),
deployed to GitHub Pages on the custom domain `maidenyeg.ca`. Currently
parked at GoDaddy with a "coming soon" page — this repo is what replaces
that once DNS is repointed (see **Deployment** below).

---

## What this site is (and is not)

- **Is:** the public marketing site — services, pricing estimator,
quote requests, and the "Join Our Team" line.
- **Is not:** a booking backend. Quote and team-inquiry forms currently
open a pre-filled email to `hello.maidenyeg@gmail.com` rather than
submitting to a server — there is no database and nothing is stored
client-side beyond the current page session.

---

## Local development

No install, no build step — it's plain HTML.

```
# Easiest: just open it
open index.html          # macOS
start index.html         # Windows

# Or serve it locally (recommended — some relative-path behaviour
# only matches production when served over http, not file://)
python3 -m http.server 8000
# then visit http://localhost:8000
```

---

## How the site is structured

```
index.html          ← the entire site (hero, services, pricing estimator,
                       booking modal, team modal, Privacy/Terms modals, footer)
  logo-primary.png       ← primary teal/white circular logo (nav, footer)
  logo-hero.png           ← hero-section logo (10% larger text, same asset family)
  favicon.ico, favicon-32.png, favicon-192.png, apple-touch-icon.png
CNAME                ← maidenyeg.ca (required by GitHub Pages — do not delete)
```

There's no templating and no content collection — copy changes mean
editing `index.html` directly. Given the size of the file, search for
the section comment (`<!-- HERO -->`, `<!-- PRICING + ESTIMATOR -->`,
`<!-- BOOKING -->`, etc.) rather than scrolling.

---

## Public repo — safety checklist

This repo is **public**, to keep hosting free on GitHub Pages. Nothing
that counts as client intel or proprietary business intelligence should
ever be committed here. Current state, as a standing checklist to
re-verify before every push:

- [x] No real client names, addresses, or photos anywhere in the repo
- [x] No internal per-unit pricing formula published (the public page
shows only a final estimate; the underlying rate card lives in project
knowledge, not in this repo)
- [x] No Senior Home / Event / Private Office rates published (those
stay quote-only, by design)
- [x] No real Alberta Business ID / GST number yet — footer shows a
"pending" placeholder until registration is complete; replace the
placeholder text only, never commit anything containing SIN, banking,
or registration application details
- [x] Contact info shown (phone, business Gmail) is intentionally public

---

## Deployment

### One-time GitHub Pages setup

1. Push this repo to `github.com/<your-username>/maidenyeg.ca` (public).
2. In **Settings → Pages**, set **Source** to **Deploy from a branch**,
branch `main`, folder `/ (root)`. No GitHub Actions workflow is needed
for a plain static site like this one.
3. Under **Settings → Pages → Custom domain**, enter `maidenyeg.ca` and
save. GitHub will commit a `CNAME` file automatically if one doesn't
already exist (this repo already includes one — don't remove it).
4. **Verify the domain first if you haven't already** — GitHub now
requires domain verification at the account/organization level before
a custom domain will be accepted at the repo level. Do this under your
GitHub profile or org **Settings → Pages → Custom domain verification**
before step 3, or step 3 will fail with a "domain not verified" error.
5. Configure DNS at GoDaddy (replacing the current "coming soon" page):
   - **Apex domain (`maidenyeg.ca`):** four **A** records, all pointing to:
     ```
     185.199.108.153
     185.199.109.153
     185.199.110.153
     185.199.111.153
     ```
   - **`www` subdomain (recommended alongside the apex):** one **CNAME**
     record pointing to `<your-username>.github.io.` (trailing dot).
     GitHub will then auto-redirect whichever one isn't set as the
     primary custom domain to the one that is.
6. Back in **Settings → Pages**, once the green "DNS check successful"
confirmation appears, tick **Enforce HTTPS**. DNS propagation can take
anywhere from a few minutes to ~24 hours — don't panic if it isn't
instant.

### Subsequent deploys

Push to `main`. GitHub Pages redeploys automatically within a minute or
two — no build, no Action to babysit.

---

## Design system reference

All design tokens live inline in `index.html`'s `<style>` block, under
`:root`:

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
(rounded sans, body/UI). Both loaded from Google Fonts via `<link>` in
`<head>` — no local font files to manage for the live site. (Note: the
separately-generated marketing banners in `cover-banners/` embed these
same fonts directly since they're rendered offline as images, not HTML.)

---

## Pre-launch checklist

- [ ] Business Gmail confirmed and swapped into both `mailto:` targets
in `index.html` (quote form and team form) — currently
`hello.maidenyeg@gmail.com`, already confirmed as final
- [ ] Alberta business registration complete; footer "pending" tags
replaced with real Business ID / GST-BN
- [ ] Privacy Policy and Terms of Service reviewed by a lawyer
(currently solid-draft, unreviewed — see modals in footer)
- [ ] DNS configured and propagated for `maidenyeg.ca` (see Deployment)
- [ ] GitHub Pages custom domain verified, set, and HTTPS enforced
- [ ] GoDaddy "coming soon" page fully replaced (confirm old page isn't
cached/still serving after DNS cutover)
- [ ] Test pass on mobile (375px), tablet (768px), desktop (1440px)
- [ ] All three social links in the footer confirmed live (Instagram
@maiden_yeg, TikTok @maidenyeg, Facebook — done as of this checklist)
- [ ] Google Business Profile linked to the live domain once site is up

---

*Last updated: July 2026.*
