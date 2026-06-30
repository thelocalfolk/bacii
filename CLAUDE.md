# CLAUDE.md — Bacii Shopify Build

Execution brief for building the **Bacii** storefront on the **Shopify Horizon** theme, exactly to the Figma design. Read this first, then `Bacii-Homepage-Build-Plan.md` for the full section detail. **Start with the homepage.**

---

## ⛔ HARD RULES — read these every session, no exceptions

These override convenience. Breaking either one is a failure of the task.

1. **ONE SECTION AT A TIME — FIX BEFORE YOU MOVE.**
   For each section: build it → `get_screenshot` the live result → `get_screenshot` the matching Figma node (see `Figma-Node-Map.md`) → list EVERY visual difference → fix until it matches → re-screenshot to confirm.
   **Do NOT start, touch, or add any other section while the current one still has unresolved differences.** If a section has known errors (e.g. the hero), the ONLY allowed next action is fixing that section. No new sections until the current one is confirmed matching.

2. **VERBATIM COPY ONLY — never invent or reword text.**
   Every piece of text — headings, body, button labels, nav, captions — must be the EXACT string from the Figma node. Read it with `get_design_context` and copy it character-for-character. Do **not** paraphrase, shorten, expand, fix grammar, or make up labels like "View all" or "Learn more" unless those exact words are in the design.
   If the design's copy has a typo, keep it and add a `{# TODO: confirm copy #}` note — except the three already-approved fixes (Jorunal→Journal, intagram→Instagram, and replacing the Social Proof Lorem ipsum once real copy is supplied).
   If text is genuinely missing from the design, insert a clearly-marked `TODO` placeholder and flag it — do NOT fill the gap with invented words.

3. **No layout invented.** Match the Figma's arrangement (alignment, order, columns, icon placement), not just its words. The value-props band, for example, is a centred heading on top with four icon columns BELOW — not a heading beside the columns.

---

## 0. Setup before you build

