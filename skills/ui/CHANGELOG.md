# 21 Grams UI changelog

## 4.7.0 — 2026-11-23

Learned from building a membership and check-in app (member phone app plus a staff dashboard). The flow side of these is in UX 1.3.0 (F51–F64); this release adds the visual specs.

- **Mobile text sizes** (`rules/type.md`): on a phone, meta and secondary lines are 14, item titles and buttons 16. 12 is only for tags, nav group labels and axis ticks.
- **Font check:** the font's CSS variable goes on `<html>`, or the page can silently fall back to the system font.
- **Spacing** (`rules/spacing.md`): sections 32 apart on a phone; a big number 8 above its caption; a list's heading 24 above the list.
- **Stat cards** (`rules/charts.md`): quiet 14px regular title, the number loudest, a live state (how busy) top right. Stats for concepts the business doesn't have are removed.
- **Usage meters:** "8/12 sessions", one segment per unit for small totals, coloured green → amber → red by what's left.
- **Hero number follows the hover:** only the changed digits roll, the label takes the column's context, other columns dim.
- **Schedules are a week calendar:** times down, days across, block height = duration, now-line, past faded, full blocks with an amber edge; a date strip on phones.
- **Full-screen verdicts** (`rules/motion.md`): a fully green phone screen that closes itself after 5s with a draining Done button; a grainy glow rising from the bottom on staff screens (~3s, never blocks clicks); Simulate controls in prototypes.
- **Pass card:** tilt on hold, 3D flip to the brand logo on tap, centred in a bright sheet for scanning.
- **Rolling digits:** only changed digits animate, blur up and out, new from below.
- **Where things live** (`rules/layout.md`): creating is a top-right button opening a dialog; actions sit on the row they change; notifications are their own page with action items first; settings and sign-out reached from the profile.
- **Dark mode** (`rules/buttons.md`, `rules/elevation.md`): secondary buttons visibly lighter than their card; dark cards a small step above the page.
- **Fields respond on the next frame** (`rules/forms.md`): live data never redraws an unchanged form, lists filter after the keystroke, clocks tick coarsely.
- New AI tells in `SKILL.md`.

## 4.6.0 — 2026-11-18

Learned from a long desktop and mobile review session on an analytics product.

- **Reading width** (`rules/layout.md`): settings, forms, detail pages and pickers sit in one centred column about card width (600–720px). When content gets tight, restack it rather than widen the column.
- **Even page padding:** the space above the first heading matches the side padding, and bottom matches top.
- **Page header:** the parent's name sits beside the back arrow, and the title sits below at H2. Every section title is one size across the product, with one gap between sections. Headings that repeat the nav or a selector go.
- **Say it once:** no status tag repeating what the card already says.
- **Cards and containers:**
  - Entities are cards.
  - Peer sections get their own containers.
  - Sibling cards share height and alignment, with text clamped to 2 lines.
- **Icon rows:**
  - The inset before the icon equals the icon-to-text gap.
  - One-line rows centre the icon; multi-line rows align it to the first line.
  - The same pattern looks the same on every screen.
- **Sticky picker edges:** title, count and search stay pinned above a long picker list.
- **Tables** (`rules/tables.md`):
  - The header is the same size as the cells. *This reverses 13 vs 14.*
  - The table sits on a white surface.
  - Empty cells say "N/A".
  - Sort icons are line carets.
  - Heatmap and score cells may be centred.
- **Standalone actions look clickable** (`rules/buttons.md`): a tinted accent fill or accent colour, never bare text. Export-type actions carry their icon.
- **Signed deltas** (`rules/charts.md`): "+1.1% in 12 months", coloured by good or bad, not "Rose from X to Y".
- **Which control** (`rules/toggles.md`):
  - Binary settings are switches.
  - Filter tabs that would wrap become one dropdown on wide screens, labelled by their value.
- **AI content edge light** (`rules/motion.md`):
  - The AI card is light and accent-tinted with a thin outline and a sparkle icon.
  - On first appearance, light runs once along the border, from 0.5px at the middle of the edges to a soft 2px glow settling at opposite corners, then rests.
  - It never loops, and it doesn't run with reduced motion.
  - It is the sanctioned exception to "no gradient borders".
