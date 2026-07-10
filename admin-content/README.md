# Admin content — paste into Shopify admin

This folder holds content that **cannot ship via theme files** (it lives in Shopify's database, not the theme). Everything here is verbatim from `Bacii_COPY FOR WEBSITE_WIP.docx`. This folder is ignored by the Shopify GitHub theme sync — it's just here for handover.

## Blog posts (5)
Shopify admin → **Online Store → Blog posts → Add blog post**. For each file:
1. Title = the filename's title (also shown as a comment at the top of each file).
2. Open the content editor, click the `<>` (show HTML) button, and paste the file's HTML.
3. Author: Bacii the Label. No featured images supplied yet — add when ready.

| File | Title |
|---|---|
| `blog-01-the-story-behind-bacii.html` | The Story Behind Bacii |
| `blog-02-our-makers.html` | Our Makers |
| `blog-03-why-we-chose-organic-cotton.html` | Why We Chose Organic Cotton |
| `blog-04-why-childhood-should-be-messy.html` | Why Childhood Should Be Messy |
| `blog-05-how-to-build-a-capsule-wardrobe-for-kids.html` | How to Build a Capsule Wardrobe for Kids |

## Collection description
`collection-snack-attack-description.html` → **Products → Collections → Snack Attack → Description** (paste via the `<>` HTML view).

## Policies (also in the theme as pages)
The Privacy Policy, Terms of Service and Shipping copy ship as theme page templates (`templates/page.privacy-policy.json` etc. — see below). But Shopify's **checkout footer** links to **Settings → Policies**, so paste these there too:

| File | Settings → Policies field |
|---|---|
| `policy-privacy.html` | Privacy policy |
| `policy-terms-of-service.html` | Terms of service |
| `policy-shipping.html` | Shipping policy |

## Activating the theme policy pages
**Online Store → Pages → Add page** three times:
- "Privacy Policy" → Theme template: `page.privacy-policy`
- "Terms of Service" → Theme template: `page.terms-of-service`
- "Shipping" → Theme template: `page.shipping-policy`

Leave the page body empty — the copy is baked into the template. Then link them in the footer menu (Navigation).

## Known copy flags (kept verbatim from the doc — confirm with Peta)
- Shipping section says `hello@baciithelabel.com` (missing `.au`) for overseas orders.
- "The Story Behind Bacii" has "As a mum to, two beautiful boys" (stray comma).
