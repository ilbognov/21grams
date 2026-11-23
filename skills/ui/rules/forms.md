# Forms: errors you can't miss

House default. When the project has its own system, express this through its form components and tokens (SKILL.md, rule zero). Wording comes from `copy.md`; this file is how errors look and behave.

## Where the error goes (strict)
- **Next to the field it's about**, directly under it. Never only in a banner, toast or alert at the top of the form.
- **No form-wide banner for a field problem.** A banner is only for errors that belong to no field (the network is down, the session expired), and it says what to do.
- **Five or more errors:** a short summary at the top ("3 fields need attention") with links that move focus to each field, as well as the inline messages.

## How it looks
| Part | Spec |
|---|---|
| Field | danger border plus a 1px danger ring, 120ms ease-out. The label stays ink |
| Message | 13px in the danger text colour, under the field with a 6px gap, an alert icon (16px, same icon style as the product) before the text. It enters with opacity and a 2px drop over 160ms |
| Signals | **outline, message and icon together.** Colour is never the only signal |
| Space | the message pushes content down; it never overlaps the next field |

## When it appears
- **Check on submit, not while typing the first time.** Don't shout at someone who hasn't finished. `blur` checks are fine for format problems on long forms.
- **After the first submit, re-check as the person types** and clear each message the moment its field is fixed. Live counts help: "Use at least 12 characters. You have 7."
- **Focus moves to the first field with a problem** on submit.
- **Server errors** land on the field they concern (an email that's already registered goes under the email field) and offer a way out: "There's already an account with this email. Sign in instead, or use a different email."
- The submit button keeps its label and width while working ("Creating account" with a spinner) and is never disabled just because the form isn't valid yet. Let people tap it and show them what's missing.

## The field shakes (excessive feedback)
Every empty or invalid field **shakes once** when the person submits, on top of the outline, message and icon.

- **Only the invalid fields shake,** never the whole form or the button. Fields that are fine stay still.
- One horizontal shake that settles: about ±6px, 4 steps getting smaller, ~320ms.
- It replays on **every submit** while a field is still wrong, and when the server rejects a field. Typing never triggers it.
- On phones, a short vibration (`navigator.vibrate(30)`) where supported.
- **Reduced motion:** no shake; the outline, message and icon carry the error.
- This is the one sanctioned exception to "no bounce": it answers something the person just did and points at the exact field to fix.

```css
.field.invalid input { border-color: var(--err); box-shadow: 0 0 0 1px var(--err); }
.shake { animation: shake 320ms cubic-bezier(.36,.07,.19,.97); }
@keyframes shake {
  20% { transform: translateX(-6px); } 40% { transform: translateX(5px); }
  60% { transform: translateX(-3px); } 80% { transform: translateX(2px); }
}
@media (prefers-reduced-motion: reduce) { .shake { animation: none; } }
```

```js
// on submit
const bad = fields.filter(f => !f.valid);
bad.forEach(f => { f.el.classList.remove('shake'); void f.el.offsetWidth; f.el.classList.add('shake'); });
if (bad.length) { navigator.vibrate?.(30); bad[0].el.focus(); }
```

## Field details
- **No label that repeats the heading.** A single field under a heading that already names it ("Added context" → a textarea) drops its visible label and keeps an `aria-label`.
- **Helper text sits tight to what it explains** (4px under its label or heading), with the bigger gap before the next group.
- **Counters appear near the limit**, e.g. "40 characters left" once 80% is used. Not a permanent "500 characters remaining".
- **Counts in headings are quiet:** "Added context · 1" in sentence case, not "ADDED CONTEXT (1)".
- Row actions on someone's own entries (delete, edit) stay faint until the row is hovered or focused, and are always visible on touch.

## Fields respond on the next frame
Typing never waits on background work (behaviour: UX F63). When fields feel slow or jumpy, look at what re-renders before touching styles:

- **Live data must not redraw the form.** Polling sends the version it already has and the server answers "not modified"; when nothing changed, don't set state at all.
- **Input state stays local to the field**, not in a store that every update replaces.
- **Long lists filter after the keystroke** (`useDeferredValue`, or a short debounce), so the field renders first and the rows follow.
- **Clocks tick coarsely.** "10 days left" or "in progress" doesn't need a root-level timer every second; 15–60s is enough.
- Check it by typing fast while live data is on. Each keystroke should land within a frame (≈16ms).

## Semantics
- `aria-invalid="true"` on the field and `aria-describedby` pointing at its message, so screen readers announce it when focus lands there.
- Messages live in a polite live region; the summary (if any) gets focus on submit.
- Use `novalidate` on the form so the browser's own bubbles don't compete with these messages.

## Audit
- Submit an empty form: does each empty field get its own message, outline, icon and shake, and does focus land on the first?
- Fix one field: does its message clear while the others stay?
- Trigger a server error: does it land on the right field with a way out?
- Turn on reduced motion: no shake, everything else still there.

## Never
"Oops!", "Something went wrong" with nothing after it, "Error: invalid input", a red banner as the only signal, shaking the whole form, shaking on every keystroke, disabled submit buttons with no explanation, the browser's native validation bubbles alongside custom messages, errors shown in placeholders.
