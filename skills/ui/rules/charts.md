# Charts: line, column, horizontal bar

Use the project's chart library and its configuration (Recharts, visx, Chart.js, ECharts, hand-rolled SVG…); never add a new one. If a data-visualisation skill is installed, load it too.

## Colour
- **Series colours never borrow the status colours.** Green, amber and red mean healthy, watch and at risk. A series coloured green reads as "good". Use a categorical palette that starts from the brand colour, for example `#0066f5 · #eb6834 · #1baf7a` on white.
- **One measure, one hue.** A ranked bar chart uses the brand colour for the bar the story is about and a lighter step (`#86b6ef`) for the rest. Never give each bar its own colour.
- **Check every categorical palette** for colour-blind separation and contrast against the surface (a palette validator or a CVD simulator). A colour under 3:1 against the surface needs direct labels or a table view.
- Text never wears the series colour. Values and labels use the ink colours, and identity comes from a line key or dot beside the text.

## Marks
| Mark | Spec |
|---|---|
| Line | 2px, round join. End dot r 4 with a 2px white ring |
| Column / bar | ≤ 24px thick, 4px rounded data end, square at the baseline |
| Area | series hue at 10% |
| Grid | 1px solid hairline `rgb(7 29 73 / .08)`; baseline `/ .22` |
| Ticks | 3–5 clean values (`0%, 0.2%, 0.4%…`, `0, 1,000, 2,000`), 12px muted, tabular figures |

## Labels
- Label line ends directly with the latest value and the series name. With ≤ 4 series, keep a small line-key legend too.
- Columns: label only the peak and the latest value. Horizontal bars: value at every tip.
- Month axis: every 2nd month (3rd on phones) plus the latest. Drop a regular label that would crowd the latest.
- No rotated axis titles. The card title names the measure, and a one-line subtitle states the takeaway ("Error rate fell from 0.8% to 0.4% this year.").
- Convert awkward units into readable ones: 0.00459% per order becomes **4.59 per 100,000 orders**. Keep the exact value in the tooltip.

## Changes are signed deltas, not sentences
Show a change as a **signed number with its period**: "+1.1% in 12 months", "−240 orders vs last week". Not "Rose from 0.6% to 1.7%".

- Colour the delta by whether the change is **good or bad for this measure** (a falling error rate is green), not by its sign. Always keep the sign and an arrow or word, so colour is never the only signal.
- The from and to values can live in the tooltip or a second muted line.
- Delta text uses the status ink that passes 4.5:1, with `tabular-nums`.

## Stat cards
- **The title is quiet:** 14px, regular weight, secondary ink ("Check-ins per hour"), not a bold heading. The number underneath is the loudest thing on the card (22–28, 600, `tabular-nums`), with its caption 8px below (`spacing.md`).
- **A live state goes in the top-right corner** of the card it describes: a small meter with a word ("Quiet", "Busy", "Packed") for how busy the place is now, beside the current count. It uses the status colours with the word, never colour alone.
- **Every stat is a real concept for this business** (behaviour: UX F59). A card that is always zero because the thing doesn't exist (debts where members have either paid or not) is removed, not restyled.

## Usage meters: used of total
For anything with a limit (sessions on a pass, seats, credits). Behaviour: UX F51.

- **Text is used of total:** "8/12 sessions", tabular figures, not "12 sessions" or "4 left".
- **Small totals (up to about 20) get one segment per unit**, so people can count them: 4px tall, radius 2, 2px gaps, full width of the card. Bigger totals use one continuous bar.
- **The filled segments are coloured by what's left:** green while there is plenty (up to about 60% used), amber when it's getting low, red when it's used up or over the limit. The colour change always comes with the text, never alone.
- Unlimited plans show the plan's name and no bar. The same count and colours appear everywhere the limit is shown (the card, the profile, the staff view).

## One scale per chart
- **Never plot two measures on one axis or on a hidden second axis.** Orders and revenue become **two charts that share the x-axis** (small multiples), each with its own scale, aligned so the months line up.

## Interaction
- Line charts: a crosshair snaps to the nearest month, and one tooltip lists every series (values lead, names follow, line keys).
- Columns and bars: the mark is the target, lifting slightly on hover. Rows in a horizontal bar chart get a soft hover wash.
- **Segmented marks get a breakdown panel, not a native tooltip.** A stacked or segmented bar (ranges, zones, a budget split) opens a small floating panel on hover instead of the browser's `title` text:
  - header: what the bar is (the entity's name) with its context underneath (date range, count of segments);
  - one row per segment **in the same order the product uses elsewhere**, each with a colour key, name, range or definition, a small proportional bar and the value (tabular figures);
  - the row under the pointer is highlighted as the pointer moves along the bar;
  - totals only when they add information; no verdicts or targets the product doesn't make;
  - it opens below the mark and flips above near the bottom of the viewport, never runs off an edge, grows from the mark (220ms in / 175ms out, opacity only with reduced motion) and closes on leave, scroll or click;
  - touch screens skip the panel; tapping does what clicking did.
- **When a column chart has a hero number above it** ("6 people in now" over check-ins per hour), hovering a column swaps that number for the column's value, and the label beside it changes to the column's context ("14 check-ins · 18:00–19:00"). Only the digits that change roll (`motion.md`, rolling digits). The hovered column stays full colour and the rest dim. On leave, the number goes back to its live value and only the current column ("Now") is highlighted.
- Linked charts share hover: hovering a month in one highlights it in the other, with a single tooltip.
- Charts are focusable. Arrow keys move the crosshair and Esc clears it.
- Every chart offers a **Chart / Table** toggle (segmented control, see toggles.md) with the same numbers.

## Motion
- Lines draw in over 600ms ease-out, each series 50ms after the last.
- Columns grow from the baseline and horizontal bars from the left, 400ms ease-out, 30ms apart.
- Run the draw-in on load and when switching back from Table. Never animate on every hover. Reduced motion means no draw-in.

## Schedules are a week calendar
Classes, bookings and shifts show as a week, not a list (behaviour: UX F61).

- **Times run down the left, one column per day** for the next 7 days. Day headers stay pinned while the grid scrolls; open the grid scrolled to the start of the working day, with the rest of the day reachable by scrolling.
- **Today is marked** on its date (a filled circle or the accent), and a **thin red line shows the current time** across today's column.
- **Each block's height is its duration.** Blocks that overlap sit side by side. A block shows the start time and how full it is ("12/12") on the first line, the name on the second, then the instructor and room (or "+2 waiting" when there is a waiting list) in secondary ink.
- **State is shown on the block, quietly:** past blocks faded to about 50%, the one in progress with a small green dot, full ones with a 3px amber edge on the left.
- Clicking a block opens its detail in a side panel, keeping the calendar in place. On a phone, the week becomes a horizontal date strip (edges fade, today scrolled into view) above that day's blocks.