- **Accordion motion:** opens over 240ms and closes over 190ms, the content fades in, and the icon swaps with a blur.
- **Field details** (`rules/forms.md`):
  - No label that repeats the heading.
  - Helper text sits tight to what it explains.
  - Counters appear only near the limit.
  - Counts in headings are quiet ("Added context · 1").
  - Row actions stay faint until hover.

## 4.5.2 — 2026-11-18

- **No lonely last word** (`rules/type.md`): headings and labels get `text-wrap: balance`; paragraphs, descriptions, captions and helper text get `text-wrap: pretty`, so no single word sits alone on the last line. Long body text is never balanced.
- **Menus grow from their button** (`rules/motion.md`): the origin is the corner of the menu that touches its trigger, and it flips when the menu opens upward or leftward near an edge. Use the library's origin variable where there is one.

## 4.5.1 — 2026-11-18

- **Animated numbers are always tabular** (`rules/type.md`, `rules/motion.md`): count-ups, timers, countdowns, live prices and progress percentages use `tabular-nums`, so every digit is the same width and the number doesn't dance or push its neighbours. Count-ups run 400–800ms ease-out and jump to the final value with reduced motion.

## 4.5.0 — 2026-11-17

- **The success wave** (`rules/buttons.md`): when an action succeeds, the button turns the success colour, its label moves to the past tense with a tick ("Sending" → "Sent"), and one 2px ring leaves it, expanding about 10px and fading over ~420ms. It fires once, never loops, keeps the button's width, and is skipped with reduced motion. Replaces the faint shadow pulse in `motion.md` and craft #8, which was barely visible.

## 4.4.0 — 2026-11-17

- **New `rules/tables.md`.** Text left and numbers right with `tabular-nums`, nothing centred; hairline rows with no zebra stripes or gradient header; equal-width status tags with text, no emoji; headers that look clickable sort (click again to reverse, sensible first direction, `aria-sort`); a slight hover tint only on clickable rows.
- **Action rows** (`rules/buttons.md`): the buttons ending a card, form or dialog sit on the card's surface with no footer tray, 32px below the last field. Two actions split the row at equal width, the secondary a quiet grey fill on the left and the primary on the right.
- **Before/after review** (SKILL.md): only the divider's handle drags so both sides stay usable, and the before side shows the original as it was.
- New AI tells: footer trays around two buttons, zebra tables with centred numbers, headers that look sortable but aren't.

## 4.3.0 — 2026-11-17

- **New `rules/forms.md`: errors you can't miss.** Errors sit under their field with a danger outline, message and icon (never colour alone, never only a banner). Fields are checked on submit, then live as the person fixes them; focus moves to the first problem; server errors land on their field with a way out; a summary appears at five or more errors.
- **Excessive feedback:** every empty or invalid field shakes once on each submit (about ±6px settling over ~320ms, with a short vibration on phones). Only the invalid fields shake, never the form; no shake with reduced motion. `rules/motion.md` names it as the one exception to "no bounce".
- New AI tells: one "Oops!" banner for field errors, shaking the whole form.

## 4.2.1 — 2026-11-17

- **Equal insets for nested controls** (`rules/layout.md`, `rules/toggles.md`): a control inside another (segmented options in their track, a button in an input, chips in a field) has the same gap on all four sides. Inner height = outer height − 2 × padding, the outer control keeps its neighbours' height, and the audit measures every side. New AI tell for uneven inner padding.

## 4.2.0 — 2026-11-17

Six rules learned from reviewing a real uplift pass.

- **New `rules/layout.md`.**
  - Table-like lists of gapped row cards become one container with 1px hairline dividers; only the container is rounded, hover and selection are fills. Card grids stay cards.
  - Screen actions are one group at the right of the screen's header, secondary first and the solid primary in the corner, never mixed into date pickers or filters; duplicates below are removed.
  - When a product shows a placeholder instead of a logo (initials tile), the audit asks the user for their logo; the supplied lockup is used as is.
