---
name: ui
description: Uplift UI that was built by AI so it stops looking AI-generated and follows proven UX and motion principles, using the project's own components and tokens. Use when the user asks to uplift, polish, de-AI, refine or "make less AI-looking" an existing screen, component or frontend, asks for "21 grams UI" or "21 grams" (or "twenty-one grams"), or wants a UI audited against the house style, the 20 UX & animation principles (squash & stretch, anticipation, staging, easing, snappy timing, Fitts's, Hick's, Miller's, Doherty, Postel's, Jakob's law, frequency of use), the 10 design hacks (concentric radius, alpha borders, OKLCH, dvh and the rest) or the 20 animation crafts.
---

# 21 Grams UI

A pass over UI that already exists. 21 Grams UI (the UI package of the 21 Grams family) doesn't redesign the product and doesn't bring its own UI kit. It removes the tells of AI-built UI and applies a fixed set of rules **through the components and tokens the project already has**, so the result looks considered, feels fast and still belongs to the product.

## Rule zero: use the project's own components

Every change goes through what the project already uses. 21 Grams UI never builds a parallel set of components.

1. **Take an inventory before touching anything.** Note the design tokens or theme (CSS variables, Tailwind config, theme files), the component library (shadcn/ui, Radix, MUI, Chakra, an in-house kit, a client design system), the icon set, the chart library and the animation library. Record what each shared component is called and where it lives.
2. **Fix things where they live.** A button rule goes into the project's `Button` (a token, a variant, a prop or its styles), never into a one-off copy on a single screen. A colour or radius rule goes into the token, not into hard-coded values.
3. **Never add a component when one exists for the job,** and never add a dependency (UI kit, icon set, chart or animation library) to get a 21 Grams UI effect. Use what is installed. Without an animation library, use CSS transitions.
4. **When a piece is genuinely missing** (no segmented control, no switch), build it from the project's existing primitives and tokens, following its file layout and naming. Say so in the report.
5. **The house-style values are defaults for gaps only.** `rules/` and `tokens/tokens.css` give values for what the project hasn't decided. Map them onto the project's tokens. Never paste `tokens.css` alongside an existing system.
6. **Brand stays the project's.** Brand colours, fonts, logos, icon style and voice are never replaced. 21 Grams UI changes how they are used (contrast, hierarchy, spacing, motion), not what they are.

**Precedence:** the user's words, then the project's design system and brand, then the 21 Grams UI house style. The principles, hacks and animation crafts apply everywhere, expressed in the project's own components.

## What's inside

1. **House style.** Eight areas in `rules/`: `radius.md` (12/8/4 nested), `buttons.md` (36px, .97 press), `motion.md` (smooth, from the trigger, no bounce), `type.md` (tight, few sizes), `spacing.md` (grouped 4pt), `colour.md` (one accent, AA), `elevation.md` (tonal fills), `copy.md` (plain and helpful). Plus six component files: `icons.md` (one style, line, solid or duotone, never mixed), `charts.md` (line, column and horizontal bars, stat cards, usage meters, week calendars), `toggles.md` (switch and segmented control) `layout.md` (reading width, page header, cards, row lists as one table, equal insets for nested controls, screen actions top right, actions on what they change, notification pages, the logo) `forms.md` (inline errors, focus, field shake) and `tables.md` (text left, numbers right, hairlines, sortable headers). Default values are in `tokens/tokens.css`.
2. **The 20 principles.** UX and animation principles in `references/principles.md`.
3. **The 10 design hacks.** CSS-level craft details in `references/design-hacks.md`.
4. **The 20 animation crafts.** Implementation-level motion rules (origins, durations, stagger, press, drag, shared layout) in `references/animation-craft.md`.
5. **The 10 typography hacks.** Reserved bold width, text-box trim, underline offset, superscript spacing, fluid display type, small-caps acronyms, curly quotes, middle truncation, auto hyphenation and line-clamped titles, in `references/typography.md`.
6. **The 20 unslop rules.** Composition and content tells (filler badges, redundant labels, random italics, decorative mono, abstract hero art, equal-weight features, vague headlines, glows, optical alignment, loading states) in `references/unslop.md`.

If a data-visualisation skill is installed, load it as well whenever a chart is involved.

