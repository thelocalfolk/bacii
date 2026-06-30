# Bacii Homepage — Figma Node Map

Per-section node IDs for the homepage. **File key `ybvqW2SQfEdqEBompQXHJH`.** Parent frame: `2121:513` (Homepage | Desktop), mobile twin `2121:774`.

## Why this file exists (context efficiency)
The Figma file is **flat** — sections are NOT grouped into container nodes, they're clusters of absolutely-positioned elements. So do **not** call `get_design_context` on the whole `2121:513` frame (it returns ~25k+ tokens and truncates). Instead:
- For **copy / colours / sizes** of a section → read the spec in this file. The text and tokens below were already extracted, so you usually don't need a Figma call at all.
- For a **visual reference** of a section → call `get_screenshot` on that section's *background or image* node (listed as “📸 screenshot node” below) — small, targeted, cheap.
- Only call `get_design_context` on a specific element node if you need exact geometry you can't get here.

`top` = y-position on the 8217px-tall desktop canvas (tells you stacking order / vertical band).

---

## 1. Announcement bar — top 0
- `2121:522` 📸 Mint `#7BD8B3` bar bg (h50, w1440)
- `2121:523` text "Free Shipping Over $X in AUD" (Cream, Poppins 15) · `2121:515` duplicate (Universal Sans 12 — trial font)

## 2. Header / nav — top 76  *(Sections.store "Header #1")*
- `2121:539` 📸 Cream `#FCF5EF` pill bg (h72, radius 1000)
- `2121:540` nav text "Shop / Our World / Jorunal / Contact" (Asap 17) — **fix "Jorunal" → Journal**
- `2121:546` "bacii" wordmark logo (Union, centred)
- `2121:541` cart circle + `2121:542` count "1" · `2121:543`/`544`/`545` search/icons

## 3. Hero — top 50–940
- `2121:520` 📸 full-bleed lifestyle image (h888, w1440) · `2121:521` cream gradient overlay
- `2121:548` H1 "Little clothes.\nBig personalities." (Electric Blue, Asap 60, top 355)
- `2121:549` intro paragraph (Blue, Poppins 15, top 523)
- `2121:639` Coral `#FF835D` button "Shop Snack Attack" (top 613)
- Sticker decals top-right: `2121:550`–`566`, `2121:626`, `2121:629`  *(Sections.store "Animated sticker effects")* **TODO — install Sections.store app first**
- `2121:735` 📸 wavy divider (Group 50, top 1199, w1491)

## 4. Featured products — top 1010–1935
- Sub-hero tagline: `2121:524` "Bacii was created to celebrate the big personalities packed into little people." (Cream, 30, top 1010) · `2121:527` sub-copy (top 1101)
- `2121:525` intro line "Our debut collection for little snack monsters, pudding lovers and muffin trouble-makers." (Asap 22, top 1396) · `2121:526` arrows "< >"
- Cards 📸 `2121:728` / `2121:729` / `2121:730` / `2121:731` (378×359, top 1486)
- Titles+prices `2121:645`–`648`: I Scream and Run Tee $45 · Muffin but Trouble Tee $45 · Every Day Terry Shorts $45 · Bacii Bucket Hat $40

## 5. Value props band — top 2021–2476
- `2121:518` 📸 Butter `#FFECA8` bg (h529)
- `2121:528` H2 "Big personalities deserve better basics." (Blue, Asap 30, top 2123)
- 4 columns (label + Poppins 12 paragraph, all Electric Blue):
  - `2121:529`/`530` Organic Cotton
  - `2121:531`/`532` Original Illustrations
  - `2121:533`/`534` Made to Be Passed Down
  - `2121:535`/`536` Ethically Made
- Decals: `2121:632` (Subtract), `2121:635` (Cloud), `2121:770` (Union), `2121:732` (Group 35)

