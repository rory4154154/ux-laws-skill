---
name: ux-laws
description: Apply five laws of UX (Jakob's law, Hick's law, Fitts's law, the Doherty threshold and Tesler's law) whenever building, designing, reviewing or changing an app, website, dashboard, form, screen, component or any user-facing interface. Use for "build me an app", "make a UI", "add a page/screen/form", "create a landing page", "review this interface", or any frontend work in React, Vue, Svelte, HTML, React Native, SwiftUI or Flutter. Stops the usual AI defaults: non-standard layouts, too many buttons, tiny tap targets, laggy interactions, and pushing complexity onto the user.
---

# UX Laws

Five laws every interface you build must obey. They are not style preferences. Each one targets a mistake you make by default when generating UI, so treat them as hard constraints, apply them while you build (not as a pass afterwards), and run the checklist at the end before handing anything back.

If the user explicitly asks for something that breaks a law, do it, but say in one line which law it breaks and what it will cost.

---

## 1. Jakob's law: work like the apps people already use

**The law.** People spend most of their time on other apps, so they expect yours to work the same way. Familiar patterns cost zero learning. Novel ones make people hunt, and if your login button is somewhere weird, they genuinely get lost.

**Your default failure.** Inventing "creative" layouts, renaming standard things, moving navigation, or building custom controls where a native one exists.

**Do this:**
- Put things where convention puts them. Logo top-left linking home. Primary nav top (web) or bottom tab bar (mobile). Account, profile and login top-right. Search top, near the centre or right. Cart top-right. Settings behind the profile or a gear. Footer holds legal, contact and secondary links.
- Use standard words: "Log in", "Sign up", "Search", "Settings", "Save", "Cancel", "Delete", "Back". Not "Enter the portal", "Begin your journey", "Commit".
- Use native or standard controls: real `<button>`, `<a>`, `<input>`, `<select>`, checkboxes, toggles, date pickers. Don't rebuild a dropdown out of divs.
- Keep standard behaviours working: links are links (open in new tab works), back button works, Enter submits forms, Escape closes modals, clicking the overlay closes a modal, the browser can autofill email and password fields (correct `type` and `autocomplete` attributes).
- Follow the platform. iOS follows Apple's Human Interface Guidelines, Android follows Material, web follows web conventions. Don't put an iOS-style back chevron in a web app's top-left by habit.
- Icons only for meanings everyone shares (search, close, menu, home, settings, trash, share). Anything else gets a text label.
- Stay consistent inside the app too: the same action looks and sits the same way on every screen.

**Don't:** hide navigation behind a hamburger on desktop, use hover-only reveals for anything important, scroll-jack, or make the user learn a gesture to do something basic.

---

## 2. Hick's law: fewer choices, faster decisions

**The law.** The more choices you give someone, the longer they take to pick one. You love adding twelve buttons. Cut it to three.

**Your default failure.** Exposing every feature at once: rows of equal-weight buttons, toolbars full of icons, settings pages with forty toggles, forms asking for everything up front.

**Do this:**
- One primary action per screen. Make it visually dominant (filled, brand colour). Everything else is secondary (outline or ghost) or tertiary (text link). If you can't name the one thing this screen exists for, the screen is doing too much.
- Aim for three or fewer visible actions in any one group. Move the rest into a "More" menu, an overflow (`...`), or a later step.
- Progressive disclosure: show the common path, hide the advanced. "Advanced options" collapsed by default.
- Break long forms into steps, and only ask for what you need right now. Shipping address can wait until checkout.
- Navigation: around five top-level items, not ten. Group the rest.
- Pricing and plan pickers: three options at most, with one marked as recommended.
- Pre-select the most likely choice so the decision becomes "confirm" instead of "choose".
- Long lists of options (countries, categories) get search or type-ahead, not a giant dropdown.

**Don't:** add a button because the feature exists. Every visible control must earn its place. When in doubt, cut it and say what you cut.

---

## 3. Fitts's law: big targets, close to the hand

**The law.** The time to hit a target depends on how big it is and how far away it is. Big buttons close to your thumb get clicked. Tiny ones in the corner don't.

**Your default failure.** Small icon buttons, text-only links as the main action, primary buttons tucked into corners, and important actions placed far from where the user's attention or thumb already is.

**Do this:**
- Minimum hit area 44x44 px (Apple HIG: 44pt; Material: 48dp). The visible icon can be smaller, but pad the clickable area to the minimum. Never go below 24x24 px (WCAG 2.2 AA).
- At least 8 px between adjacent tap targets so people don't hit the wrong one.
- Primary actions are the largest buttons on the screen. On mobile, make the main CTA full-width or close to it and put it in the bottom third, in the thumb zone. Sticky bottom bars beat top-right buttons on phones.
- Put the action next to the thing it acts on: "Save" at the end of the form, "Add to cart" beside the price, row actions on the row.
- Make the whole card, row or list item clickable, not just the small title text inside it. Labels on checkboxes and radios must be clickable (`<label for>`).
- Keep destructive actions small, separated and away from the primary action, and confirm or allow undo. Fitts cuts both ways: make what you want clicked easy, and what you don't want clicked by accident harder.

