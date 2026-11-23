# Layout: width, pages, cards, lists, nested controls, screen actions and the logo

House default. When the project has its own system, express this through its components and tokens (SKILL.md, rule zero).

## Reading width (strict)
Settings, forms, detail pages, pickers and single-item pages sit in **one centred column about the width of a card (600–720px)**, never stretched across a wide screen. Lines stay readable and the eye doesn't travel.

- The back arrow, page title and screen actions line up to the column, not to the window edge.
- Dashboards, tables with many columns and boards may use the full width. A table too wide for the column scrolls sideways inside its card.
- When content gets tight in the column, restack it (label/value rows, two rows of tiles, a dropdown instead of wrapping tabs) instead of widening the column.

## Even page padding
The space above the first heading **matches the side padding**, and the bottom padding matches the top. A page never starts with a cramped top and a deep side gutter.

## Page header
- **Detail pages:** the parent's name sits next to the back arrow on one line (and links back to it). The page's own title sits below at a real heading size (H2, ~24px), never a small bold line.
- **Section headings sit one step below the page title**, and every section or card title in the product uses **the same size** (e.g. 16/600). Measure them across screens; one-offs at 14 or 20 are bugs.
- **One gap between sections** on a page (e.g. 24px): between cards, between a heading and the card above it, before footnotes. Tighter gaps belong inside cards.
- Remove headings and labels that repeat the nav, the breadcrumb or a selector's own value.

## Say it once
A page states each fact once. If a card already says "Data unavailable" in its value, don't add a "Data unavailable" tag above it or a status chip beside it. Delete the duplicate, keep the clearest one.

## Cards and containers
- **Entities are cards.** Things with several facts each (products, accounts, projects) are cards with their facts laid out, not bare list rows. Row lists (below) stay for table-like lists of many similar items.
- **Peers get their own container.** Two sections of equal weight are two containers, not one box split by a line.
- **Sibling cards line up.** Cards side by side stretch to the same height. Their matching parts (title, description, the bottom metric or action) align across cards, with the bottom part anchored to the bottom. Multi-line titles and descriptions clamp to 2 lines with an ellipsis (`line-clamp: 2`), full text in a tooltip or the detail page.

## Rows with a leading icon
- **The padding before the icon equals the gap between the icon and the text** (e.g. 16 and 16, or 20 and 20).
- **One-line rows centre the icon** on the text; **multi-line rows align it to the first line.**
- The same pattern uses the same icon size and spacing on every screen. When a row style is fixed on one page, fix it everywhere it appears.

## Sticky picker edges
In a long picker step (choosing products, people, files), the **title, selected count and search stay pinned at the top**, separated from the list by the same divider the pinned action bar uses at the bottom. The list scrolls between them.

## Row lists are one table (strict)
When a screen shows a table-like list (many rows, each drawn as its own bordered or shadowed card with a small gap between them), merge the rows into **one container**.

| Part | Spec |
|---|---|
| Container | one surface, radius 12, `overflow: hidden` (keep `overflow: auto` on lists that scroll) |
| Rows | no gap, no radius of their own, no border or shadow. The first row carries the top corners and the last row the bottom ones |
| Dividers | a 1px horizontal hairline between rows in the alpha border colour, none after the last row |
| Hover | a fill step on the row, never a border, shadow or lift |
| Selected / expanded | a tinted fill shared by the row and its expanded detail, so they read as one unit. No coloured outline |
| Focus | ring inside the row (`outline-offset: -2px`) so the container doesn't clip it |

Applies to patient, order and user lists, file lists, and pickers in dialogs. **Multi-column card grids stay separate cards.**

```css
.list { border-radius: 12px; overflow: hidden; background: var(--surface); }
.list > .row { border-radius: 0; margin: 0; box-shadow: none; border: 0; }
.list > .row + .row { border-top: 1px solid var(--border); }
.list > .row:hover { background: var(--surface-hover); }
```

## Nested controls have an equal inset (strict)
When a control sits inside another (segmented control options in their track, a button inside an input, a chip inside a field, tabs inside a tab bar), **the gap between them is the same on all four sides**.

- Derive the inner size from the outer one: **inner height = outer height − 2 × padding.** Never give the two their own unrelated heights (a 40px track around 30px buttons leaves 5px top and bottom but 3px at the sides).
- The outer control keeps the height of its neighbours (the search box, the sort select beside it), so the row stays aligned; the inner control is what gets resized.
- Inner radius = outer radius − padding (hack #1).
- Audit: measure the gap on every side in the browser (`getBoundingClientRect` of both elements), don't judge it by eye.

```css
.track { height: 40px; padding: 3px; border-radius: 8px; }
.track > button { height: calc(40px - 2 * 3px); border-radius: 5px; }
```

## Screen actions sit top right (strict)
Actions that act on the whole screen or window (Copy, Export, Share, Open PDF, New…) are **one group at the right edge of that screen's header**.

- Order: secondary actions first, the **one solid primary last, in the corner**.
- Icon + verb-object label ("Copy values", "Open PDF"). Wrap the group in a labelled container (`role="group"` with an `aria-label` naming the screen) so it's announced as this screen's actions.
- **Never mix actions into selectors.** Date pickers, report pickers, filters and pagination stay in their own bar; actions don't sit between them.
- **Remove duplicates** further down the screen (a card's own "Copy" that does the same as the header's).
- Actions that belong to one card (a chart's view toggle, a row's menu) stay in that card.
- Mobile: the group wraps to a full-width row under the title, buttons 40px tall, primary on the right.
- **Creating is a button, never a resident form.** "New post" or "Add member" is the primary in this group and opens a dialog or side panel; the page below is the list (UX F58). A creation form sitting permanently at the top of a list page is a finding.

## Actions sit on what they change
Behaviour: UX F57.

- **On a detail page the record comes first and largest**, with Edit and Delete on its card. History and stats follow.
- **Actions live on the row or section they change:** Renew and Pause sit in the membership row (a trailing link or row menu) and open their own flow. They are not separate sections further down, and their options appear only after the action is tapped.
- An action that needs someone's approval reads as a request ("Request a pause") and shows its Pending state on that same row (UX F55).
- Profile ends with links to Settings and Sign out; account settings (name, email, password, notification switches, delete account) live on the Settings page, not on the profile.

## Feeds get their own page
- **On a phone, the bell opens a notifications page**, not a dropdown or a home-screen section (UX F58). Back returns to where the person was.
- Group it: **items that need action first** ("For you": a class soon, a membership about to expire), then news from the organisation, newest first, each with its date. Unread items get a small dot; the full message shows on the page rather than linking elsewhere.
- The bell's dot lights only for items that need action or arrived recently, not for everything unread forever.

## The logo
- **If the product has no real logo** (an initials tile, a letter in a gradient square, a generic icon standing in for the brand), **ask the user for theirs during the audit** (SVG preferred) instead of polishing the placeholder. Initials in a user's avatar aren't a logo; leave those alone.
- Use the logo exactly as supplied: keep the proportions between the mark and the wordmark and their gap, and centre them on each other. No tile, gradient, glow or shadow behind it.
- The wordmark follows the theme's ink colour (dark in light mode, light in dark mode) when it's a single-colour wordmark. A coloured mark stays as is if it holds 3:1 on both backgrounds.
- A collapsed sidebar shows the mark only. The mark can double as the favicon.
