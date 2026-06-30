# Bacii Homepage — Code Build Plan

Theme: **Shopify Horizon** · Source of truth: [Figma — Bacii Website Design](https://www.figma.com/design/ybvqW2SQfEdqEBompQXHJH/Bacii-%7C-Website-Design?node-id=2121-513) (Homepage | Desktop, node `2121:513`)

This plan covers the **homepage** as the first build. The same method rolls out to the other 12 templates afterward.

---

## 1. How we keep it on-design

The design is read straight from Figma via the Dev Mode MCP — exact colours, fonts, spacing and text, not eyeballed from a screenshot. To avoid drift we follow four rules:

1. **Tokens first.** Every colour, font and size below is defined once in Horizon's settings + a base CSS variable layer. No hardcoded hex in sections.
2. **One section at a time.** Build a section → preview it live (`shopify theme dev`) → screenshot it → compare against its Figma frame → fix → only then move on.
3. **Absolute → responsive.** Figma exports everything as absolutely-positioned pixels. We do **not** copy that. Each section is rebuilt as a proper responsive Horizon section (fl/grid, theme settings) that matches the design visually at desktop width and reflows sensibly to the mobile frames.
4. **Reuse Horizon, don't fight it.** Before building, read the real Horizon section/block files in this repo and follow its conventions (theme blocks, schema, `settings_data.json`). Match the design *within* Horizon's architecture rather than bolting on a parallel system.

---

## 2. Design tokens

### Colours
| Token | Hex | Use |
|---|---|---|
| Cream | `#FCF5EF` | Page background, light text on colour |
| Dark Grey | `#59697A` | Body text, nav |
| Electric Blue | `#007DFE` | Hero headline, accent, newsletter band |
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

- **Asap** and **Poppins** are both Google Fonts — load via Shopify's `font_picker` or `@font-face`.
- ⚠️ **"Universal Sans Display Trial"** appears in some text (announcement bar, footer menus, a few labels). It is a *trial* font and cannot be used in production. **Decision needed:** license Universal Sans, or fall back to Asap/Poppins. Plan assumes fallback to Poppins unless told otherwise.

### Other tokens
- Button radius: ~28px (full pill on inputs: `1000px`).
- Section max width: 1440 design canvas → build to Horizon's standard page width with consistent side padding (~3.85% / ~55px desktop gutter in the design).

---

## 3. Homepage section inventory (top → bottom)

| # | Section | Figma | Build approach | Notes |
|---|---|---|---|---|
| 1 | Announcement bar | top 0, Mint | Horizon native announcement bar | "Free Shipping Over $X in AUD". Possibly the **Scrolling Text** Sections.store piece if a marquee is wanted. |
| 2 | Header / nav | top 76, Cream pill | **Sections.store "Header #1"** — configure to match | Logo "bacii", menu: Shop / Our World / Journal / Contact, search + cart w/ count. |
| 3 | Hero | top 50–940 | Native section | H1 "Little clothes. Big personalities." (Blue 60), intro paragraph, Coral "Shop Snack Attack" button, full-bleed lifestyle image w/ cream gradient, decorative stickers top-right. Wavy divider below. |
| 4 | Featured products carousel | top 1396–1884 | Native section (product list / featured collection) | Intro line + 4 product cards w/ arrows. Titles + prices: I Scream and Run Tee $45, Muffin but Trouble Tee $45, Every Day Terry Shorts $45, Bacii Bucket Hat $40. |
| 5 | Value props band | top 2021–2476, Butter | Native section | "Big personalities deserve better basics." + 4 icon columns: Organic Cotton, Original Illustrations, Made to Be Passed Down, Ethically Made. Cloud/shape decals. |
| 6 | About split | top 2550–3270 | Native image-with-text | Left lifestyle image, right Periwinkle panel: "About us" + brand story paragraph. |
| 7 | Shop Collections | top 3386–4005 | Native collection-list | "Shop Collections" + 4 category tiles (Tees, Shorts, Dresses, +1) with label overlays. |
| 8 | Social Proof / reviews | top 4117–4771 | **Judge.me** reviews (styled) or native carousel | "Social Proof" + 4 review cards w/ star ratings + arrows. Judge.me is in the stack. |
| 9 | Our Vision split | top 4896–5616 | Native image-with-text | Left Bubblegum panel: "Our Vision" + paragraph + "Learn More"; right lifestyle image w/ sparkles. |
| 10 | From the blog | top 5616–6436, Butter | Native blog-posts section | "From the blog" + "Go to Blog" button + 3 article cards (title, date, excerpt, Learn More). |
| 11 | Join the Bacii Club | top 6436–6755, Blue | Native newsletter / Klaviyo-Shopify form | Heading + copy + email input w/ arrow submit. |
| 12 | Instagram feed | top 6850–7136 | **Instafeed app** | "Follow us on instagram #baciithelabel" + 6 square posts. |
| 13 | Big "bacii" wordmark wave | top 7251 | Native — large SVG/brand graphic on wave | Decorative oversized logo band. |
| 14 | Footer | top 7900–8217 | Horizon native footer | Columns: Shop / Bacii / Customer Care / Connect + newsletter, social icons (IG, FB, TikTok), "Website by Good Manners". |

**Decorative stickers / sparkles** (stars, clouds, scribbles overlaid across the hero and panels) map to the **"Animated sticker effects"** Sections.store piece. The pink "Architectural Digest" quote and "Get Inspired" video grid from the strategy doc appear to live on other templates, not the homepage.

---

## 4. Build order

1. **Global foundation** — register colour scheme + fonts in Horizon settings; add base CSS variable layer; set button styles. (Nothing visible yet, but everything references it.)
2. **Install + configure the purchased Sections.store sections** (Header #1, Animated sticker effects, Scrolling Text if used) into the theme so they're real files before assembly.
3. **Header + announcement bar** (sections 1–2) — top of page, sets the frame.
4. **Hero** (3).
5. **Featured products** (4) — needs sample products in the store.
6. **Value props** (5).
7. **About split** (6).
8. **Shop Collections** (7) — needs collections created.
9. **Social Proof / Judge.me** (8).
10. **Our Vision split** (9).
11. **Blog** (10) — needs blog posts.
12. **Newsletter** (11).
13. **Instagram / Instafeed** (12).
14. **Wordmark wave + Footer** (13–14).
15. **Full-page verify** — screenshot the assembled homepage vs the Figma frame end-to-end; fix drift; check mobile against `Homepage | Mobile`.

Each step ends with a screenshot-compare against its Figma node before it's marked done.

---

## 5. To confirm before / during build

- **Font:** license "Universal Sans Display Trial", or fall back to Poppins/Asap?
- **Sections.store install type:** do the purchased sections drop in as native `.liquid` section files, or via the app's embed/app block? (Affects how cleanly they slot into Horizon.)
- **Reviews:** build Social Proof as styled Judge.me, or a native carousel fed manually?
- **Products/collections/blog:** the homepage needs real sample products, 4 collections (Tees/Shorts/Dresses/Accessories) and a few blog posts to populate sections 4, 7 and 10. I can scaffold placeholders.
- **Newsletter backend:** Shopify native customer form, or Klaviyo/Mailchimp?

---

## 6. Dev + deploy setup (recommended)

- **Shopify CLI** for the build loop (`shopify theme dev` = live reload for the screenshot-verify cycle).
- **GitHub** connected to the Horizon theme for version control / rollback.
- This folder = the git repo; theme files pulled via `shopify theme pull`.