## Workflow

1. **Take the inventory** (rule zero). If the project has no design system at all, say so and use the house-style defaults.
2. **Audit before changing anything.** Go through the screen or component and list findings grouped by area (radius … copy), principle number, hack number and craft number. Use the checklists at the end of `references/principles.md`, `references/design-hacks.md`, `references/animation-craft.md`, `references/typography.md`, `references/unslop.md` and `rules/icons.md`. Each finding gets the file and line, what is wrong, the fix, and **which existing component or token the fix goes into**. Flag every place where a 21 Grams UI rule conflicts with the project's design system, so the user can decide which wins. **If the product shows a placeholder instead of a logo** (initials tile, letter in a gradient square), ask the user for their logo here (`rules/layout.md`).
3. **Show the audit to the user** as a short list and ask before applying broad changes. Small, obvious fixes in the requested scope can go straight in.
4. **Apply the fixes** in this order: tokens → shared components → screens. Keep diffs scoped to what was audited and in the project's own conventions (formatting, lint, naming).
5. **Verify in the browser.** Before and after screenshots of each changed screen. Check hover, press, focus, loading, error, both themes and reduced motion. Measure button and text contrast; don't eyeball it. For motion, record the before and after if possible. A before/after page with a draggable divider and working interactions on both sides is the clearest way to review an uplift. **Only the divider's handle drags** (keep it keyboard-operable with a range input), so clicks and hovers reach the UI on both sides. The before side shows the original honestly: never add bad behaviour it didn't have.
6. **Report** what changed per area, principle, hack and craft, which components and tokens were touched, and anything left undone.

## House style at a glance (defaults for gaps)

