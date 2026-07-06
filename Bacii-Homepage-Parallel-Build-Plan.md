# Bacii Homepage — Native Section Fidelity Plan

Goal: take the **native Horizon sections that are already scaffolded** and edit each one until it matches the Figma design (`2121:513` desktop / `2121:774` mobile). Custom-code sections (§8 reviews, §12 Instagram, §13 wordmark wave, sticker/sparkle decals) are **parked for now.**

---

## Rules of engagement (from CLAUDE.md)
1. **One section at a time. Fix before you move.** No new section until the current one is confirmed matching.
2. **Per-section loop:** edit → screenshot live → screenshot the Figma node → list *every* visual diff → fix → re-screenshot to confirm.
3. **Verbatim copy** — already extracted in `Figma-Node-Map.md`; don't reword.
4. **Tokens, not hex** — colours/type come from `bacii-brand-tokens.liquid` + settings, no stray hardcoded values.

## Sync protocol (GitHub-linked theme)
- Before I edit: `git pull` (picks up any editor commits).
- I edit `index.json` / section settings / `bacii-brand-tokens.liquid`, push, screenshot-compare.
- If you're also editing in the theme editor, we don't work the same section at the same time.

---

## Order of work (native only)

| Step | § | Section | Type | Figma node | Status |
|---|---|---|---|---|---|
| 1 | 1–2 | Announcement + Header | header group | `2121:522` / `2121:539` | pill looks right — verify + fix diffs |
| 2 | 3 | Hero | hero | `2121:520` | built — needs fidelity pass |
| 3 | 4 | Featured products | product-list | `2121:728–731` | built — needs data + fidelity |
| 4 | 5 | Value props | section | `2121:518` | built — verify 4-col layout/type |
| 5 | 6 | About split | media-with-content | `2121:589` | built — needs image + fidelity |
| 6 | 7 | Shop Collections | collection-list | `2121:537`+ | built — needs collections + fidelity |
| — | 8 | ~~Social Proof~~ | *custom* | — | **PARKED** |
| 7 | 9 | Our Vision split | media-with-content | `2121:593` | built — needs image + fidelity |
| 8 | 10 | From the blog | featured-blog-posts | `2121:661` | built — needs posts + fidelity |
| 9 | 11 | Newsletter | section | `2121:662` | built — verify pill input/arrow |
| — | 12 | ~~Instagram~~ | *app* | — | **PARKED** |
| — | 13 | ~~Wordmark wave~~ | *custom* | — | **PARKED** |
| 10 | 14 | Footer | footer group | `2121:691–723` | default — configure to match |
| 11 | all | Full-page compare | — | `2121:513` → `2121:774` | final desktop + mobile pass |

---

## Per-section fidelity checklist (what to diff against Figma)

Each section runs the same loop; these are the usual suspects to check per section.

### Step 1 — Announcement + Header (`2121:522` / `2121:539`)
- Mint bar height/colour, text font + colour, centring.
- Cream pill: radius 1000, height ~72, padding, logo centred, nav order Shop / Our World / Journal / Contact, search + cart-count placement.

### Step 2 — Hero (`2121:520`)
- Full-bleed image position/crop; cream gradient shape (left-half fade — recent commits).
- H1 size/colour/line-height/letter-spacing; intro paragraph; Coral button pill + label; vertical placement of text block.
- Wavy divider at bottom (decorative — may defer if it's an asset).

### Step 3 — Featured products (`2121:728–731`)
- Sub-hero tagline block above cards; intro line + arrows; card ratio, gap, 4-up; title + price type; carousel arrows style.
- (Data: needs real products to look right — Wave 0.)

### Step 4 — Value props (`2121:518`)
- Butter bg; centred H2 on top; 4 equal columns *below*; label (H4) + Poppins-12 body; all Electric Blue; column gap/alignment.

### Step 5 — About split (`2121:589`)
- Media left / Periwinkle panel right, full-width, equal 720 heights; label + H2 + body + cream pill button; text colour Cream; vertical centering.
- (Needs left lifestyle image — placeholder until supplied.)

### Step 6 — Shop Collections (`2121:537`+)
- Heading; 4 tiles ~428×515; label overlays; grid gap; hover.
- (Needs 4 collections + tile images.)

### Step 7 — Our Vision split (`2121:593`)
- Bubblegum panel left / media right; label + H2 + body + cream "Learn More" pill.
- (Needs right lifestyle image; sparkles parked.)

### Step 8 — From the blog (`2121:661`)
- Butter band; "From the blog" + Coral "Go to Blog" button on same row; 3 cards: image, title, date, excerpt, Learn More.
- (Needs 3 posts + images.)

### Step 9 — Newsletter (`2121:662`)
- Blue band; centred heading + copy; pill email input (radius 1000) with arrow submit; text Cream.

### Step 10 — Footer (`2121:691–723`)
- Columns Shop / Bacii / Customer Care / Connect; newsletter repeat; social IG/FB/TikTok; "Website by Good Manners"; footer logo. Type Asap headings / Poppins links.

### Step 11 — Full-page compare
- Assembled homepage vs `2121:513`; then mobile reflow vs `2121:774`. Fix spacing/order/stacking.

---

## Data dependencies (block full fidelity on some sections)
- **§4** real products · **§6/§9** lifestyle photos · **§7** collections + tile images · **§10** blog posts + images.
  Where an asset is missing, match *layout + type + colour* now with a clearly-marked placeholder, and revisit visuals once the asset lands.