## 6. About split — top 2550–3270
- `2121:569` 📸 left lifestyle image (723×720) · stickers `2121:570`–`586`
- `2121:589` 📸 right Periwinkle `#C9BCF4` panel (720×720)
- `2121:592` "About us" (Asap 22, top 2596) · `2121:590` heading "Bacii celebrates the big personalities packed into little people." (Asap 30, top 2713) · `2121:591` brand-story body (Poppins 15, top 2863)
- `2121:641` Cream pill button "About Us" (top 3162)

## 7. Shop Collections — top 3386–4005
- `2121:638` heading "Shop Collections" (Asap 30, top 3386)
- Tiles 📸 (428×515, top 3490) + label overlays:
  - `2121:537` + `2121:538` "Tees"
  - `2121:517` + `2121:636` "Shorts"
  - `2121:516` + `2121:637` "Dresses"
  - 4th tile = Accessories/Hats (confirm via screenshot — label node not captured)

## 8. Social Proof / reviews — top 4117–4771  *(Judge.me or native carousel)*
- `2121:623` heading "Social Proof" (Asap 30, top 4117)
- `2121:624` subtext — **still Lorem ipsum, needs real copy**
- Review cards 📸 `2121:619` / `2121:621` / `2121:620` / `2121:622` (286×506, top 4265)
- Star ratings `2121:649` / `652` / `655` / `658` (top 4488) · arrows `2121:618` "<" / `2121:625` ">"

## 9. Our Vision split — top 4895–5616
- `2121:593` 📸 left Bubblegum `#F5A8B8` panel (720×720)
- `2121:598` 📸 right lifestyle image (721×721) · sparkles `2121:599`–`615`
- `2121:596` "Our Vision" (Asap 22, top 4938) · `2121:594` heading "Because childhood should be celebrated loudly, joyfully and unapologetically." (Asap 30, top 5225) · `2121:595` body (Poppins 15, top 5378)
- `2121:643` Cream pill button "Learn More" (top 5519)

## 10. From the blog — top 5616–6436
- `2121:661` 📸 Butter `#FFECA8` bg (h820)
- `2121:663` "From the blog" (Asap 22, top 5736) · `2121:707` Coral button "Go to Blog" (top 5738)
- Article images 📸 `2121:685` / `2121:686` / `2121:687` (430×298, top 5818)
- Post 1 `2121:664`/`666`/`667`/`668`: "The Story Behind Bacii" · 20/05/26 · excerpt · Learn More
- Post 2 `2121:669`/`670`/`671`/`672`: "Our Makers"
- Post 3 `2121:673`/`674`/`675`/`676`: "Why We Chose Organic Cotton"

## 11. Join the Bacii Club (newsletter) — top 6436–6755
- `2121:662` 📸 Electric Blue `#007DFE` bg (h319)
- `2121:677` "Join the Bacii Club" (Asap 22, top 6526) · `2121:678` copy (Poppins 12, top 6586)
- `2121:679` email input (border, radius 1000, top 6572) · `2121:680` placeholder "Email Address" · `2121:681` arrow submit

## 12. Instagram feed — top 6850–7136  *(Instafeed app)*
- `2121:665` heading "Follow us on intagram #baciithelabel" (Asap 17, top 6850) — **fix "intagram" → Instagram**
- 6 square posts 📸 `2121:701`–`706` (213×213, top 6923)

## 13. "bacii" wordmark wave — top 7251
- `2121:688` 📸 oversized brand wordmark on wave (Group 44, 2654×966) — decorative, full-bleed

## 14. Footer — top 7900–8217
- Columns (Asap 17 headings + Universal Sans 12 links — trial font, fall back to Poppins):
  - `2121:691`/`692` Shop · `2121:693`/`694` Bacii · `2121:695`/`696` Customer Care · `2121:697` Connect
- Footer newsletter "Join the Bacii Club": `2121:719`/`720`/`721`/`722`/`723`
- Social icons: `2121:709` Instagram · `2121:714` Facebook · `2121:717` TikTok
- `2121:698` "Website by Good Manners" · `2121:699` footer logo (Union)

---

## Mobile
Same content, frame `2121:774` (393×10044). Pull a section's mobile layout with `get_screenshot` on `2121:774` (or its child nodes) when building responsive behaviour — don't infer mobile from desktop.
