# Bacii Build — Handover Note

_Last updated: 2026-07-07. Theme: **bacii/main** (draft, id `190183964964`) · Store: `bacii-the-label.myshopify.com` · Live domain: `baciithelabel.com.au` · Repo: `thelocalfolk/bacii` (branch `main`)._

---

## ⚠️ Two root-cause gotchas we burned hours on (READ FIRST)

1. **Schema `unit` must be ≤ 3 characters.** A custom section (`bacii-marquee.liquid`) had a range setting with `"unit": "px/s"` (4 chars). Shopify's GitHub integration **failed to validate that file**, which cascaded — every `templates/*.json` referencing that section type also failed ("Section type does not refer to an existing section file"), which **froze the entire GitHub→theme sync**. Symptom looked like "deploys don't stick / theme is stuck." Fix was `px/s` → `px`.
   - **Diagnostic tool:** Shopify admin → Online Store → Themes → bacii/main → **"View logs"** shows GitHub-integration validation errors per file. Always check this when a push "doesn't appear."

2. **Stale `.git/index.lock`.** Interrupted git processes left `.git/index.lock`, which silently blocked ALL local git writes (commit/add) and made git commands hang. Fix: `pkill -9 git; rm -f .git/index.lock`.

---

## How deploys work now (it's fixed — use this)

- **Deploy = `git push origin main`.** The GitHub→theme sync then validates + applies to bacii/main (usually < 1 min). No `shopify theme push` — direct CLI pushes get **reverted** on this GitHub-linked theme (GitHub is authoritative).
- If a push doesn't appear: check **View logs** (validation error), fix, push again.
- The sync applies **changed files per commit**. If a template failed earlier due to a bad dependency, after fixing the dependency you must **touch the template** (new commit) so it re-imports.
- **No CDN to purge.** DNS is at GoDaddy → Shopify IP `23.227.38.65`; the `cloudflare`/`cf-ray` headers are Shopify's own and serve dynamic/uncached (`cache-control: no-store`). Earlier "product 404" was a **missing template**, not cache.
- Store is **password protected** (pw `Crumpet2502`). Preview draft theme: `https://bacii-the-label.myshopify.com/?preview_theme_id=190183964964` (sets a preview cookie; then storefront pages show the draft).
- **Note:** the live theme "Bacii x Full Cup" is ALSO GitHub-connected — keep live vs draft straight.

---

## ✅ Live & verified on bacii/main

**Homepage** (`templates/index.json`, Figma `2121:513` desktop / `2121:774` mobile):
- Announcement (mint), Header (cream pill), Hero (blue H1, coral btn, cream gradient), Coral tagline band (`section_GFViaT`), **Wavy marquee — Approach B** (`bacii-marquee.liquid`, text follows the wave via SVG textPath), Value Props (butter, 4 icons + row), About split (periwinkle + cream button), Our Vision (bubblegum + cream button), Newsletter (blue, 2-col, pill input + arrow), Footer (Tiffany, 5 columns, styled newsletter).

**Product page** (`templates/product.json`, Figma `2121:1402` desktop / `2121:1620` mobile):
- **Main:** gallery thumbnails-below, title → ★review block → price → description → size (variant pills) → **coral Add to Cart** (`button-custom` `#ff835d`) → accordions (Fabrication / Product Care / Shipping).
- Then: `pdp_marquee` → `pdp_value_props` ("Made for big personalities and everyday adventures.") → "You may also like" (related products) → `pdp_collections` → `pdp_faq` (pink band, 6 Q accordion + "More FAQ" pill).

**Data:** 9 products imported + published. Theme has all block files (incl. `quantity.liquid`).

---

## 🔧 Remaining work

**Content / copy (placeholders marked with `{# TODO #}`):**
- Product accordions (Fabrication / Product Care / Shipping) — real copy (ideally metafields).
- FAQ answers (6) — real copy.
- Value-props/collection tiles need collections created + tile images; lifestyle photos for About/Vision panels + hero stickers.

**Custom / app sections still to build:**
- **Bacii Club** gallery carousel (product page + homepage-style).
- **Reviews** (Judge.me) — also powers the ★ rating block on PDP.
- **Instagram feed** (Instafeed app or static grid).
- **Wordmark wave** (§13 homepage — oversized `bacii` on a wave).
- Hero **stickers/decals** + hero **wavy divider**.

**Admin:**
- Footer: create 3 nav menus (**Shop**, **Bacii**, **Customer Care**) with the design's links; set real IG/FB/TikTok/Pinterest URLs.
- Fix nav typo if any; create `/pages/faq`, `/pages/about`, `/pages/size-guide` for button links.

**Other templates (after PDP):** About, Fabrication, Collection, Blog, Contact, etc. — each has Desktop+Mobile frames in Figma (`ybvqW2SQfEdqEBompQXHJH`).

---

## Reference
- Figma file key: `ybvqW2SQfEdqEBompQXHJH`. Homepage `2121:513`/`2121:774`; Product `2121:1402`/`2121:1620`; About `2121:1806`/`2121:1969`; Fabrication `2121:2374`.
- Brand tokens live in `snippets/bacii-brand-tokens.liquid`; palette + type in `CLAUDE.md`.
- Custom button/input colours only apply with the `-custom` style variants (`button-custom`, input `input_style: custom`).
