# Field rules

Rules learned from real passes on AI-built products and from UX research on industry-leading products (`research.md`). Each one comes from a change the author asked for while reviewing a live build, or from a pattern the author adopted after research, written as a general rule. They're cited as F1, F2… so they never clash with the numbered rules in `rules.md` (#1…) or the laws in `laws.md` (A1…).

This file grows over time: after each review session, the UX changes made there are added here.

Each entry has the rule, how to apply it through the project's own components, and what to flag in an audit.

---

## Session 1: clinical dashboard (patient list, report and trend screens)

### F1. One control per job
**Rule:** A screen has one control for each job. Remove duplicates, even when they're in different places.
**Apply:** Look for controls that do the same thing: several collapse buttons for one sidebar, a copy button in both a card and the header, two routes to the same dialog. Keep the one in the conventional place (A3) with the clearest icon, and remove the rest. Where the survivor moves (a sidebar toggle when collapsed), it stays reachable in every state.
**Flag:** Two or more buttons, links or icons that do the same thing on one screen.

### F2. Screen actions top right, primary in the corner
**Rule:** The actions for the current screen sit together at the top right of its header, with the primary action in the corner. They're never mixed in with selectors, filters or date controls.
**Apply:** Move screen-level actions (export, open PDF, copy, share) into the header's right edge as one group: secondaries first, the solid primary last, in the corner. Label the group for assistive tech ("Report actions"). Selectors and navigation (date pickers, previous/next, filters) keep their own bar. On mobile, the group drops below the title as a full-width row. Remove any copy of the same action elsewhere on the screen (F1).
**Flag:** Actions inline with selectors, actions scattered between header, toolbar and cards, the primary not in the corner, more than one primary.

### F3. Details on demand, not always on
**Rule:** Secondary detail goes in a popover or the detail view, not in every row. Keep each row to what people scan for.
**Apply:** Move breakdowns, ranges, notes and counts that people only need sometimes into a hover popover (desktop) or the detail view, and remove them from the row. Nothing may be lost: every removed fact has to be reachable in the popover or detail view. Once a popover explains a thing, remove the in-row expand button, the legend strip and the hint that used to explain it.
**Flag:** Rows with two or three lines of small supporting text, legends that repeat what a popover or label already says, expand buttons next to a popover that shows the same thing.

### F4. Popovers that present a breakdown clearly
**Rule:** A hover popover for a chart or bar is a small, structured panel, not the browser's text tooltip.
**Apply:**
- **Header:** what it's about (the entity, e.g. the person's name) and its context (date range, number of segments).
- **One row per segment:** colour, name, the value range if there is one, a small bar sized to the share, and the figure. Order rows the same way as everywhere else in the product.
- **Follow the pointer:** highlight the row for the segment under the cursor.
- **Totals only when they add something.** Skip a totals line that would repeat the rows.
- **Position:** below the trigger, flipping above near the bottom edge, never off-screen.
- **Closing:** close on pointer leave and on scroll.
- **Touch:** no hover popovers on touch; a tap opens the detail view instead.
- **Keyboard and screen readers:** the trigger's accessible name carries the same figures, so nothing depends on hovering.

**Flag:** Native `title` tooltips for data, popovers that cover the trigger or run off-screen, data that's only reachable by hovering.

### F5. Never remove the only accessible path
**Rule:** Before removing a control, check whether it was the only way to reach something by keyboard, touch or screen reader. If it was, give that path somewhere else first.
**Apply:** When a hover popover replaces an expand button, give the trigger an accessible name with the values, keep tap-to-open on touch, and keep the detail reachable by keyboard.
**Flag:** Information only reachable by mouse hover, removed buttons that leave touch or keyboard users with no route.

### F6. Say each thing once
**Rule:** Remove copy and labels that repeat what the screen already says.
**Apply:**
- An eyebrow that repeats the breadcrumb goes.
- A "demo" chip goes when the header already says demo.
- A count pill goes when the heading can carry the count (F7).
- Legend strips go when the popover or labels name each item.
- Keep the clearest single instance, in the conventional place.

**Flag:** The same fact in a chip, an eyebrow and a subtitle; legends next to self-labelling charts; status said twice.

### F7. Counts belong in the heading
**Rule:** A list's count sits in its heading as a quiet number, not in a separate pill: "Patients 21".
**Apply:** Put the number right after the heading text at the same size, visibly secondary (lower opacity or the secondary text colour). When search or filters are active, it shows the matching count, and the full figure is available on hover ("1 of 21 patients").
**Flag:** "21 / 21 items" pills beside a heading, counts that don't change with filters, a count far from the list it counts.

