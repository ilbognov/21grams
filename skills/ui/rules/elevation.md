# 7g · Elevation: tonal fills

House default. When the project has its own system, express this through its components and tokens (SKILL.md, rule zero).

## Layers
| Layer | Light | Dark | Border | Shadow |
|---|---|---|---|---|
| 0 Page | `--surface-0` | L≈15% | none | none |
| 1 Resting (cards, sections, wells) | one fill step from the page | L≈22% | **none** | **none** |
| 2 Floating (menus, popovers, toasts) | `--surface-raised` (white in light) | L≈30% | 1px alpha ring | yes |
| 3 Modal | same as floating | L≈30% | 1px alpha ring | strongest, plus scrim |

- Resting surfaces separate by **fill only**: no border, no shadow.
- **Only floating layers cast shadows.** A shadow means "this sits above the page".
- Dark mode: each higher layer is lighter (hack #8). Shadows barely show on dark, so the lightness step does the work.
- **Keep the dark step small.** On a near-black page, cards sit a few percent lighter (about `#1F1F1F` on `#121212`), not a jump to `#2A2A2A` that makes every card shout. Dividers inside dark cards are fainter still.
- No cards inside cards. If content needs a sub-group inside a card, use a divider or a fill step, not another bordered box.

```css
.card    { background: var(--surface-1); border-radius: var(--r-container); }
.popover { background: var(--surface-raised); box-shadow: var(--ring), var(--shadow-float); }
```

## Never
Shadow + border + radius on every card, `shadow-lg` on resting content, floating menus that look like the cards beneath them, dark themes where page, card and menu share one colour.
