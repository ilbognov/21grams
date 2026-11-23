---
name: ux
description: Audit and fix the flows and usability of a product built by AI, so it works the way people expect and not just looks finished, using the project's own components and patterns. Use when the user asks for "21 grams UX" (or "twenty-one grams UX"), wants a flow, journey or screen audited for usability, or asks to fix back and close behaviour, scroll restoration, infinite feeds, optimistic likes and saves, draft saving, permission prompts, bottom sheets, deep links, navigation, forms, empty, loading and error states, feedback, onboarding (questionnaires, sign-up, trials, paywalls, permission asks, tours), destructive actions, accessibility and keyboard use, task length or choice overload in an existing frontend, AI proposals and accept/reject flows, contextual toolbars, delete scopes, keyboard shortcuts, collaboration presence, filters and bottom sheets, missing data and N/A, text truncation, role-based views, mobile and desktop parity, reading width, usage limits and progress, check-in and scan results, expired and blocked states, grace periods, approval requests, date ranges, notification pages, calendars and schedules, grouped navigation, input lag, hardware and kiosk flows, asks how leading products handle a flow or wants UX research with examples (e.g. from Mobbin), or wants a flow checked against UX laws (Hick's, Fitts's, Jakob's, Miller's, Doherty Threshold, Tesler's, Postel's).
---

# 21 Grams UX

A pass over flows that already exist. 21 Grams UX (the UX package of the 21 Grams family) doesn't redesign the product and doesn't add a UI kit. It walks the real flows, finds where AI-built products break down for the people using them (dead ends, missing states, silent failures, unrecoverable actions, forms that fight the user), and fixes them **through the components and patterns the project already has**.

21 Grams UI handles how it looks. 21 Grams UX handles whether it works. When both are installed, run UX first: there's no point polishing a step that shouldn't exist.

## Rule zero: use the project's own components

Every change goes through what the project already uses. 21 Grams UX never builds a parallel set of components or a parallel flow.

1. **Take an inventory before touching anything.** Note the router and route map, the component library, the form library and validation approach, the toast, dialog and empty-state components, the data-fetching layer (where loading and error states come from) and the analytics or event layer if there is one.
2. **Fix things where they live.** A missing error state goes into the shared data or empty-state component, not into one screen. A confirm pattern goes into the project's dialog, not a one-off.
3. **Never add a component or dependency when one exists for the job.** No new form library, toast library or tour library to get a 21 Grams UX effect.
4. **When a piece is genuinely missing** (no empty-state component, no undo), build it from the project's existing primitives, following its file layout and naming. Say so in the report.
5. **Product decisions stay the product's.** 21 Grams UX doesn't change what the product does, who it's for or its business rules. It changes how the existing tasks are carried out. Anything that would change scope goes in the report as a question, not a fix.

**Precedence:** the user's words, then the project's established patterns and product rules, then the 21 Grams UX house rules.

## What's inside

1. **The UX research step.** Before designing or redesigning a flow, analyse the current product and three to five industry-leading examples, one at a time, using a pattern library such as Mobbin when one is connected. The full process is in `references/research.md`.
2. **The UX laws.** The knowledge the rules come from, in `references/laws.md`, cited as A1, A2… by section. Section A is the core laws: Hick's, Fitts's, Jakob's, Miller's, the Doherty Threshold, Tesler's and Postel's. When no rule covers a case, reason from the laws.
3. **The UX rules.** Numbered rules in `references/rules.md`, each with the rule, how to apply it and what to flag, plus a quick audit checklist. Written mobile-first and applied to the web too (primary nav for "bottom tab", popover for "bottom sheet" on desktop).
4. **Field rules.** Rules learned from real review sessions on AI-built products and from UX research on leading products, in `references/field-rules.md`, cited as F1, F2…. This file grows after every session (see "Growing the field rules").
5. **House rules by area** in `rules/`, one file per area, each listing the laws, numbered rules and field rules that belong to it:

| File | Area |
|---|---|
| `navigation.md` | Navigation and wayfinding |
| `forms.md` | Forms and input |
| `states.md` | Empty, loading, error and success states |
| `feedback.md` | Feedback and system status |
| `onboarding.md` | Onboarding and first run |
| `destructive.md` | Destructive actions and recovery |
| `accessibility.md` | Accessibility and keyboard |
| `flows.md` | Flows and task length |
| `choice.md` | Choice and cognitive load |

> Rules #1–5 are reserved and will be added in a later version. Until an area has rules, audit it on general usability judgement and say so in the report.

## Non-negotiables