### F8. Keep instructions true
**Rule:** When an interaction changes, update every hint, subtitle, note and help line that describes it, in the same change.
**Apply:** Search the copy for the old verb and the old control ("click the bar", "use the arrow") and rewrite it for the new behaviour, or remove it if the interface now explains itself.
**Flag:** Hints that mention removed buttons, "click" copy for something that now opens on hover, help text describing an old flow.

### F9. No internal language on screen
**Rule:** Product UI never shows version numbers, design notes, internal codes or regulatory shorthand that its users wouldn't recognise.
**Apply:**
- Remove "UX V7", "V7.9", "draft" labels and design-rationale boxes from the interface. Versions live in the page title, the about screen or code comments.
- Replace jargon ("outside SaMD scope") with what it means for the user, said once (F6). If it must stay for compliance, ask.
- Keep one form of address throughout (informal or formal, never both).

**Flag:** Version labels that disagree with each other, notes that read like design comments, acronyms from the team's world rather than the user's, mixed formal and informal address.

### F10. Stay inside the product's stated scope
**Rule:** New UI never makes judgements or claims the product says it doesn't make.
**Apply:** If the product says it doesn't classify risk or raise alarms, popovers show no target flags ("TIR > 70% ✓"), notifications are about workflow only (new reports, imports, exports ready), and sorting criteria are chosen by the user. Read the product's disclaimers before adding status, colour-coding or alerts.
**Flag:** Pass and fail marks, risk colours or alerts added by a redesign in a product that disclaims them.

