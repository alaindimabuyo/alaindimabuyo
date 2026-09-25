---
name: anatomy-ux-redesign
description: Use when redesigning, critiquing, polishing, or auditing an existing screen, especially a product detail page (mobile or web e-commerce, marketplace, grocery, SaaS item or plan detail), when a screen "looks cheap", "feels messy", or does not convert, or when asked to "make it premium", "clean up the UI", "spot the mistakes", or fix icons on images, alignment, color, typography, badges, reviews, dividers, spacing, price, quantity, or the add to cart button. Applies even if the user only says "make this page look better".
---

# Anatomy: UX Redesign

A redesign has two passes. The **fix pass** removes mistakes, one at a time, each with a stated reason. The **flow pass** makes buying (or the screen's main action) easier. A redesign that only looks cleaner has done half the job.

## Using this in any project
- **With a codebase:** read the real screen first: its components, design tokens (colors, type scale, spacing), the catalog data it renders (all image types, longest titles, missing ratings, sold-by-weight vs per-item), and how price, discount, and quantity are computed. Search by content ("product", "price", "addToCart", "tokens") instead of assuming a folder layout.
- **Without a codebase:** use the owner's description or screenshot. Data you were not given (review counts, previous prices, popular quantities) is `[NEEDS: ...]`.
- **Output format:** the before/after table in Step 3, then code in the project's framework if one is named.

## Shared rules (same in all anatomy-* skills)
- Never invent facts, prices, discounts, ratings, or claims. Use `[NEEDS: ...]` placeholders and list them at the end.
- Keep facts identical across the site. Structured data (Product, Offer, AggregateRating) must match the visible text exactly.
- When the owner's request conflicts with this skill, build the skill's version and output a "Changed from the request" table: asked for, built, why. Do not drop a request silently, and do not build a request that breaks accessibility or consumer law because it was asked for.

This skill adds two rules.

**1. Design for the whole catalog, not one screenshot.** Every fix must hold for the brightest image, the busiest image, the longest title, a product with no reviews, and a product with no discount. Test the redesign against those cases before calling it done.

**2. A visual element may only state a true fact.** A discount badge needs a real previous price: for EU consumers, the lowest price in the 30 days before the reduction (Price Indication Directive Art. 6a, via the Omnibus Directive). Raising the price before a sale to show a bigger percent is a fake reference price; do not design the badge, replace it with the real one or none. A rating shows its real count ("4.6 · 212 reviews"). A total in the button is the real total, marked "est." if the final weight can vary.

## Step 0: See the screen first (Playwright MCP)
Before any audit, critique, or redesign, open the real screen in the Playwright MCP browser. Do not audit from code, a description, or memory of the page.

1. **Get the URL.** A running local dev server or a deployed URL of the screen. If none is given, ask for it, or start the project's dev server. If the screen cannot be opened at all (only a screenshot or a brief exists), say so at the top of the output and mark every finding "unverified in browser".
2. **Open it:** `browser_navigate` to the URL. If the screen needs sign-in or a specific state (item in cart, sale product, product with no reviews), reach that state with real clicks and typing, not by editing the DOM.
3. **Capture both widths:** `browser_resize` to 390×844 (mobile), then `browser_take_screenshot` (full page) and `browser_snapshot` (accessibility tree); repeat at 1440×900 (desktop).
4. **Read what rendered:** look at every screenshot before writing findings. Use the snapshot for control names, labels, and headings. Use `browser_evaluate` to read computed colors and font sizes when a contrast or size finding depends on the exact value.
5. **Check the console:** `browser_console_messages` for errors that break the screen.
6. **Walk the flow:** scroll the full page and capture it mid-scroll (sticky bar, header behavior); change the quantity and confirm the total updates; open at least one bright-image product, one long-title product, and one with no reviews for the catalog stress test (rule 1).
7. **Close the browser** (`browser_close`) when done.

Every finding in the audit cites what it came from: a screenshot (width), a snapshot entry, or a measured value. A finding with no browser evidence is marked "unverified in browser".

If the Playwright MCP server is not connected, stop and tell the user; do not fall back to guessing the layout. If navigation fails with "Browser is already in use", another session holds that browser profile: try any other connected Playwright MCP server, otherwise wait and retry, and never kill another session's browser or delete its lock file.

## Step 1: Fix pass (check each, fix what fails)

| # | Area | Mistake | Fix |
|---|---|---|---|
| 1 | Icons on images | Nav icons readable only on dark photos | Put each icon in a small solid or translucent container; icon to background contrast at least 3:1 (WCAG 1.4.11) on every catalog image; tap target at least 44×44 pt (Apple) / 48×48 dp (Android), never below 24×24 CSS px |
| 2 | Product image | Busy frame, hands or props as focus, single item for a product sold by weight, artificial backdrop, every product styled differently | One catalog image system: same background, lighting, angle, and crop for all products; the product is the focal point; image shows the quantity sold. Lifestyle photos go further down the gallery |
| 3 | Alignment | Elements drift off a shared edge | One grid: same side margin everywhere (e.g. 16 or 24 px), a spacing scale (4 or 8 px steps), shared left edges |
| 4 | Color | Saturated colors everywhere compete | Neutral base, one accent for the main action and one for sale; color never the only signal (WCAG 1.4.1) |
| 5 | Typography | Several font families | One family (two at most); hierarchy from size, weight, color, line height. Use the project's font; do not swap brands to a new font unasked |
| 6 | Labels and badges | Cramped caps; long badges ("🔥 30% OFF DISCOUNT!!") | Small caps labels get letter spacing (about 0.05 to 0.1 em); badges say one thing ("−30%"), one color, no emoji |
| 7 | Title | Too loud or too weak; contains a quantity the user can change ("Avocados 1kg" with a stepper) | Title names the product only; size and weight above body, below nothing else in the details area; long titles wrap to 2 lines, never truncate the key word |
| 8 | Body text | Tight line height, low contrast | Line height 1.4 to 1.6, 16 px on mobile, contrast at least 4.5:1 (WCAG 1.4.3). "Softer" means a darker grey that still passes, never #bbb on white |
| 9 | Reviews | Rating far from the title | Rating with count directly under the title, linked to the reviews; hide the row (do not show 0 stars) when there are no reviews |
| 10 | Feature icons | Mixed colors, filled and outline styles | One icon set, one stroke weight, one color; each icon has a text label |
| 11 | Dividers | Thick dark lines | Hairline in a light neutral, or spacing alone |
| 12 | Spacing | Uneven gaps; related items far apart | Related items close, groups separated (proximity); use the spacing scale from #3 |
| 13 | Price label | "Price:" before the amount | Drop the visible word; the currency makes it clear. The quantity stepper still needs an accessible name ("Quantity, kg") and a visible unit, because removing visual labels never removes accessible names |
| 14 | Price position | Price far below the fold | Price (and unit price, e.g. "€4.99 / kg", required for many EU grocery listings) near the title |
| 15 | Main action | All-caps shouting button; quantity far from it | Sentence case ("Add to cart"); stepper right next to the button with the unit inside; button shows the total ("Add · €9.98"), updated live and announced to screen readers |

## Step 2: Flow pass (add what fits the product)
- **Sticky action bar:** quantity and "Add to cart" stay visible while scrolling. Respect safe areas; add bottom padding so it never covers the last content.
- **Content card over the image:** details scroll up over the image; the title moves into the top bar once the image is gone so context stays. Turn off the motion for `prefers-reduced-motion`.
- **Preset quantities:** one-tap chips ("500 g · 1 kg · 2 kg") drawn from real order data (`[NEEDS: top quantities]` if unknown), plus the custom stepper. Related: `anatomy-ux-psychology` (smart defaults).

## Step 3: Output
- Before/after table: area, before, after, reason, the rule or standard it follows
- Catalog stress test results (rule 1): brightest image, longest title, no reviews, no discount
- "Changed from the request" table
- Tokens used (colors with contrast ratios, type scale, spacing scale)
- `[NEEDS: ...]` list

## Auditing an existing screen
Run Step 0 first. Report pass/fail with the fix for each row of Step 1, then:
16. The design holds for every catalog stress case
17. Every badge, rating, and total states a true, sourced fact
18. Main action and quantity stay reachable while scrolling
19. Every control has an accessible name; text passes contrast; motion respects reduced-motion
