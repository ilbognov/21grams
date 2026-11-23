# 3g · Motion: smooth, from the trigger, no bounce

Everyday UI enters from its trigger with a slight scale and a soft landing, leaves faster than it came, and never bounces. Full detail for each technique is in `references/animation-craft.md`. Use the project's animation library if it has one; otherwise CSS transitions.

## Tokens
| Token | Value | Use |
|---|---|---|
| `--ease-out` | `cubic-bezier(.2, 0, 0, 1)` | all entrances |
| `--ease-in` | `cubic-bezier(.4, 0, 1, 1)` | all exits |
| `--ease-move` | `cubic-bezier(.4, 0, .2, 1)` | moving from A to B on screen |
| `--dur-press` | 150ms | press scale |
| `--dur-fast` | 120ms | hover colour, icon swaps |
| `--dur-menu` | 220ms | menus, dropdowns, popovers, tooltips (150–250 range) |
| `--dur-menu-exit` | 175ms | ≈ 80% of `--dur-menu` |
| `--dur-panel` | 240ms | drawers, sheets, dialogs, accordions |
| `--dur-panel-exit` | 190ms | ≈ 80% of `--dur-panel` |
| `--stagger` | 30ms | list rows on open, capped at ~6 rows |
| `--trail` | 50ms | secondary details settling after the body |

## Recipes
- **Menu / popover / dropdown:** never appears out of thin air. `transform-origin` at the trigger: the corner or edge of the menu that touches the button it came from (top right for a menu under a right-aligned button). **When the menu flips** to open upward or leftward near the screen edge, the origin flips with it. Use the library's variable where it has one (Radix `--radix-*-content-transform-origin`, Floating UI placement). Enter from `opacity 0; scale(.95)` over `--dur-menu --ease-out`, with rows staggered 30ms. Exit back toward the trigger: `scale(.95)` + opacity over `--dur-menu-exit --ease-in`. **No overshoot.**
- **Dialog:** scrim fades over `--dur-panel`. Dialog enters from `scale(.96)` + opacity with `--ease-out`, no overshoot. Exit over `--dur-panel-exit`.
- **Toast:** enters 8px from its edge with `--ease-out`. Contents trail by 50ms.
- **Button press:** `scale(.97)` over `--dur-press` plus the colour step (see buttons.md). Hover: colour only.
- **Toggle and slider knob:** ~12% area-preserving stretch while travelling (`scaleX 1.12 / scaleY .89`).
- **State swaps (Save → Saved, tabs):** old and new overlap, with no blank frame between them. Icons: scale + opacity + `blur(4px)`.
- **Segmented controls and tabs:** the indicator moves with `--ease-move`. The active label colour is revealed by a clip or mask that travels with it.
- **Animated numbers:** always `tabular-nums` so the digits don't dance (`type.md`). Count up over 400–800ms ease-out, and with reduced motion jump straight to the final value.
- **Success:** one wave: a 2px ring in the success colour leaves the button and fades about 10px out over ~420ms, as the label turns to "Sent". Never loop. Spec in `buttons.md`.
- **Error:** each invalid field shakes once on submit (±6px settling, ~320ms), never the whole form, always with the inline message, outline and icon. Full spec in `forms.md`.
- **AI content (summaries, suggestions):** marked by an **edge light, not a dark or gradient block.** The card is a light accent tint with a thin accent outline and the product's sparkle icon by the title. When it first appears, light runs **once** along the border: it starts as a 0.5px line from the middle of the top and bottom edges, travels around the rounded corners, grows to ~2px with a widening soft blur in a blue–cyan–violet hue, and settles at the top-right and bottom-left corners, then fades back to the plain outline (~2.5–3s in all). Never loops, never on every render, none with reduced motion. Draw it with a masked `conic-gradient` border (`@property` angle) so it follows the radius.
- **Accordion:** height opens over `--dur-panel` ease-out and closes over `--dur-panel-exit`; the content fades in with a 4px drop; the +/− or chevron swaps with the blur crossfade. Reduced motion: fade only.
- **Full-screen verdict (check-in, scan, payment result):** behaviour in UX F52.
  - **On the person's own phone:** the whole screen, status bar included, fills with a success green dark enough for white text (≥ 4.5:1), with a large white tick and one line of result ("Checked in · 18:04 · 8/12 sessions") at 22–28px. It closes by itself after 5s. Its button ("Done") shows the countdown as its fill draining left to right; this is a timer, so it runs linear. Tapping anywhere closes it sooner. Failure is the same in the error red, with the reason and the fix.
  - **On a staff screen that must stay usable:** the verdict is a glow, not a cover. A gradient rises from the bottom edge across the whole viewport (sidebar included), green for valid and red for refused. Over a soft gradient sits a fine grain layer in the same hue, slightly lighter, densest at the bottom and thinning to nothing towards the top, like sand. About 3s in all (300ms in, hold, slow fade out), `pointer-events: none` so work carries on. No glow when nothing was decided (the person is already inside).
  - Prototypes give each outcome a **Simulate** control (valid, expired, unknown) that runs through the real flow (UX F64).
  - Reduced motion: opacity only, no rise.
- **Pass card (a card people show to be scanned):**
  - Press and hold tilts it towards the finger, up to about 8°, with `perspective: 800px`, tracking the pointer 1:1 while held and settling back with `--ease-out` on release.
  - A tap flips it 180° around the Y axis (~450ms, `--ease-move`, `backface-visibility: hidden`) to its back: the brand's logo.
  - The sheet that shows it for scanning is tall enough to put the card in the middle of the screen, and asks for full screen brightness while open where the platform allows, restoring it on close.
  - Reduced motion: no tilt, and the flip becomes a crossfade.
- **Rolling digits:** when a number changes in place (a hero number following the hover, a live count), only the digits that change animate. The old digit blurs and leaves upward while the new one enters from below, ~200ms `--ease-out`, each changed digit ~30ms after the one to its left. Digits that stay the same don't move. Always `tabular-nums`. Reduced motion: a crossfade.
- **Travel (add to cart, move file):** an arc (~32px lift), `--ease-move`.
- **Card → detail:** the same element expands (shared `layoutId` / view transition). Never a disconnected replacement.
- **Drag:** 1:1 with the pointer, no transition while held. Rubber band past bounds, then settle with `--ease-out` on release.

## Limits
- **No spring overshoot or wobble on everyday UI** (menus, popovers, dialogs, panels, tabs, toasts). Bounce is allowed only for rare, playful moments the user asks for. The one exception is the error shake on an invalid field (`forms.md`).
- No motion on high-frequency interactions (keyboard navigation, list and palette highlight, tabs in tools): instant, or 60ms opacity at most (principle #20).
- No fade-up-on-scroll and no page-load stagger for content. The 30ms stagger is only for lists inside a surface that just opened.
- No hover scale on cards or buttons.
- Never `scale(0)` entrances. Never centre-origin popovers.
- Animate only `transform`, `opacity`, `filter` and `clip-path`.
- Nothing user-triggered takes longer than 300ms to settle. The exceptions are the pass-card flip and a verdict's hold, which are moments to look at rather than transitions to wait for.
- `prefers-reduced-motion: reduce`: remove translate, scale, stretch and stagger. Keep opacity at `--dur-fast`.

```css
@media (prefers-reduced-motion: reduce) {
  :root { --dur-menu: 120ms; --dur-menu-exit: 100ms; --dur-panel: 120ms; --dur-panel-exit: 100ms; --stagger: 0ms; --trail: 0ms; }
  * { --motion-scale: 1; --motion-distance: 0px; }
}
```