### F11. Account at the bottom of the nav, notifications at the top right
**Rule:** The signed-in user sits at the bottom of the side navigation, with a menu that holds sign-out. Notifications sit in the top bar's right-hand tools.
**Apply:**
- **Account:** avatar, name and role at the bottom of the sidebar. It opens a small menu upward with the account details and "Sign out". With the sidebar collapsed, the avatar alone stays pinned at the bottom.
- **Notifications:** a bell with an unread count in the top-right tools. It opens a panel where:
  - unread items are marked;
  - clicking an item marks it read and opens the exact content (#15);
  - "Mark all as read" clears the count.
- **Keyboard:** both menus close on Escape and move with the arrow keys.
- **Mobile:** bell, theme and avatar sit in the header's right side, each 44×44. They share state with desktop, so reading an item on one clears it on the other.

**Flag:** A user block in the top bar that isn't a person, sign-out buried in settings, notifications with no unread state or no route to the item, account and notifications missing on mobile.

### F12. Confirm in place without moving things
**Rule:** Quick actions confirm on the control itself, and controls keep their size across every state.
**Apply:** After copy, save or similar, the button shows the success state (check icon plus "Copied") at the same width, then returns to its resting state after a few seconds (about 5). Nothing beside it shifts. Buttons whose label changes with the mode (e.g. "See transcript" inside and outside a session) get a fixed width that fits the longest label. Use a toast only when the result isn't visible from the control.
**Flag:** Buttons that change width on success or between modes, success states that never revert, "✓ Copied!" with an exclamation mark, a toast for something the button could show.


---

## Session 2: collaborative canvas (nodes, connections and AI proposals)

### F13. Don't ask again for what was just chosen
**Rule:** A step that repeats the choice that opened it goes. Clicking "Create session" lands on the first real step of creating one, not on a screen that asks to create a session.
**Apply:** Walk every entry point and remove intro and confirmation screens that only restate the intent. Open dialogs on the step that needs input, with an X at the top right to close (#6).
**Flag:** "Are you ready to…?" screens after an explicit click, two clicks on the same verb in a row, splash steps inside a dialog.

### F14. No dead controls
**Rule:** Only show controls that do something here and now. Remove the ones that can't act (an Edit button on something that can't be edited) and options nothing uses.
**Apply:** For each control, ask what it does in this state. If nothing, hide it in that state or remove it from the product. Don't keep placeholder actions "for later".
**Flag:** Edit on read-only items, menu options with no effect, actions that only show an error when used.

### F15. Inline edits save themselves
**Rule:** Editing text in place needs no Save or Confirm button. Enter or clicking away commits; Escape cancels.
**Apply:** Remove per-field Save and tick buttons from inline edits. Commit on blur and Enter, cancel on Escape, and show a quiet saved or error state on the field (#11, #12).
**Flag:** Tick or Save buttons beside inline fields, edits lost on click-away, a separate save step for a single value.

### F16. Contextual toolbars follow the selection
**Rule:** One selection, one contextual toolbar. It appears when something is selected and goes away when the selection does.
**Apply:**
- Selecting an item shows its toolbar; selecting another item moves the toolbar, never adds a second one.
- Clicking empty space deselects and hides the toolbar.
- When another mode takes over (writing an annotation, a dialog), the toolbar hides until that mode ends.
- Items that can't be edited (an unaccepted AI proposal, someone else's locked item) get no edit toolbar.
- Every selectable item type shows its toolbar; check each one.

**Flag:** Two edit toolbars at once, toolbars that stay after clicking away, toolbars on items that can't be edited, item types that don't show a toolbar when selected.

### F17. Only offer real choices
**Rule:** If there's only one option, do it instead of asking. If an option doesn't apply, leave it out instead of showing it disabled.
**Apply:** A drag that can only create one kind of item creates it straight away. A menu whose second option has no target (nothing after this item to delete) shows only the first. Keep disabled states for options that will become available once the person does something they can see.
**Flag:** Pickers with one choice, disabled options that can never be enabled in this context, menus that shrink to a single item but still open (A1).

### F18. Everything that can be added can be removed
**Rule:** Every item, connection, step or action people can create has a visible way to remove it.
**Apply:** Check each creatable thing for a remove path in its toolbar or menu, plus Delete/Backspace when it's selected. That includes things in between other things (an action between two nodes, a step in the middle of a flow).
**Flag:** Items that can be created but not deleted, delete only by keyboard, middle items that can't be removed without breaking the rest.

### F19. Show what a delete will remove
**Rule:** When a delete can take more than the item itself, offer the scopes as named options and preview each one before it happens.
**Apply:** Delete opens a small menu next to the toolbar with clear scopes ("Delete card only", "Delete card and what follows"). Hovering or focusing an option dims everything that option would remove (around 20% opacity), so people see the consequence before they click. Show only scopes that apply (F17). Pair with undo where the product has it.
**Flag:** Deletes that silently take children or following steps, scope options with vague names, no preview of what goes.

### F20. Shortcuts are shown and don't fight the browser
**Rule:** Every tool's tooltip names it and shows its shortcut, and shortcuts never use combinations the browser or OS already owns.
**Apply:** Tooltips read "Add story actor ⌘A" style: name, then shortcut. Before assigning a shortcut, check it against reserved ones (⌘W closes the tab, ⌘T, ⌘N, ⌘Q, ⌘R, ⌘L; ⌘A is select-all in text fields, so scope it to the canvas). Give the main groups of tools shortcuts, not just some.
**Flag:** Tools with no tooltip or no shortcut shown, shortcuts that close or reload the browser, shortcuts that hijack text editing.

### F21. The cursor says what will happen
**Rule:** The cursor matches the action available under it.
**Apply:** Default arrow for selecting, an open hand where the canvas can be panned and a closed (grabbing) hand while panning, a pointing hand on handles and connection points that start a drag, text cursor in editable text. Use the product's own cursor art if it has some.
**Flag:** The same cursor for selecting, panning and connecting; a hand where clicking selects; no cursor change on drag handles.

### F22. Canvas tools ignore zoom
**Rule:** Toolbars, menus and labels attached to canvas items stay the same screen size at every zoom level.
**Apply:** Render floating tools in screen space, positioned from the item. Hide them while the person is zooming or panning and bring them back when it stops.
**Flag:** Toolbars that grow and shrink with zoom, menus too small to hit when zoomed out, tools that lag behind during pan.

### F23. AI proposals stay provisional until accepted
**Rule:** Anything the AI proposes looks clearly provisional, is handled the same way everywhere, and becomes real the moment it's accepted.
**Apply:**
- **Look:** proposals are visibly different from confirmed content (reduced opacity, dashed outline and dashed connections), and only the new part is marked. Content that's already confirmed doesn't get the proposal treatment, even when it's part of the proposed sentence or path.
- **One decision pattern:** every proposal uses the same accept and reject controls, wherever it appears. Clicking the proposal itself can accept it. Reject sits apart, with a trash or X icon.
- **Preview the decision:** hovering accept raises the proposal towards full opacity; hovering reject fades it further. Hovering a proposal highlights everything it belongs to (the whole path).
- **No editing before acceptance:** proposals get no edit toolbar (F16). If the person changes a proposed word, apply it straight away instead of proposing the change.
- **Instant acceptance:** accepting is immediate, with no delay or animation blocking the next action. Accepted items settle in place before moving to their final position.
- **Not a loading state:** the proposal treatment mustn't look like content still loading.
- **Confidence:** where confidence differs, show it through the treatment (e.g. underline style), not scores or badges.

**Flag:** Proposals that look like confirmed content, different accept/reject designs in different places, editable proposals, delays after accepting, the proposal frame drawn around already-confirmed items, proposal styling that reads as "loading".

### F24. Show what the AI is doing, on request
**Rule:** When an AI is listening or working in the background, show a small, persistent status and let people open it to see what it heard and did.
**Apply:** A compact chip or bar shows the state (listening, processing, done, error). Tapping it expands in place, at the same width, to show the recent transcript or steps, with the recognised words highlighted. Keep a short, capped history (around five items) and stack older ones. Design the error and success states as well as the idle one.
**Flag:** Background AI with no visible status, status that can't be inspected, endless growing lists of what was heard, no error state.

### F25. Show who else is here
**Rule:** In shared spaces, people see each other's cursors, names and selections.
**Apply:** Each collaborator gets a colour. Their cursor carries a name label, items they select are outlined in their colour, and hovering an item someone else has selected shows their name. Keep your own selection style distinct from theirs.
**Flag:** No presence on a shared canvas, selections with no owner, colours that clash with status or proposal colours.

### F26. Waits and cooldowns live on the control
**Rule:** When an action is temporarily unavailable, the control says when it'll be back. Don't explain the wait in a separate paragraph.
**Apply:** "Resend link in 9:42" as the disabled button's label, counting down, then the enabled "Resend link". Remove the explanatory paragraphs around it ("The link lasts 10 minutes…", "You can now request another link"). Confirmation copy echoes what the person entered ("Link sent to name@example.com") so they can spot a typo (A4).
**Flag:** Disabled buttons with no reason, countdowns in body text, paragraphs explaining timing the control could show, confirmations that don't repeat the address or value used.


---

## Research: onboarding (Brilliant, Duolingo, Raycast)

From a UX research pass over three leading iOS onboarding flows on Mobbin: [Brilliant](https://mobbin.com/flows/7ffbd4f0-78d1-49be-bf0d-9c90cac00e8c), [Duolingo](https://mobbin.com/flows/b0b4f93f-5637-46ec-9d77-49ecda6b991d) and [Raycast](https://mobbin.com/flows/1c30eb52-9997-4a33-a50d-05dc3e7a8f09).

### F27. Match onboarding depth to what people already know
**Rule:** People who are still deciding get a short, personalised onboarding. Returning users, and people who already chose the product (a companion app, a tool their team uses), go straight into the product.
**Apply:** Work out who arrives at the first screen and why. Skip the questionnaire for people who come from another platform or an invite, and let the product's empty states teach instead (F34). Keep personalisation for first-time evaluators.
**Flag:** Long questionnaires for people who already know the product, account walls before any value for people still deciding.

### F28. Two doors on the first screen
**Rule:** The first screen offers "Get started" and "I already have an account" with equal weight.
**Apply:** Two full-width buttons, start first. Returning users go straight to sign-in and never see onboarding questions. Keep the welcome copy to one line about what the product does.
**Flag:** Sign-in hidden in a small link or only reachable after the onboarding questions, welcome carousels before the doors.

### F29. One question per screen, with progress
**Rule:** Onboarding questions come one per screen, with a progress bar and a back arrow on every step.
**Apply:** Large answer cards or a single field per screen. Continue stays disabled until there's an answer. The progress bar fills as people go, so they always know how much is left. Use at most one screen that only reassures or explains; every extra screen is a chance to leave.
**Flag:** Several questions on one screen in onboarding, no progress indicator, no way back, several filler screens ("You'll fit right in") in a row.

### F30. Options show, not label
**Rule:** Answer options describe what the person can do or show a concrete example, rather than an abstract label.
**Apply:** "I can have basic conversations" instead of "Intermediate", a code sample instead of "Advanced", "Morning routine during breakfast" instead of "Morning". Add a small icon or level indicator where it helps. Offer "Other" when the list can't be complete (A7). Use multi-select with checkboxes when more than one answer is true.
**Flag:** Beginner/Intermediate/Advanced with no description, lists that force a wrong answer, single-select where several answers apply.

### F31. Reflect answers back
**Rule:** Show people how their answers changed what they get, and say how long the next step takes.
**Apply:** After the questions, one line that uses the answers ("Since you know a few words, let's start at Score 10") and sets the expectation ("Here's your first 2 minute lesson"). Use the name or details people gave in later steps ("What is your email address, Sam?").
**Flag:** Questions whose answers never visibly matter, open-ended next steps with no time or size, forms that re-ask what was already given.

### F32. Value before the account
**Rule:** People get something of value before they're asked to create an account, and the account is presented as keeping it.
**Apply:**
- Personalise first, or let people use the product (a first lesson, a first result) before the sign-up screen.
- Frame sign-up as saving what they made ("Create a free account to keep your learning path").
- Put Apple, Google and any audience-specific provider (GitHub for developers) first, email second, and "Existing user? Log in" visible.
- Keep the form to email and password; derive usernames, ask for names later.
- Show a busy state on the button while the account is created ("Creating…").

**Flag:** An account wall on the first screen for people still deciding, sign-in providers below a long form, four-field sign-up forms, sign-up with no visible busy state.

### F33. Permissions and add-ons in context
**Rule:** Ask for permissions and add-ons (notifications, widgets, contacts) at the moment they make sense, show what people get, and make "Not now" a clear second option.
**Apply:** Show a picture of the benefit (the widget on a home screen, the reminder they'll get), one primary button and a "Not now" that's easy to see and tap. Never use fear of missing out in the copy. Extends #13.
**Flag:** Permission prompts with no benefit shown, hidden or tiny "Not now", pressure copy ("Don't lose your streak!").

### F34. Empty states that onboard
**Rule:** A new user's empty screens teach the product: what will go there, and one action to start.
**Apply:** Faded example content in the shape of the real thing, one line saying what it's for, and a single action ("Customize", "Add your first…"). Where the product can see what people do, offer suggestions from it (recent searches, suggested items, each with a + to add).
**Flag:** Blank screens or "Nothing here" for new users, empty states with several competing actions, suggestions that ignore what the person has done.

### F35. Honest money
**Rule:** Money is always clear and never a trap: a real free path, trials with dates, upgrades offered at the moment they matter.
**Apply:**
- **Free path:** if there's a free plan, it's a full option on the plan screen, and the reply to choosing it is positive ("You can upgrade anytime").
- **Trials:** a timeline (today, the reminder, the charge date) and a reminder the person chooses, with real dates, plus "Cancel anytime" in plain words.
- **Upgrades:** offered when someone reaches a limit or uses a paid feature, next to that feature, with a usage meter ("45 AI messages left").
- **Terms:** price, renewal and cancellation in one plain sentence, plus Restore purchases.

**Flag:** Paywalls in the middle of onboarding with no free option, struck-through "discount" prices as pressure, trials with no charge date, hidden renewal terms, no Restore.

### F36. Tours can always be skipped
**Rule:** Feature tours come after the first win, and every step has "Skip".
**Apply:** Show the tour once the person has done the main thing, keep it to a few steps with a step indicator, and let them skip or close it at any point. Prefer teaching in context (F34, tooltips at first use) to a tour.
**Flag:** Tours before the first use, tours with only "Next", tours that come back after being dismissed.

## Session 3: mobile-first analytics app (portfolio, product and role views)

### F37. Reading width for reading and choosing
**Rule:** Steps where people read or pick from a list sit in a narrow, centred column, not stretched across the screen.
**Apply:** Selection steps, settings and text-heavy pages get a column about as wide as a card (roughly 480–640px on desktop), centred, with the rest of the screen left empty. Dashboards and tables can use the full width; reading and choosing can't.
**Flag:** Pickers, settings or forms stretched across a wide screen, lines too long to scan, checkboxes far from their labels.

### F38. Pin only what's needed while scrolling
**Rule:** In a long step, the context and the action stay on screen; everything else scrolls away.
**Apply:** In a multi-select step, pin the title, the selection count and the search at the top, separated the same way as the pinned primary action at the bottom (a hairline or a surface change). Page headers, greetings and decorative bars scroll with the content.
**Flag:** A selection count or Next button that scrolls out of view, sticky headers that only take up space, top and bottom pinned areas separated in different ways.

### F39. Filters sit with the list and open as a sheet
**Rule:** Filters sit next to the list they change and, on mobile, open as a bottom sheet with an Apply action.
**Apply:** Call the control "Filters", put it beside the list header or search, open a bottom sheet, apply on the button, and show the number of active filters on the control. Reuse the same filter component across screens. Extends #14.
**Flag:** Filters far from what they filter, filters that apply on every tap with the list jumping behind the sheet, different filter patterns on different screens, no sign that filters are on.

### F40. Overview first, detail on tap
**Rule:** Dense visuals show a compact overview first and open the full view on tap.
**Apply:** On mobile, show the overview the page is for near the top (for example, a colour-only heat map that lists every row) and open the full chart on tap, in landscape or full screen. In cards, "See all" expands the card in place to show the remaining values. Extends F3.
**Flag:** The page's main visual buried below lists, full desktop charts squeezed onto a phone, "See all" that jumps to another screen for a few values.

### F41. Clickable at the level you click
**Rule:** The affordance sits on the thing that acts: the cell, the card or the button, not the whole row.
**Apply:** When each cell in a table opens something, give each cell its own hover and pressed state. Make buttons look like buttons when idle (a tinted fill with coloured text), not only on hover. If a hover state carries useful information, make it the default, because touch has no hover.
**Flag:** Row hover on tables where only cells act, buttons that look like plain text until hovered, information only visible on hover.

### F42. Short labels, definitions on request
**Rule:** Labels are one or two plain words. The explanation is a tap or hover away, and every label passes the test "what does this mean?".
**Apply:** "Forecast", "Supply", "Cost", "Quality" as labels, with the definition in a popover on the label (F4). When a reviewer asks what something means, rename it or add the definition; don't add a paragraph under it.
**Flag:** Long column headers, labels that need a sentence to explain, definitions printed under every label, labels nobody outside the team understands (F9).

### F43. Say when data is missing
**Rule:** When there's no value, the screen says so ("N/A"), never a blank, a zero or a broken chart.
**Apply:** Use one missing-value marker across the app, in the same place as the value, muted, with the reason on hover or tap when it's known. Charts leave a gap rather than drawing zero.
**Flag:** Blank cells, zeros standing in for missing data, "undefined" or "NaN", charts that drop to zero where data is missing.

### F44. Clamp text and align siblings
**Rule:** Text in repeated cards has a line limit, and the same slot sits at the same height in every sibling.
**Apply:** Clamp to a set number of lines (two for supporting text) with an ellipsis and the full text on tap or hover. Pin repeating slots, like a card's key metric, to the same place (for example, the bottom of the card), so titles and values line up across a row.
**Flag:** Cards of different heights because one value wraps, the same field at different heights across siblings, text cut without an ellipsis.

### F45. Design for real volumes
**Rule:** Check every list, chart and card group with realistic and extreme amounts of data before calling it done.
**Apply:** Try none, one, the typical count and many (ten products, not two), plus the longest real names and values. Decide what happens beyond the limit: scroll, "Show more" or a summary.
**Flag:** Layouts that only work with the two sample items, long names breaking cards, charts that become unreadable at real counts.

### F46. One kind of thing per container
**Rule:** Different kinds of content sit in separate containers. The things people act on are cards, and things of the same level get the same treatment.
**Apply:** Separate items (products at risk) from commentary (insights) with separate containers, not a divider inside one. Show objects people open or compare as cards with their name and key figure, not as plain list rows. When two sections have the same importance, give them the same container and heading size.
**Flag:** Unrelated content in one box split by a line, objects shown as plain text rows that don't feel like objects, equally important sections styled differently.

### F47. Roles change the starting point, not the app
**Rule:** When different roles use the same product, change what each sees first and what they can switch between, and keep shared screens identical.
**Apply:** Give each role its own home (a team sees its products, executives see the portfolio as home) and hide only the views that role doesn't use. Keep names, components and flows the same everywhere else. For prototypes and reviews, add a view switcher so everyone can see each role.
**Flag:** Separate apps per role, the same screen built twice with small differences, roles that lose shared features for no reason.

### F48. One picker for add and edit
**Rule:** Adding and editing a selection open the same picker, and an empty selection leads straight to it.
**Apply:** "Add products" with nothing selected and "Edit" on an existing selection both open the same slide-in panel, which lists what this person can choose from, with current choices ticked. The empty state's action is that same "Add" (F34).
**Flag:** Different screens for adding and editing the same thing, empty states with no way to start, pickers that list items the person can't use.

### F49. On/off settings are toggles
**Rule:** A setting with two states that takes effect at once is a toggle.
**Apply:** Use a switch for on/off settings that apply immediately, checkboxes for choices submitted with a form, and a segmented control for two or three named options.
**Flag:** On/off settings as dropdowns or pairs of buttons, toggles that need a Save to take effect.

### F50. Same patterns on every platform
**Rule:** Mobile and desktop share the same patterns, names and order; only the layout adapts.
**Apply:** Design mobile first, then carry each pattern to desktop in the desktop layout (bottom sheets become side panels or popovers, stacked cards become a grid). Use the same labels, icons and flow order on both.
**Flag:** A feature named differently on desktop, flows with different steps per platform, icons or components that only one platform uses.

## Session 4: membership and check-in app (member app, front desk and back office)

### F51. Show usage as used of total
**Rule:** Anything with a limit shows how much is used out of the total, not only what's left or what was bought.
**Apply:** Write "8/12 sessions", not "12 sessions". For small totals, draw one segment per unit so people can count at a glance, and colour the bar by what's left (plenty, getting low, used up). Keep the same count and colours everywhere the limit appears.
**Flag:** A bare total with no usage, a remaining count with no total, progress bars that can't be counted, a limit that is shown differently on different screens.

### F52. Big outcomes fill the screen, then step aside
**Rule:** The result of a moment people wait for (a check-in, a scan, a payment) is unmistakable from across the room and leaves on its own.
**Apply:** On success, wash the whole screen in the success colour (for example, a green glow rising from the bottom), with the name and the reason in large type, and failures in the error colour with the reason. Close the confirmation by itself after about five seconds, with a button to close it sooner.
**Flag:** A small toast for the moment the whole flow is for, a result someone has to read up close, a confirmation that waits for a tap before the next person can go.

### F53. Every blocked state offers the way forward
**Rule:** When something stops people (expired, locked, over the limit), the same screen offers the fix.
**Apply:** An expired membership shows "Renew" right there, prefilled with the last plan. A full class offers the waiting list. Name the fix with a verb, and keep people where they are when it's done.
**Flag:** "Expired" or "Not allowed" with no action, a fix that lives in another part of the app, staff who have to leave the current screen to unblock someone.

### F54. Grace periods leave a note for the next person
**Rule:** When the rules allow an exception, it is a choice with a record, and the next person who meets the same case sees it.
**Apply:** For a short grace window (expired a day or two ago), offer two options: fix it now, or let it through once with a reminder. The reminder appears as a warning the next time that person is seen, for whoever is on shift, and the exception can't be used twice in a row.
**Flag:** Exceptions that leave no trace, warnings that only the person who made them can see, grace that can repeat forever, a hard stop where the business allows judgement.

### F55. If someone has to approve it, it's a request
**Rule:** Actions that need another party's approval are sent as requests with a visible status, not switched on directly.
**Apply:** "Request a pause" sends the request, shows it as Pending on the item, and tells the person when it is approved or declined. The other side gets an approve and decline queue. Never show an action as done before it is approved.
**Flag:** Buttons that look instant for things that need approval, requests with no status, approvals that happen without the requester hearing back.

### F56. Time-bound actions ask for the range
**Rule:** An action that lasts for a period asks for its start and end, not a single tap.
**Apply:** Pausing, holidays, bookings and suspensions open a from–to date picker with sensible limits and the length shown ("14 days"). Prefill the start with today.
**Flag:** A single "Pause" button with no dates, an end date that has to be set later somewhere else, ranges with no visible length.

### F57. The record leads its own page, and its actions sit on it
**Rule:** On a detail page the record itself is the main thing, and the actions for it (edit, delete, renew, pause) sit on the record.
**Apply:** Put the record's card first and largest, with edit and delete on it. Offer actions in the section they change (renewal inside Membership, pause on the membership row), and show their options only after the action is tapped, not up front.
**Flag:** A detail page where history or stats outrank the record, records that can't be edited or deleted, actions in a separate section away from what they change, option panels shown before anyone asks.

### F58. Feeds are pages; creating is a button
**Rule:** A stream people come back to (notifications, news, activity) is a page of its own, and making a new item is a button that opens a dialog.
**Apply:** Notifications open their own page from the bell, with the count on the bell. On a list page, put "New post" or "Add member" as the primary action top right (F2), opening a dialog or panel, and let the list fill the page. Put the most common creation action on the screen staff start their day on.
**Flag:** A notification stream squeezed into a home-screen section, a creation form permanently taking the top of a list, a common action buried in a sub-page.

### F59. Model the states the business really has
**Rule:** States, statuses and concepts on screen match how the business actually works. Don't invent ones it doesn't have.
**Apply:** Before adding a status, check it with the domain: if a membership is either paid or not, there is no "debt" to show. Remove states nobody uses, and name the rest the way staff say them.
**Flag:** Statuses that never apply, figures that are always zero because the concept doesn't exist, terms staff have to translate.

### F60. Show there's more sideways
**Rule:** A horizontal scroller shows that it scrolls.
**Apply:** Fade the edges where more content continues, let the last item peek, and scroll the selected item (today, the active filter) into view on load.
**Flag:** Horizontal rows that look complete, edges cut cleanly so nobody swipes, the selected item off screen.

### F61. Time looks like a calendar; summaries stay small
**Rule:** Things that happen at times (classes, bookings, shifts) are shown as a calendar, and history summaries take as little room as they can.
**Apply:** Use a week strip or week view with days across and times down, today marked and selected by default. Show past activity as a compact summary (a count and a small strip or month grid) that opens the full view on tap (F40).
**Flag:** Schedules as plain lists with dates repeated in each row, history grids that take over the screen, no sign of today.

### F62. Group long navigation
**Rule:** When a navigation has more than about seven items, it is grouped under short headings.
**Apply:** Group by job (for example, Today, People, Business, Settings), with small all-caps group labels and the most-used group first. Keep the account and staff profile at the bottom (F11).
**Flag:** Long flat sidebars, items grouped by how the code is built rather than by job, the same item in two groups.

### F63. Typing never waits on background work
**Rule:** Fields respond on the next frame, whatever the app is doing in the background.
**Apply:** Background refreshes and live updates must not re-render the form people are typing in; skip updates when nothing changed and keep input state local. Check by typing fast while live data is on.
**Flag:** Laggy or dropped keystrokes, cursors that jump, fields that reset when new data arrives.

### F64. Show the device side of the flow
**Rule:** When a flow depends on hardware (a card reader, a turnstile, a kiosk, a printer), the product shows what that device does, and a prototype simulates it.
**Apply:** Show the device's state on screen (reader ready, card read, door open) and, in demos and reviews, give a simulator that plays each outcome: valid, expired, unknown card. Use those same outcomes for testing.
**Flag:** Flows that assume the hardware just works, no way to demo or test a failed read, staff who can't tell whether the device is waiting or broken.

---

## Quick audit checklist

| Rule | Area | Check |
|---|---|---|
| F1 | Choice | One control per job, no duplicates |
| F2 | Navigation | Screen actions grouped top right, primary in the corner, apart from selectors |
| F3 | Choice | Secondary detail on demand, nothing lost |
| F4 | Feedback | Structured popovers: header, ordered rows, pointer highlight, flips, touch fallback |
| F5 | Accessibility | No removal leaves keyboard, touch or screen-reader users without a route |
| F6 | Choice | Each fact said once |
| F7 | Navigation | Count in the heading, follows filters, full figure on hover |
| F8 | Onboarding | Hints and help match current behaviour |
| F9 | Flows | No versions, design notes or internal jargon on screen; one form of address |
| F10 | Flows | Nothing claims more than the product's stated scope |
| F11 | Navigation | Account bottom of the nav with sign-out; notifications top right; both on mobile |
| F12 | Feedback | In-place confirmation at the same width |
| F13 | Flows | No step that repeats the choice that opened it |
| F14 | Choice | No controls that can't act here |
| F15 | Forms | Inline edits commit on Enter or blur, cancel on Escape |
| F16 | Navigation | One selection, one toolbar, gone on click-away |
| F17 | Choice | One option → just do it; inapplicable options left out |
| F18 | Destructive | Every creatable thing is removable |
| F19 | Destructive | Delete scopes named and previewed |
| F20 | Accessibility | Tooltips show name and shortcut; no browser-reserved shortcuts |
| F21 | Feedback | Cursor matches the available action |
| F22 | Navigation | Canvas tools stay screen-sized at every zoom |
| F23 | Feedback | AI proposals provisional, one decision pattern, instant accept |
| F24 | Feedback | Background AI status visible and inspectable |
| F25 | Feedback | Collaborators' cursors, names and selections shown |
| F26 | Forms | Cooldowns on the control; confirmations echo the input |
| F27 | Onboarding | Onboarding depth matches what people already know |
| F28 | Onboarding | Start and sign-in as equal doors |
| F29 | Onboarding | One question per screen, progress, back |
| F30 | Onboarding | Options as "I can…" statements or examples, "Other" when needed |
| F31 | Onboarding | Answers reflected back, next step's length stated |
| F32 | Onboarding | Value before the account, Apple/Google first, short form |
| F33 | Onboarding | Permissions in context with a clear "Not now" |
| F34 | States | Empty states that teach, with suggestions |
| F35 | Flows | Free path, dated trials, upgrades at the limit, plain terms |
| F36 | Onboarding | Tours after the first win, always skippable |
| F37 | Choice | Reading and picking steps in a narrow centred column |
| F38 | Navigation | Context and action pinned in long steps, nothing else sticky |
| F39 | Navigation | Filters beside the list, bottom sheet with Apply, active count |
| F40 | Choice | Compact overview first, full view on tap, "See all" in place |
| F41 | Feedback | Affordance on the cell or button that acts; no hover-only info |
| F42 | Choice | One- or two-word labels, definition on request |
| F43 | States | Missing data shown as N/A, never blank or zero |
| F44 | States | Line limits with ellipsis; sibling slots aligned |
| F45 | States | Checked with none, one, typical, many and longest values |
| F46 | Choice | Separate containers per kind; objects as cards; equal levels styled alike |
| F47 | Flows | Roles change home and scope, shared screens identical |
| F48 | Flows | Same picker for add and edit; empty selection opens it |
| F49 | Forms | Immediate on/off settings are toggles |
| F50 | Navigation | Same patterns, names and order on mobile and desktop |
| F51 | States | Limits shown as used of total, countable, coloured by what's left |
| F52 | Feedback | Key outcomes fill the screen and close themselves after about 5 s |
| F53 | Flows | Every blocked state offers its fix on the same screen |
| F54 | Flows | Grace exceptions are recorded and shown to the next person on shift |
| F55 | Flows | Approval-needing actions are requests with a status |
| F56 | Forms | Time-bound actions ask for a from–to range with the length shown |
| F57 | Choice | The record leads its page; actions sit on what they change |
| F58 | Navigation | Feeds are their own page; creating is a top-right button opening a dialog |
| F59 | Flows | Only the states the business really has |
| F60 | Navigation | Horizontal scrollers fade at the edges and show the selected item |
| F61 | Choice | Times as a calendar; history summaries compact, full view on tap |
| F62 | Navigation | Navigation over ~7 items grouped by job |
| F63 | Forms | Typing never lags or resets because of background updates |
| F64 | Feedback | Hardware steps shown on screen and simulated in demos |
