# 5g · Spacing: grouped, 4pt

House default. When the project has its own system, express this through its components and tokens (SKILL.md, rule zero).

## Scale
4 · 8 · 12 · 16 · 20 · 24 · 32 · 48 · 64. Nothing off-scale. No 6px except label → input.

## Grouping (proximity encodes relationship)
| Relationship | Gap |
|---|---|
| Title → its description | 4 |
| Label → its input | 6 |
| Input → its helper or error text | 6 |
| Field → field | 16 |
| Group → group (fieldsets, card sections) | 24–32 |
| Section → section on a page | 48 (**32 on a phone**) |
| Panel padding | 20 (16 on mobile) |

- **A big number and its caption: 8.** "€12,480" over "83 members" is a title and its description, but the large figure needs a little more air than the 4 used for text.
- **A list's heading sits 24 above the list** when the list is the page's main content ("Published · 3" above the posts), so the heading reads as the header of the whole list rather than of the first item.
- Things inside a group are always closer than the gap between groups. If two gaps are equal, the grouping is lost (the AI tell).
- Footers and action bars are separated by a hairline or a fill step (see elevation.md), padding 12×20, actions right-aligned with the primary last.
- Use `gap` on flex and grid parents, not margins on children.

## Controls
- Inputs and selects: height 36, padding x 12.
- **Selects and dropdown triggers:** replace the native arrow with a 16px chevron placed **12px from the right edge**, and give the control `padding-right: 36px` so text never runs under it.

```css
select, .select-trigger {
  appearance: none;
  padding-inline: 12px 36px;
  background: var(--chevron) no-repeat right 12px center / 16px 16px;
}
```

## Never
Uniform `p-6 gap-6` everywhere, a label as far from its input as from the next field, cards used to create spacing (use whitespace and dividers first).