1. **Connect the Figma Dev Mode MCP** (this is non-negotiable for fidelity — build from live node data, not from this doc's descriptions).
   - File key: `ybvqW2SQfEdqEBompQXHJH`
   - Homepage | Desktop node: `2121:513` · Homepage | Mobile node: `2121:774`
   - Per section: `get_design_context` for structure/text/tokens, `get_screenshot` to compare, `download`/asset URLs for images & SVGs.
2. **Pull the Horizon theme** into this folder via Shopify CLI (`shopify theme pull`). The store owner permission wall only blocks the Claude *connector app* — CLI uses your collaborator/theme access and is fine.
3. **Read the real Horizon files first** (`sections/`, `blocks/`, `snippets/`, `config/settings_schema.json`, `config/settings_data.json`, `templates/index.json`). Match Horizon's conventions — it uses the **theme-blocks architecture** (nestable blocks with their own schema). Build within it; don't bolt on a parallel system.
4. Run `shopify theme dev` for live reload during the build/verify loop.

---

## 1. Non-negotiable methodology (how we keep it on-design)

1. **Tokens first** — define every colour/font/size once (§2); no hardcoded hex in sections.
2. **One section at a time** — build → preview → `get_screenshot` of the built section → compare to the Figma frame → fix → only then move on.
3. **Absolute → responsive** — the Figma file is flat & absolutely positioned with NO auto-layout and NO components. Do NOT copy pixel coordinates. Rebuild each section as a proper responsive Horizon section that matches the design at desktop (1440 canvas) and reflows to the mobile frame (`2121:774`).
4. **Verify, don't assume** — section boundaries below were inferred from y-coordinates; confirm against screenshots.

---

## 2. Design tokens (→ Horizon `settings_data.json` color schemes + base CSS variables)

### Colours
| Token | Hex | Use |
|---|---|---|
| Cream | `#FCF5EF` | Page bg; light text on colour |
| Dark Grey | `#59697A` | Body text, nav |
| Electric Blue | `#007DFE` | Hero headline, accents, newsletter band |
| Coral | `#FF835D` | Primary buttons |
| Mint | `#7BD8B3` | Announcement bar |
| Butter | `#FFECA8` | Value-prop band, blog band |
| Bubblegum | `#F5A8B8` | "Our Vision" panel |
| Periwinkle | `#C9BCF4` | "About us" panel |
| Tiffany Blue | `#D8F9F2` | Accent |

### Type
| Style | Font | Size / line-height | Letter-spacing |
|---|---|---|---|
| Heading 1 | Asap | 60 / 1.0 | 2 |
| Heading 2 | Asap | 30 / 1.15 | 2 |
| Heading 4 | Asap | 22 / 25px | 2 |
| Heading 5 | Asap | 17 / 20px | 2 |
| Buttons | Asap | 18 / 1.5 | 2 |
| Underlined link | Asap | 14 / 33px | 0 |
| Paragraph 1 | Poppins | 15 / 1.5 | 0 |
| Paragraph 2 | Poppins | 12 / 1.55 | 0 |

- Asap + Poppins = Google Fonts (load via Horizon `font_picker` or `@font-face`).
- ⚠️ **"Universal Sans Display Trial"** appears in some text (announcement bar, footer menus, a few labels). It is a TRIAL font — cannot ship. **Default: fall back to Poppins** unless the client licenses Universal Sans. Confirm before finalizing.
- Buttons: full pill, radius ~28px; inputs radius `1000px`.

---

## 3. Homepage section map (top → bottom)

All node IDs are children of `2121:513`. Source = how to build it. **Per-section node IDs + extracted copy/colours are in `Figma-Node-Map.md` — read that when building a section. Do NOT call `get_design_context` on the whole `2121:513` frame (it truncates at ~25k tokens); pull per-section nodes or use the screenshot nodes listed there.**

| # | Section | Source | Key content |
|---|---|---|---|
| 1 | Announcement bar | Horizon native (or Sections.store Scrolling Text if marquee wanted) | Mint band, "Free Shipping Over $X in AUD" |
| 2 | Header / nav | **Sections.store "Header #1"** — configure to match | Cream pill; logo "bacii"; menu Shop / Our World / Journal / Contact; search + cart count |
| 3 | Hero | Native | H1 "Little clothes. Big personalities." (Blue 60), intro, Coral "Shop Snack Attack" btn, full-bleed image + cream gradient, sticker decals, wavy divider |
| 4 | Featured products carousel | Native (featured collection) | Intro line + 4 cards w/ arrows: I Scream and Run Tee $45 · Muffin but Trouble Tee $45 · Every Day Terry Shorts $45 · Bacii Bucket Hat $40 |
| 5 | Value props band | Native | Butter bg, "Big personalities deserve better basics." + 4 icon cols: Organic Cotton · Original Illustrations · Made to Be Passed Down · Ethically Made |
| 6 | About split | Native image-with-text | Left lifestyle image · right Periwinkle panel "About us" + brand story |
| 7 | Shop Collections | Native collection-list | "Shop Collections" + 4 category tiles (Tees, Shorts, Dresses, +1) w/ label overlays |
| 8 | Social Proof / reviews | **Judge.me** styled, or native carousel | "Social Proof" + 4 review cards w/ star ratings + arrows |
| 9 | Our Vision split | Native image-with-text | Left Bubblegum panel "Our Vision" + paragraph + "Learn More" · right lifestyle image w/ sparkles |
| 10 | From the blog | Native blog-posts | Butter band, "From the blog" + "Go to Blog" btn + 3 article cards (title, date, excerpt, Learn More) |
| 11 | Join the Bacii Club | Native newsletter form | Blue band, heading + copy + email input w/ arrow submit |
| 12 | Instagram feed | **Instafeed app** | "Follow us on instagram #baciithelabel" + 6 square posts |
| 13 | "bacii" wordmark wave | Native — oversized brand SVG on wave shape | Decorative band |
| 14 | Footer | Horizon native footer | Columns Shop / Bacii / Customer Care / Connect + newsletter; social icons IG/FB/TikTok; "Website by Good Manners" |

**Decorative stickers/sparkles** across hero & panels → **Sections.store "Animated sticker effects"**. The pink "Architectural Digest" quote and "Get Inspired" video grid from the strategy doc appear on other templates, not the homepage.

### Purchased Sections.store sections (configure-to-match, don't rebuild)
Header #1 · Scrolling Text #3 · Animated sticker effects · Sticker pin/pro · Video grid social media v3 · Size Guide · Product videos. Install as theme files BEFORE assembling the pages that use them.

---

## 4. Build order

1. Global foundation — color schemes + fonts + button styles in Horizon settings; base CSS variable layer.
2. Install + configure purchased Sections.store sections.
3. Header + announcement (1–2) → Hero (3) → Featured products (4) → Value props (5) → About split (6) → Shop Collections (7) → Social Proof (8) → Our Vision (9) → Blog (10) → Newsletter (11) → Instagram (12) → Wordmark wave + Footer (13–14).
4. Full-page verify: assembled homepage vs Figma `2121:513`, then mobile vs `2121:774`.

Each step ends with a screenshot-compare against its Figma node.

---

## 5. Open questions (resolve with Eliza)

- Font: license Universal Sans Display Trial, or fall back to Poppins/Asap?
- Sections.store install type: native `.liquid` files or app block/embed?
- Reviews: styled Judge.me vs native carousel?
- Sample data: homepage needs real products, 4 collections (Tees/Shorts/Dresses/Accessories), a few blog posts to populate §4, §7, §10.
- Newsletter backend: Shopify native form, or Klaviyo/Mailchimp?

### Content fixes noticed in the Figma copy
- "Jorunal" → **Journal** (nav)
- "intagram" → **Instagram**
- Social Proof subtext is still **Lorem ipsum** — needs real copy.

---

## 6. Other templates (after homepage)

Same method for: Product, About, Fabrication, Collection, Blog/Collection, Blog/Single, Gift Card, FAQ, Contact, Privacy Policy, Terms of Service, Shipping Policy — each with Desktop + Mobile frames in the same Figma file.

---

## 7. Project facts

- Theme: **Horizon** (already installed on the Bacii store).
- Figma file: `ybvqW2SQfEdqEBompQXHJH` — single page "Final Design" (`2121:512`); strategy doc at `2008:2`.
- Dev/deploy: Shopify CLI for the build loop + GitHub for version control. This folder = the git repo.
- The Claude Shopify *connector app* is blocked by the client store's permissions — not needed; use CLI.
