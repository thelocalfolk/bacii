# Bacii Build — Handover Note

_Updated 2026-07-07. Theme: **bacii/main** (draft, id `190183964964`) · Store `bacii-the-label.myshopify.com` · Live domain `baciithelabel.com.au` (pw `Crumpet2502`) · Repo `thelocalfolk/bacii` branch `main`. Figma key `ybvqW2SQfEdqEBompQXHJH`._

Git is in sync: local `main` == `origin/main`. Everything below is on GitHub and deployed to the theme.

---

## ⚠️ CRITICAL gotchas (read before touching anything)

1. **Deploy = `git push origin main`.** The Shopify GitHub integration then validates + syncs to the theme (<1 min). `shopify theme push` does **NOT** persist (linked theme reverts to GitHub). Only git.
2. **Schema `unit` must be ≤ 3 characters.** A `"unit": "px/s"` in a custom section froze the ENTIRE sync (the bad file fails validation → every template referencing it fails → whole sync stalls). If a push "doesn't appear," check **admin → Online Store → Themes → bacii/main → "View logs"** for per-file validation errors. Fix, re-push. If you fix a *dependency*, you must also touch the *template* that referenced it (new commit) so it re-imports.
3. **If git hangs / "index.lock" error:** `pkill -9 git; rm -f .git/index.lock`. A stale lock silently blocks all local git. Use `GIT_OPTIONAL_LOCKS=0`.
4. **No CDN to purge.** DNS at GoDaddy → Shopify IP; served dynamic/no-store. Earlier "product 404s" were a *missing template*, not cache.

## Verifying the live site (SCREENSHOTS ARE HARD)

- **claude-in-chrome screenshot / read_page / scroll all TIME OUT** on this store's pages — their scripts never reach `document_idle`. `javascript_tool` works (execute DOM queries) but theme markup makes selectors fragile.
- **Desktop computer-use screenshot DOES work on Chrome.** Grant it by bundle id: `request_access(["com.google.Chrome"])` (it's not found by display name "Google Chrome"). Then it must be the **front tab** — but browser is view-only (can't click to switch tabs, no switch_to_tab tool), so **ask the user to bring the target page to the front tab**, then `screenshot` + `zoom`.
- **Simplest:** the user pastes screenshots (worked well all session).

---

## ✅ Live & verified

**Homepage** (`templates/index.json`, Figma `2121:513`): announcement, header pill, hero, coral tagline, **wavy marquee — Approach B** (text-follows-wave, `sections/bacii-marquee.liquid`, type `bacii-marquee`), value props (butter), About split (periwinkle), Our Vision (bubblegum), Newsletter (blue), Footer (Tiffany, 5 col).

**Product page** (`templates/product.json`, Figma `2121:1402`): order `main → pdp_marquee(pink) → pdp_value_props(CREAM) → You may also like → pdp_collections → pdp_faq(pink)`. Product-main: gallery carousel+thumbnails-below, title H2, price H4, description, size pills, Size Guide link, **coral Add to Cart only** (Buy-it-now removed), **vertical trust badges** (leaf/recycle/check_box coral icons), accordions (Fabrication/Product Care/Shipping — placeholder text).

**7 templates built (subagents), all verbatim copy, on theme:**
- Page templates: `page.contact` (`2121:4254`), `page.about` (`2121:1806`), `page.faq` (24 Q&A, `2121:3927`), `page.fabrication` (`2121:2374`).
- Dynamic: `collection` (`2121:2615`), `blog` (`2121:2990`), `article` (`2121:3442`).

**Pages created + templates assigned** (handles confirmed): `/pages/about`, `/pages/faq`, `/pages/contact`, `/pages/fabrication` all resolve and render. (Collection/blog/article auto-apply.)

---

## 🔧 Remaining — PRODUCT PAGE (top priority next)

The user's main complaint is the product-main "doesn't match Figma." Biggest issue = **description clutter**: products have rich descriptions ("The good stuff / Size guide / Product & care / Shipping & delivery") inline, which duplicates the (empty) accordions and makes the column much taller than the clean Figma.
- **Recommended fix:** product **metafields** (Fabrication, Product Care, Shipping & Delivery). Move each description's sub-sections into metafields, trim description to the intro, wire the accordions to `closest.product.metafields...`. **Connect the Shopify MCP** (currently needs auth) and this can be automated across all 9 products (read desc → split → write metafields → trim). MCP also unblocks related-products setup + API verification.
- **★ rating + a Reviews section** → need **Judge.me** (the `review` block renders nothing without a reviews source).
- **"What our followers think"** UGC video row (below product-main) → custom section, needs video assets.
- **Gallery thumbnails** — set to carousel + thumbnail_position bottom; **unconfirmed** whether it renders below vs beside — verify visually.
- **"You may also like"** empty → related-products needs setup (or point at a collection).
- Missing sections vs Figma order: **Bacii Club gallery**, **Reviews**, **Instagram**, **wordmark wave** (custom/app — parked).

## 🔧 Remaining — SITE-WIDE

- **Content/copy:** accordion + FAQ answers where marked `{# TODO #}`; trim/relocate product descriptions.
- **Admin/data:** create 4 **collections** (Tees/Shorts/Dresses/Hats) + tile images; **blog posts** + images; **lifestyle photos** for hero/About/Vision/Fabrication panels; footer **nav menus** (Shop/Bacii/Customer Care) + **social URLs**; create `/pages/size-guide` (product Size Guide link points there); **Judge.me** install.
- **Parked custom/app sections:** Instagram feed (Instafeed) · **wordmark wave** (self-contained, quick to build) · hero stickers + wavy divider · Bacii Club gallery · product video row · article prev/next nav.
- **Other Figma templates not yet built:** Gift Card (`2121:3596`), plus mobile-frame fidelity passes.

## Reference
- Homepage `2121:513`/`774` · Product `2121:1402`/`1620` · About `2121:1806` · Fabrication `2121:2374` · Collection `2121:2615` · Blog `2121:2990` · Article `2121:3442` · FAQ `2121:3927` · Contact `2121:4254` · Gift Card `2121:3596`.
- Brand tokens: `snippets/bacii-brand-tokens.liquid`; palette/type in `CLAUDE.md`.
- Custom button/input colours only apply with `-custom` variants (`style_class: button-custom`, `input_style: custom`).
- Panel colours: Periwinkle `#C9BCF4` · Bubblegum `#F5A8B8` · Butter `#FFECA8` · Tiffany `#D8F9F2` · Cream `#FCF5EF` · Coral `#FF835D` · Blue `#007DFE` · Mint `#7BD8B3`.