- **Segmented controls** (`rules/toggles.md`): no outline. The track is filled with the soft border colour (about 9% ink) and the selected option is raised; in dark mode the track sinks and the selection rises. Unselected labels must pass 4.5:1 on the track.
- **Chart hover** (`rules/charts.md`): stacked or segmented marks open a breakdown panel (one row per segment, hovered row highlighted, flips near the edge) instead of a native `title` tooltip.
- **Copy** (`rules/copy.md`): no version tags, draft names or internal shorthand on screen, and one form of address throughout.
- New AI tells for each in SKILL.md.

## 4.1.0 — 2026-11-17

- **Mono is for code only (strict).** Monospace is now limited to code, commands and copyable hashes or keys. Labels, eyebrows, badges, tags, buttons, table headers, timestamps, IDs and numbers use the UI sans, with `tabular-nums` for aligned figures. Fixes `rules/type.md`, which had sent numbers, IDs and timestamps to Geist Mono and allowed small uppercase mono labels. Added an audit search and new AI tells.

## 4.0.0 — 2026-11-17

- The family is now `21grams`, without the hyphen: the repo is `ilbognov/21grams`, the plugin and marketplace are `21grams`, and the skill appears as `21grams:ui` in Claude Code.
- Install: `npx skills add ilbognov/21grams --skill ui`, or `/plugin marketplace add ilbognov/21grams` then `/plugin install 21grams@21grams`. Old `21-grams` links redirect on GitHub.

## 3.0.0 — 2026-11-17

- Shorter names: the skill is now `ui` (`npx skills add ilbognov/21-grams --skill ui`). In Claude Code, one `21-grams` plugin holds every scale, so this one appears as `21-grams:ui`.
- Layout: `skills/ui/` holds the skill, README and changelog. Tags are `ui@<version>`.

## 2.0.0 — 2026-11-17

- **Renamed to 21 Grams UI** (`21-grams-ui`). The repo is now the home of the 21 Grams family; a UX package will follow.
- New layout: `plugins/21-grams-ui/` holds the plugin, its skill, README and changelog. The repo root is the index of all scales; the Claude Code marketplace is still `21-grams`.
- Release tags are now per scale: `21-grams-ui@2.0.0`. Earlier tags `v1.0.0`–`v1.3.0` belong to this scale.
- Install changes: `npx skills add ilbognov/21-grams --skill 21-grams-ui`, or `/plugin install 21-grams-ui@21-grams`.

## 1.3.0 — 2026-11-17

- New `references/unslop.md`: 20 composition and content rules for unslopping AI designs, cross-referenced to the existing rules where they overlap.
- More AI tells in SKILL.md: filler badges, redundant eyebrows, random italic or mono words, abstract hero art, equal-weight feature grids, vague headlines, glowing borders, emoji icons.

## 1.2.0 — 2026-11-17

- New `references/typography.md`: 10 typography hacks (reserved bold width, text-box trim, underline offset, superscript spacing, fluid display type, small-caps acronyms, curly quotes, middle truncation, auto hyphenation, line-clamped titles), each with code and audit checks.
- `rules/type.md`: fluid `clamp()` allowed for display headings only; UI text stays on the fixed scale.

## 1.1.0 — 2026-11-17

- New `rules/icons.md`: one icon style (line, solid or duotone), never mixed within a menu, nav, toolbar, list or card, and unchanged across states. One library, one stroke width, one size per group.

## 1.0.1 — 2026-11-17

- Replaced project-specific examples in the type, chart and toggle rules with neutral ones.

## 1.0.0 — 2026-11-17

First public release.

- Rule zero: every fix goes through the project's own components and tokens; no new UI kits or dependencies.
- House style across eight areas (radius, buttons, motion, type, spacing, colour, elevation, copy) plus charts and toggles.
- 20 UX & animation principles, 10 design hacks and 20 animation crafts, each with apply and audit notes.
- Workflow: inventory → audit → approve → tokens → components → screens → verify → report.