**Don't:** make the main action a 12 px text link, put a lone "Next" button in the top-right on mobile, or place "Delete" right next to "Save" at the same size.

---

## 4. Doherty threshold: respond in under 400 ms

**The law.** When a system responds in under about 400 milliseconds, people stay engaged and in flow. Past that, they feel it lagging and start losing focus.

**Your default failure.** Waiting for the server before showing anything, full-page spinners, blocking the UI during saves, no feedback on clicks, and shipping heavy bundles that make first load slow.

**Do this:**
- Acknowledge every input instantly (within about 100 ms): pressed state, ripple, button switches to a loading state, the item appears in the list.
- Optimistic UI for likely-to-succeed actions (likes, toggles, adding to a list, reordering, sending a message): update the screen immediately, sync in the background, roll back with a clear message if it fails.
- Skeleton screens shaped like the real content instead of a blank page with a spinner. Use a spinner only for small inline waits.
- Anything over about 1 second gets visible progress. Anything over about 10 seconds gets a progress bar or step indicator, and the user can keep doing other things or cancel.
- Disable the submit button while submitting to stop double-submits, but keep the label readable ("Saving...").
- Prefetch and cache: load the next likely screen on hover or in the background, cache API responses, debounce search inputs (around 200-300 ms) rather than firing a request on every keystroke and waiting for each.
- Keep it light: lazy-load routes and heavy components, compress and size images properly, don't pull in a large library for one function.
- Animations and transitions run 150-300 ms. Never make the user wait for decoration.

**Don't:** block the whole screen for a background save, show nothing while data loads, or chain sequential API calls that could run in parallel.

---

## 5. Tesler's law: you absorb the complexity, not the user

**The law.** Every app has some complexity that can't be removed. The only question is whether the system deals with it or the user does. You will always push it onto the user unless told otherwise. You are being told otherwise.

**Your default failure.** Making the user do work the code could do: typing data that could be inferred, picking formats, remembering things, configuring before they can start, decoding raw error messages, and fixing input to match a strict format.

**Do this:**
- Smart defaults everywhere. Detect timezone, locale, currency and country. Pre-fill what you already know. The app works with zero configuration; settings are for changing defaults, not establishing them.
- Accept input the way people type it. Phone numbers with spaces or dashes, dates in common formats, card numbers with or without spaces, emails with trailing whitespace. Normalise in code, don't reject.
- Infer instead of asking: card type from the number, city from the postcode, name from the email sign-in.
- Validate inline as the user goes (on blur), with errors written in plain language that say how to fix it. "Password needs at least 8 characters" not "Invalid input" or `ERR_VALIDATION_422`.
- Never lose user work. Autosave drafts, preserve form input on errors and navigation, make destructive actions undoable.
- Remember things: last-used options, previous inputs, where they left off.
- Handle the edge cases in code: empty states that explain what to do next, retries for flaky network calls, graceful offline behaviour, sensible handling of duplicates.
- When some complexity genuinely must reach the user, make it as small as possible: one clear decision with a recommended default, not a configuration screen.

**Don't:** ship a setup wizard when defaults would do, expose internal IDs, enums or stack traces, or make the user re-enter anything the app has already seen.

---

## When the laws pull against each other

- **Hick vs Tesler.** Cutting options must not dump work on the user. Don't remove a choice by forcing a manual workaround; remove it by choosing a smart default.
- **Hick vs Fitts.** Fewer, bigger targets beats many small ones. If three things don't fit at a good size, that's a sign to cut to fewer.
- **Jakob vs everything.** Convention wins unless breaking it clearly removes work for the user. "Looks more unique" is never a reason.
- **Doherty vs correctness.** Optimistic updates only for actions that almost always succeed and can be rolled back. Payments, deletions and irreversible actions wait for confirmation, but still show instant feedback that something is happening.

---

## Checklist before you hand back any UI

Go through every screen you built or changed. Fix failures before responding; don't just list them.

**Jakob**
- [ ] Logo, nav, login/account, search and cart are where users expect them
- [ ] Standard labels and native controls; back, Enter, Escape and autofill all work
- [ ] Same action looks the same on every screen

**Hick**
- [ ] Each screen has exactly one visually dominant primary action
- [ ] No group shows more than about three equal-weight actions
- [ ] Advanced options are collapsed; forms only ask what's needed now

**Fitts**
- [ ] Every tap target is at least 44x44 px with 8 px gaps
- [ ] Mobile primary CTA is large and in the thumb zone
- [ ] Whole rows/cards are clickable; destructive actions are small and apart

**Doherty**
- [ ] Every click gets feedback within about 100 ms
- [ ] Loads use skeletons; likely-to-succeed actions are optimistic
- [ ] Waits over 1 second show progress; nothing blocks the whole screen unnecessarily

**Tesler**
- [ ] Works with zero configuration via smart defaults
- [ ] Input is accepted in any reasonable format and normalised in code
- [ ] Errors are plain-language and say how to fix; user work is never lost

When you report back, add one short line per law only where you made a notable call (what you cut, what you defaulted, what you moved). Don't pad it.
