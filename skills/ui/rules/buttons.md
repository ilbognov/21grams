# 2g · Buttons: ink, 36px

House default. When the project has its own system, express this through its components and tokens (SKILL.md, rule zero).

## Anatomy
| Property | Value |
|---|---|
| Height | 36px default · 32px compact (tables, toolbars) · 40px prominent (forms, empty states) |
| Padding x | 14px (12px compact, 16px prominent) |
| Radius | 8px |
| Type | 14px / 500 (13px compact) |
| Icon | 16px, left of label, gap 6px, stroke matched to the text (hack #5) |
| Icon-only | square at the button height, hit area ≥ 44×44 on touch (principle #14) |

## Icon-only send in chat
On mobile, the send button of a chat or ask-style input is **icon-only**: a 44×44 square, a paper-plane icon at 18px, radius 8, with `aria-label="Send"`. The label follows the state ("Sending", "Sent"). The states swap icon-to-icon (plane → spinner → check) with the blurred crossfade, and Sent gets the success wave (below). On desktop the button keeps its text label ("Ask", "Send").

```html
<button type="submit" class="send" aria-label="Send"><svg aria-hidden="true">…paper-plane…</svg></button>
```

## Action rows in cards, forms and dialogs
The buttons that end a small card, form or dialog (Cancel / Send invite, Back / Continue):
- **No footer tray.** They sit on the card's own surface, not in a grey strip or a bordered footer container.
- **32px above the row** from the last field, more than the gaps between fields, so the actions read as their own group.
- **Two actions split the row equally:** same width, same height, Cancel (or Back) on the left, the primary on the right. Three or more: right-aligned at their natural widths.
- **The secondary is a quiet filled button** (a light grey fill with ink text), not an outline or bare text, so the pair look like siblings.
- Screen-level actions are different: they go top right in the screen's header (`layout.md`).

## Standalone actions look clickable
An action that stands alone in a card or header ("Export CSV", "View more", "Add context") never sits as bare text that reads like a label. It gets a shape: the **tinted accent fill with accent text** (secondary) or the solid primary. Inline links inside a sentence stay links.

- Export, download and share actions carry their icon before the label.
- "View more" / "Show all" toggles are accent-coloured so they read as actions, not body text.

## Variants
- **Primary:** ink fill (`--ink`), page-colour text. **One per view** (principle #3).
- **Secondary:** 7% ink fill, ink text. No border. **In dark mode, check it on a card, not just on the page:** its fill must be visibly lighter than the card it sits on (about 10–12% ink, or the next surface step). A secondary button the same colour as its card disappears, and this is the most common dark-mode miss.
- **Ghost:** transparent, `--ink-2` text, 6% ink fill on hover.
- **Destructive:** ghost or secondary with `--err` text. It becomes a solid red fill only in the final confirm step.
- **Accent primary:** allowed only where the brand needs the main CTA in colour. The text must pass AA (see colour.md).

## States
| State | Treatment |
|---|---|
| Hover | colour step only (ink mixed 14% toward page). **No movement, no scale, no shadow.** |
| Pressed | colour step 24% **plus `scale(.97)` over 150ms** `--ease-out`, starting in < 100ms (principle #17, craft #4). Not applied when disabled. |
| Focus | 2px ring in `--accent`, 2px offset, `:focus-visible` only |
| Disabled | 40% opacity, `cursor: not-allowed`, no hover change |
| Loading | spinner 14px left of the label, label stays, **width does not change** |
| Success | fill turns the success colour (green, with text that still passes 4.5:1 in both themes), label swaps to the past tense with a tick from the product's icon set ("Sending" → "Sent", "Saving" → "Saved") via a blurred icon swap (hack #7), **plus one wave** (below). Width does not change. It reverts after ~2s, or stays if the view closes |

### The success wave
When an action succeeds, **one thin ring leaves the button** so the person sees that something happened.

- A 2px ring in the success colour, starting on the button's edge and expanding about 10px out while it fades. Its radius grows with it (8 → 14).
- **Snappy:** ~420ms, ease-out. It fires once, the moment the label turns to "Sent". Never loops, never on hover, never on failure.
- Only for actions that leave the screen or can't be seen otherwise (send, invite, publish, save). Not on toggles or navigation.
- Reduced motion: no wave; the green fill, tick and label carry it.

```css
.btn::after { content: ""; position: absolute; inset: 0; border-radius: 8px; border: 2px solid var(--ok); opacity: 0; pointer-events: none; }
.btn.is-success::after { animation: wave 420ms cubic-bezier(.2,.7,.2,1); }
@keyframes wave { from { inset: 0; border-radius: 8px; opacity: 1; } to { inset: -10px; border-radius: 14px; opacity: 0; } }
@media (prefers-reduced-motion: reduce) { .btn.is-success::after { animation: none; } }
```

Transitions: `background-color 120ms cubic-bezier(.2,0,0,1), transform 150ms cubic-bezier(.2,0,0,1)`.

```css
button:active:not(:disabled) { transform: scale(.97); }
```

## Never
Gradients, glow shadows, hover scale or lift, press scale deeper than .95, emoji in labels, mismatched heights in one row, more than one primary in a view, labels like "Get started" or "Submit" (see copy.md).