- Radius 12 containers / 8 controls / 4 small parts, nested as outer − padding. No pills except tags and toggles.
- Nested controls (segmented options, a button inside an input, chips in a field) have the same inset on all four sides: inner height = outer height − 2 × padding, and the outer control matches its neighbours' height.
- Buttons 36px (32 compact, 40 prominent), radius 8, 14/500, one solid primary, one primary per view, hover = colour step only, press = colour step + `scale(.97)` 150ms, loading keeps width.
- Motion: no bounce on everyday UI. Menus 220ms in / 175ms out from `scale(.95)` at the trigger, panels 240 / 190, entrances ease-out, exits ease-in (~80% of the entrance), list rows staggered 30ms, frequent interactions instant.
- Type: the project's fonts (Geist when there are none). Mono is for code only, never labels, eyebrows, badges, timestamps or numbers (`tabular-nums` in the sans aligns figures, and any number that animates or ticks is always tabular so its digits don't dance). Sizes 12/14/16/22/28, weights 400/500/600, headings −0.022em, at most four sizes per screen. No lonely last word: `text-wrap: balance` on headings, `pretty` on paragraphs and captions. On mobile, headings go up one step: section 18, card 16. On a phone, meta and secondary lines are 14 (never 12), item titles and buttons 16; 12 is only for tags, nav group labels and axis ticks. Check the font variable sits on `<html>` so the real font loads.
- Layout: settings, forms, detail pages and pickers sit in one centred column about card width (600–720px). Top padding matches the side padding. Detail pages put the parent's name beside the back arrow and the title below at H2. Every section title is one size across the product, with one gap between sections. Say each fact once. Entities are cards; peer sections get their own containers; sibling cards share height and alignment, text clamped to 2 lines. In icon rows, the inset before the icon equals the icon-to-text gap.
- Lists: a table-like list of gapped row cards becomes one container with 1px hairline dividers; only the container is rounded. Card grids stay cards.
- Screen actions: one group at the right of the screen's header, secondary first, the solid primary in the corner. Never mixed into date pickers or filters; duplicates below are removed.
- Controls: binary settings are switches. Filter tabs that would wrap become one dropdown on wide screens. Standalone actions (Export, View more) get a tinted accent fill or accent colour, never bare text.
- Segmented controls: no outline. The track is filled with the soft border colour and the selected option is raised (surface + small shadow); in dark the track sinks and the selection rises.
- Segmented chart marks: hover opens a breakdown panel (one row per segment, hovered row highlighted), never a native `title` tooltip.
- Chat send on mobile is an icon-only 44×44 paper-plane button with `aria-label="Send"`.
- Spacing: 4pt scale. Tighter inside groups than between them (4 / 6 / 16 / 24–32 / 48; sections 32 apart on a phone). A big number sits 8 above its caption. Select chevron 12px from the right, padding-right 36px.
- Colour: one accent (actions, focus, selection), status colours separate, **button text ≥ 4.5:1 in both themes** with `--on-accent` per theme.
- Elevation: resting surfaces are a fill step with no border or shadow. Only floating layers get a ring and shadow. Dark mode is lighter per layer.
- **Icons: one style per product, line, solid or duotone, and never mixed in a menu, nav, toolbar, list or card. Selected states change colour, not icon style. One icon library, one stroke width, one size per group.**
- Action rows ending a card, form or dialog: no footer tray, 32px above the row, two buttons of equal width (secondary as a quiet grey fill on the left, primary on the right).
- Tables: text left, numbers right with `tabular-nums`, hairline rows (no zebra, no gradient header), header the same size as the cells (weight and ink tell them apart), "N/A" for empty cells, line-caret sort icons, equal-width status tags, headers that look clickable sort (with `aria-sort`), subtle row hover only on clickable rows.
- Form errors: under the field, with a danger outline, message and icon; checked on submit then live as the person fixes it; focus moves to the first problem; **each invalid field shakes once on submit** (not the form, not with reduced motion). Server errors land on their field with a way out.
- Stats and limits: stat titles are 14 regular in secondary ink with the number loudest below and a live state (how busy) top right. Limits read "8/12 sessions" with one segment per unit, coloured green → amber → red by what's left. Stats for concepts the business doesn't have are removed.
- Hero numbers over a column chart follow the hover: only the changed digits roll, the label takes the column's context, other columns dim, and it returns to the live value on leave.
- Schedules: a week calendar (times down, days across, block height = duration, red now-line, past faded, full with an amber edge); a date strip on phones.
- Verdicts (check-in, scan): the person's phone turns fully green with a tick and closes itself after 5s with a draining Done button; staff screens get a grainy glow rising from the bottom for ~3s that doesn't block clicks. Prototypes can simulate each outcome.
- Pass cards tilt on hold, flip in 3D to the brand logo on tap, and sit centred in a bright sheet for scanning.
- Where things live: creating is a top-right button that opens a dialog, actions sit on the row they change (Renew and Pause on the membership), notifications are their own page with action items first.
- Dark mode: secondary buttons are visibly lighter than the card they sit on; dark cards stay a small step above the page (#1F1F1F on near-black, not #2A2A2A).
- Speed: fields respond within a frame. Live data never redraws a form that hasn't changed, long lists filter after the keystroke, clocks tick coarsely.
- Data: changes are signed deltas with their period ("+1.1% in 12 months"), coloured by good or bad, never "Rose from X to Y" sentences.
- AI content: a light accent-tinted card with a thin outline and the sparkle icon. An edge light runs once around its border on first appearance, then rests. Never a dark or gradient block.
- Copy: verb + object buttons, errors with cause and fix, sentence case, no emoji, no hype words, no version tags or internal jargon on screen, one form of address.

## Non-negotiables (from the 20 principles)

- User-triggered UI motion is 120–300ms, and exits are about 80% of the entrance. Never `linear` for movement.
- Easing matches the direction: enter ease-out, exit ease-in, A→B on screen ease-in-out. No overshoot on everyday UI.
- High-frequency interactions (keyboard nav, list highlight, tabs in tools) are instant.
- Every input is acknowledged in under 100ms. Use optimistic UI for saves. Show progress past 400ms.
- Hit areas are at least 44×44 on touch and 32×32 on dense desktop, even when the icon is smaller.
- One focus and one primary action per view. Dim the context when something takes focus.
- Long numbers are chunked. Inputs accept messy formats and echo back the clean value.
- Standard placement and icons unless there's a reason not to.
- Every component state is designed: idle, hover, pressed, loading, success, error, disabled.
- Rejected input gets excessive feedback: the invalid field shakes once, on top of the message, outline and icon.
- `prefers-reduced-motion`: remove movement, scale and overshoot, keep a brief opacity change.

## Non-negotiables (from the 10 hacks)

- Nested radius: inner = outer − padding.
- Borders are alpha (`rgb(0 0 0 / .12)`), never solid grey hex on varied surfaces.
- Palettes and gradients in OKLCH (`in oklch` on gradients).
- Icon stroke matches the weight of adjacent text.
- Horizontal scrollers fade at the edges with a mask.
- Icon swaps crossfade with `filter: blur(4px)`.
- Dark mode: each higher layer is lighter (page < card < menu).
- Mobile full-height: `dvh`/`svh`, never bare `100vh`.
- White-background product shots on tinted cards: `mix-blend-mode: multiply`.

## Non-negotiables (from the 10 typography hacks)

- Bold-on-hover or bold-on-select never shifts layout (reserve the bold width).
- Single-line labels in buttons and badges are optically centred (`text-box-trim`).
- Link underlines clear descenders (`text-underline-offset: 0.2em`). Superscripts don't break line rhythm.
- Real punctuation in copy: curly quotes, apostrophes, en dashes, `…`.
- Names that differ at the end are middle-truncated. Card titles in grids are clamped to the same line count.

## Non-negotiables (from the 20 animation crafts)

- Popovers and menus grow out of their trigger (`transform-origin` at the trigger), start at `scale(.95)`, never `scale(0)`, and exit back into the trigger. The origin flips when the menu opens upward or leftward.
- Old and new states overlap. There is never a blank frame between Save and Saved.
- Drags track the pointer 1:1 with no transition while held, and rubber-band past their bounds.
- Card → detail expands the same element (shared `layoutId` / view transition), never a disconnected replacement.
- Segmented controls and tabs reveal the active label with a mask that travels with the indicator.
- Moving knobs stretch about 12% (area-preserving). Success turns the button green and sends one thin ring out from it, once (`buttons.md`).

## AI tells to remove

Mixed icon styles (a solid house beside an outline folder, an outline icon that turns solid when selected), two icon libraries on one screen, emoji used as icons, "NEW" filler pills above headlines, eyebrows that repeat the heading, one random italic or mono word in a headline, mono labels, eyebrows, badges, timestamps or numbers ("tech" uppercase mono like `// 01 STATUS`), glossy 3D orbs instead of the real product, initials-in-a-gradient-tile placeholder logos, buttons in a grey footer tray, zebra-striped tables with centred numbers and headers that look sortable but aren't, form errors as one "Oops!" banner or a shaking form instead of messages on each field, table rows drawn as separate floating cards with gaps, actions scattered among date pickers and filters, outlined segmented controls, inner controls with uneven padding (more at the top and bottom than the sides), browser `title` tooltips on chart segments, version tags like "V7 demo" in the UI, rows of equal feature cards, "X, meet Y." headlines, glowing gradient borders that stay on (the one-time AI edge light is the exception), AI summaries as dark navy or gradient blocks, settings stretched across a wide screen, small bold page titles, a status tag that repeats what the card already says, bare-text actions, filter tabs wrapping onto three rows, "Rose from 0.6% to 1.7%" sentences, light/dark as an icon button, indigo-to-violet gradients, gradient text, coloured glow shadows, the same 16px radius on everything (inner radius equal to outer), pill buttons beside rounded inputs, hover scale-up on cards and buttons, 300ms ease-in-out on everything, fade-up on page load, uniform `p-6 gap-6`, cards inside cards, shadow plus border plus radius on every block, grey-500 for all secondary text, emoji in headings, and copy like "Unlock", "Supercharge", "Seamless" or "Oops!". Also: 12px secondary lines on a phone, a bold stat title that outshouts its number, a usage count with no total ("12 sessions"), a schedule as a flat list, a small toast for the result the whole flow is for, a creation form parked on top of a list, secondary buttons that vanish on dark cards, and fields that lag because live data redraws the page.

## Credits

The principles, hacks and animation crafts are paraphrased and extended from five short-form design videos: "20 Principles of UX & Animation", "10 Niche Design Hacks", "20 Ways to Make Beautiful AI Animations", "10 Niche Typography Hacks" and "20 Ways to Unslop AI Designs". See the README for credits.