- X closes a modal or flow. A left arrow goes back one screen. (#6)
- Never a blank screen while loading: skeleton, spinner or progress bar. (#7)
- Back to a feed restores the exact scroll position. (#8)
- Tapping the active tab returns to the top. (#9)
- The next page loads before people reach the bottom. (#10)
- Likes, follows and saves are optimistic, with rollback and a message on failure. (#11)
- Drafts and unfinished input save automatically. (#12)
- Permissions are asked when the feature is used, never at launch. (#13)
- Quick actions open in a bottom sheet that swipes down to dismiss. (#14)
- Notifications and shared links open the exact content. (#15)
- Few choices per step with a recommended default; the rest disclosed. (A1)
- The primary action is large and within reach; touch targets are 44×44. (A2)
- Common jobs use the standard pattern. (A3)
- Information is grouped; nothing has to be remembered between steps. (A4)
- Every input is acknowledged at once; longer waits show progress. (A5)
- The product carries the complexity, not the person. (A6)
- Accept messy input and echo it clean, but never loosen security or data integrity. (A7)
- One control per job. (F1)
- Screen actions grouped top right, primary in the corner, never mixed with selectors. (F2)
- Secondary detail on demand, never lost; never remove the only accessible path to it. (F3, F5)
- Each fact said once; no version numbers, design notes or internal jargon on screen. (F6, F9)
- When an interaction changes, every hint describing it changes too. (F8)
- New UI never claims more than the product's stated scope. (F10)
- No step that repeats the choice that opened it; one option means just do it. (F13, F17)
- One selection, one contextual toolbar, gone on click-away. (F16)
- Everything that can be added can be removed, and a delete shows what it will take. (F18, F19)
- Shortcuts are shown in tooltips and never use browser-reserved keys. (F20)
- AI proposals look provisional, use one accept/reject pattern, and accept instantly. (F23)
- Onboarding: two equal doors, one question per screen with progress, value before the account, skippable tours. (F28, F29, F32, F36)
- Money is honest: a real free path, trials with dates, upgrades at the limit. (F35)
- Reading and picking happen in a narrow centred column; only the step's context and action stay pinned. (F37, F38)
- Missing data says N/A, text is clamped and aligned, and every list is checked with real volumes. (F43, F44, F45)
- Roles change the starting point, not the app; mobile and desktop share the same patterns. (F47, F50)
- Limits show used of total, and the moments people wait for fill the screen, then close themselves. (F51, F52)
- Every blocked state offers its fix; approvals are requests and exceptions leave a note for the next person. (F53, F54, F55)
- Only the states the business really has, and typing never waits on background work. (F59, F63)

## Workflow

1. **Take the inventory** (rule zero).
2. **Research** (`references/research.md`). For a new flow, a redesign or onboarding, start here: find out what's being designed and for whom, analyse the current flow, recommend three to five industry-leading examples, and go through them one at a time with the user before changing anything. Skip it only for small fixes to an existing flow.
3. **Map the flows.** List the main tasks a person comes to do, and for each one the route through the product: entry point, every step, every branch, the end state. Note where each step's data comes from.
4. **Walk each flow in the browser,** not just the code. Try the happy path, then the edges: nothing there yet, slow network, a failed request, invalid input, going back, refreshing mid-flow, keyboard only, a narrow screen.
5. **Audit before changing anything.** Go through the checklists at the end of `references/rules.md`, `references/laws.md` and `references/field-rules.md`, and the area files. List findings grouped by area, rule number and law. Each finding gets the flow and step, the file and line, what goes wrong for the person, the fix, and **which existing component or pattern the fix goes into**. Rank them: blocks the task, slows the task, rough edge.
6. **Show the audit to the user** as a short list and ask before applying broad changes. Small, obvious fixes in the requested scope can go straight in.
7. **Apply the fixes** in this order: shared components and patterns → flows → individual screens. Keep diffs scoped and in the project's own conventions.
8. **Verify by walking the flows again** in the browser, including the edge cases from step 3. Capture before and after for each changed step.
9. **Report** what changed per flow and area, which components were touched, and the open questions that are product decisions.

## Growing the field rules

21 Grams UX learns from real work. When the author finishes a review session on an AI-built product and asks for it to be added:

1. Read that session's conversation and list every change the author asked for or accepted.
2. Keep the UX changes (flow, structure, placement, states, feedback, copy that guides people, accessibility paths). Visual changes (radius, colour, type, icons, motion) belong to 21 Grams UI.
3. Write each one as a general rule: the rule, how to apply it through the project's own components, and what to flag. No client names, product names or private content.
4. If a rule refines an existing one, update that rule instead of adding a new one.
5. Add new rules to `references/field-rules.md` under a session heading, continue the F numbering, and list them in the right area files.
