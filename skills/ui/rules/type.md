# 4g · Type: few sizes, tight headings

House default. When the project has its own system, express this through its components and tokens (SKILL.md, rule zero).

## Families
- **The project's fonts come first.** Keep its brand typefaces and apply the scale, weights and tracking below.
- Default when the project has none: **Geist** for all UI text (`"Geist", ui-sans-serif, system-ui, -apple-system, "Segoe UI", sans-serif`). **Geist Mono** only for code (see below).
- Use `font-variant-numeric: tabular-nums` in the UI sans wherever digits line up: tables, stats, prices, timers, chart axes. Figures do not need a mono font to align.
- **Numbers that change on screen are always tabular (strict).** Count-ups, timers, countdowns, live prices, progress percentages, seat counts, odometer rolls: proportional digits are different widths, so the number dances and pushes its neighbours as it ticks. Tabular figures give every digit the same width and lock it in place. Right-align (or fix the width of) the container so a new digit is added on the left without shifting the rest.

## Mono is for code, never for labels (strict)
Mono labels are one of the most common tells of AI-built UI. Monospace is allowed only for text a person would read or copy as code:
- code blocks and inline code
- terminal commands and CLI output
- hashes, API keys, tokens and commit SHAs that a user copies

Everything else uses the UI sans: labels, eyebrows, section headers, tags, badges, pills, buttons, tabs, nav items, table headers, form labels, metadata, timestamps, dates, IDs shown as reference (order #4821), numbers, stats, prices and chart axes. Uppercase tracked mono "tech" labels (`STATUS`, `// SECTION 01`, `[ BETA ]`) are always removed.

Audit: search for `font-mono`, `monospace`, `--font-mono`, `ui-monospace`, `Mono` in font stacks, and `<code>`/`<kbd>` used for decoration. Each hit that is not code becomes the sans (with `tabular-nums` when it holds figures). When the project's own design system styles labels in mono, flag it as a design-system conflict in the audit rather than overriding it silently (rule zero).

## Scale (use only these)
| Token | Size / line-height | Weight | Tracking | Use |
|---|---|---|---|---|
| `--text-xs` | 12 / 16 | 400–500 | 0 | meta, captions, table headers |
| `--text-sm` | 14 / 22 (1.55) | 400 | 0 | body, controls |
| `--text-md` | 16 / 24 | 500 | −0.006em | emphasised body, section labels |
| `--text-lg` | 22 / 28 | 600 | −0.022em | panel and page titles |
| `--text-xl` | 28 / 32 | 600 | −0.025em | page hero titles (rare) |

At most **four sizes per screen**. Weights are only 400, 500 and 600. Large display headings (28px and up) may scale fluidly with `clamp()` (see `references/typography.md` #5); UI text stays on this fixed scale.

**Check that the font actually loads.** With `next/font` (or any font exposed as a CSS variable) and Tailwind, put the font's variable class on `<html>`, where the theme's `font-family` reads it. On `<body>` it often isn't picked up and the page silently falls back to the system font, so a whole review is done against the wrong face. Confirm with the computed `font-family` in the browser before judging type.

The finer details (reserved bold width, text-box trim, underline offset, superscripts, small caps, punctuation, truncation, hyphenation, line clamping) are in `references/typography.md`.

## Mobile headings
On phone layouts (< 768px), headings go up one step so they read at arm's length:

| Heading | Desktop | Mobile |
|---|---|---|
| Section heading (e.g. "Recent activity") | 16 / 24, 600 | **18 / 24, 600**, −0.015em |
| Card heading (e.g. "Top issues", "Team members") | 14 / 20, 600 | **16 / 22, 600** |
| Page title | 28 / 32 | 22 / 28 (when shown in the body; a header title stays 16) |

## Mobile text sizes (strict)
On a phone, 12px is too small for anything people need to read. Body stays 14, and:

| Text | Desktop | Mobile |
|---|---|---|
| Meta and secondary lines (instructor · room, "60 min · Done", a payment date, a delta line, the caption under a stat) | 12 | **14** |
| Card and list-item titles, month headers, post titles | 14 | **16** |
| Buttons | 14 | **16** (40px tall) |

12px stays only for small labels that are glanced at, not read: tags, nav group labels, axis ticks, tab-bar labels, day names in a date strip. A mobile screen then uses 18 / 16 / 14 / 12, which is still four sizes. The usual audit finding on a phone is a row of 12px secondary lines; move them all to 14 at once rather than one at a time.

## Secondary text
- Secondary: ink at about 70% (`--ink-2`). Tertiary and meta: about 50% (`--ink-3`). Both are mixed from the ink colour, never Tailwind `gray-500`.
- Must still pass 4.5:1 for body sizes (3:1 for 18px+ or 14px/600+).

## Rules
- **No lonely last word (strict).** Headings, titles, button and card labels get `text-wrap: balance` so their lines come out even. Paragraphs, card descriptions, captions, helper text and empty-state copy get `text-wrap: pretty`, which only fixes the last line, so one word never sits alone on it. Don't balance long body text; it makes every line short. Body is at most about 65ch wide.

```css
h1, h2, h3, h4, .title { text-wrap: balance; }
p, li, figcaption, .description, .hint { text-wrap: pretty; }
```
- Sentence case everywhere. Avoid uppercase labels; if the project already has them, keep them in the UI sans at 12px with +0.04em tracking, never mono.
- Long numbers are chunked (principle #16): `4532 0151 1283 0366`.

## Never
Mono labels, eyebrows, badges or numbers (mono is for code only), gradient text, a 30px+ bold headline in product UI, wide-tracked bold coloured eyebrows, Inter at default tracking as an unconsidered default, more than one display face.
