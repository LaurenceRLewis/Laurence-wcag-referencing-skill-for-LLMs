# Principle 2 — Operable

User interface components and navigation must be operable.

---

## Guideline 2.1 — Keyboard Accessible

### SC 2.1.1 — Keyboard (Level A)
**Intent:** All functionality is available via keyboard, without requiring specific timings for keystrokes.

**Passes when:**
- Every interactive element can be reached and activated with keyboard alone
- Custom widgets implement the correct keyboard interaction patterns (see ARIA APG)
- Drag-and-drop interactions have a keyboard alternative (see SC 2.5.7)

**Fails when:**
- Mouse-only event handlers (`onmousedown`, `onmouseover`) without keyboard equivalents
- Custom `<div>` or `<span>` used as interactive control without keyboard support
- Focus cannot reach a control via Tab or Arrow keys

**Exception:** Functionality where the underlying operation requires a path-dependent input (e.g. freehand drawing, handwriting) is exempt — but an alternative method should be provided where possible.

**WCAG 2.2 change:** No change.

**Related SC:** 2.1.2, 2.4.3, 4.1.2

---

### SC 2.1.2 — No Keyboard Trap (Level A)
**Intent:** Keyboard focus is never locked inside a component from which users cannot navigate away using standard keys.

**Passes when:**
- User can always navigate away from a component using Tab, Shift+Tab, Arrow keys, or Escape
- Modal dialogs that trap focus intentionally provide Escape or a visible close mechanism

**Fails when:** Focus enters a widget and there is no keyboard mechanism to leave it; pressing Tab cycles within the component indefinitely with no way out.

**Note:** Intentional focus trapping in modals is correct behaviour — the trap is acceptable as long as Escape or a close button exits and returns focus appropriately.

**WCAG 2.2 change:** No change.

---

### SC 2.1.3 — Keyboard (No Exception) (Level AAA)
**Intent:** All functionality operable via keyboard with no exceptions (stricter than 2.1.1 — path-dependent exceptions do not apply).

**WCAG 2.2 change:** No change.

---

### SC 2.1.4 — Character Key Shortcuts (Level A)
**Intent:** If keyboard shortcuts using only a single character key (letter, number, punctuation, symbol) are implemented, users can turn them off, remap them, or activate them only when a component has focus.

**Passes when:** Single-character shortcuts can be disabled or remapped; or are only active when the relevant component has focus.

**Fails when:** A single-character shortcut fires globally and cannot be turned off (interferes with speech input users who may inadvertently trigger shortcuts while dictating).

**WCAG 2.2 change:** No change.

---

## Guideline 2.2 — Enough Time

### SC 2.2.1 — Timing Adjustable (Level A)
**Intent:** For time limits set by content, users can: turn off the limit, adjust it (at least 10× default), or extend it with a warning (at least 20 seconds notice, extendable at least 10 times).

**Exception:** Real-time events (live auctions), essential time limits, time limits > 20 hours.

**Fails when:** Session times out without warning or without offering an extension.

**WCAG 2.2 change:** No change.

---

### SC 2.2.2 — Pause, Stop, Hide (Level A)
**Intent:** Moving, blinking, scrolling, or auto-updating content that starts automatically and lasts more than 5 seconds must have a pause/stop/hide mechanism — unless it's essential.

**Applies to:** Carousels, animated banners, auto-scrolling feeds, parallax effects, loading spinners (if shown for > 5 seconds).

**Passes when:** User can pause/stop/hide moving content; OR moving content lasts ≤ 5 seconds; OR movement is essential.

**WCAG 2.2 change:** No change.

---

### SC 2.2.3 — No Timing (Level AAA)
**Intent:** Timing is not an essential part of the event or activity (except real-time or essential situations).

**WCAG 2.2 change:** No change.

---

### SC 2.2.4 — Interruptions (Level AAA)
**Intent:** Interruptions (alerts, status updates) can be postponed or suppressed by the user, except for emergencies.

**WCAG 2.2 change:** No change.

---

### SC 2.2.5 — Re-authenticating (Level AAA)
**Intent:** When an authenticated session expires, users can continue after re-authenticating without losing their data.

**WCAG 2.2 change:** No change.

---

### SC 2.2.6 — Timeouts (Level AAA)
**Intent:** Users are warned of the duration of inactivity that will cause data loss, unless data is preserved for more than 20 hours.

**WCAG 2.2 change:** No change.

---

## Guideline 2.3 — Seizures and Physical Reactions

### SC 2.3.1 — Three Flashes or Below Threshold (Level A)
**Intent:** Content does not contain anything that flashes more than 3 times per second, or the flash is below the general flash and red flash thresholds.

**Fails when:** Animated GIFs, video, or JavaScript animations flash rapidly (> 3 Hz) without warning or mechanism to stop.

**WCAG 2.2 change:** No change.

---

### SC 2.3.2 — Three Flashes (Level AAA)
**Intent:** Content does not flash more than 3 times per second (stricter — no threshold exception).

**WCAG 2.2 change:** No change.

---

### SC 2.3.3 — Animation from Interactions (Level AAA)
**Intent:** Motion animation triggered by interaction can be disabled, unless essential.

**Passes when:** `prefers-reduced-motion` media query is respected; or no non-essential motion animation.

**WCAG 2.2 change:** No change.

---

## Guideline 2.4 — Navigable

### SC 2.4.1 — Bypass Blocks (Level A)
**Intent:** A mechanism exists to bypass blocks of content repeated on multiple pages.

**Passes when:** Skip navigation link at the top of each page; or landmark regions (`<main>`, `<nav>`) allow screen reader users to jump between sections.

**Fails when:** No skip link; no landmarks; screen reader or keyboard user must Tab through entire navigation on every page load.

**Best practice:** Both a visible (or focusable) skip link AND semantic landmarks.

**WCAG 2.2 change:** No change.

---

### SC 2.4.2 — Page Titled (Level A)
**Intent:** Web pages have titles that describe their topic or purpose.

**Passes when:** `<title>` element is present, unique, and describes the page (e.g. "Checkout — Acme Shop", not "Page 3" or "Untitled").

**Fails when:** `<title>` is empty, missing, generic, or identical across all pages.

**WCAG 2.2 change:** No change.

---

### SC 2.4.3 — Focus Order (Level A)
**Intent:** Focusable components receive focus in an order that preserves meaning and operability.

**Passes when:** Tab order follows the logical reading sequence (top to bottom, left to right in LTR languages); dialogs and dynamic content receive focus in a logical order when opened.

**Fails when:** `tabindex` values > 0 create an unintuitive tab order; dynamically inserted content appears at the end of the DOM but should logically appear earlier; focus jumps unpredictably.

**Best practice:** Never use `tabindex` values > 0. Rely on DOM order for focus sequence.

**WCAG 2.2 change:** No change.

---

### SC 2.4.4 — Link Purpose (In Context) (Level A)
**Intent:** The purpose of each link can be determined from the link text alone, or from the link text together with its surrounding context.

**Context allowed:** Same sentence, list item, table cell, or table header.

**Passes when:**
- "Download the 2024 Annual Report (PDF)" — clear from text alone
- A link within a product card where the heading provides context
- `aria-label` or `aria-labelledby` provides a more descriptive name

**Fails when:**
- "Click here", "Read more", "Learn more" without additional context or label
- Multiple "Read more" links on the same page referring to different articles

**WCAG 2.2 change:** No change.

**Related SC:** 2.4.9 (AAA — link text alone, no context allowed)

---

### SC 2.4.5 — Multiple Ways (Level AA)
**Intent:** More than one way to locate a page within a set of pages (except when a page is a step in a process).

**Passes when:** Site search AND navigation menu; or site map AND navigation; or breadcrumbs AND navigation.

**Fails when:** Single-page apps with only one route to each view; no search or site map.

**Exception:** A page that is a step in a process (checkout step 2 of 4) is exempt.

**WCAG 2.2 change:** No change.

---

### SC 2.4.6 — Headings and Labels (Level AA)
**Intent:** Headings and labels describe the topic or purpose of the content they introduce.

**Passes when:** Headings accurately describe the section; form labels clearly identify the input purpose.

**Fails when:** Generic headings like "Section 1", "Part A"; form labels like "Field 1", "Input".

**Note:** This SC does not require headings or labels to be present — that is SC 1.3.1 and SC 3.3.2. This SC requires them to be *descriptive* when they exist.

**WCAG 2.2 change:** No change.

---

### SC 2.4.7 — Focus Visible (Level AA)
**Intent:** Any keyboard-operable user interface has a visible keyboard focus indicator.

**Passes when:** When an element receives keyboard focus, there is a visible focus indicator (ring, outline, underline, or other visual change).

**Fails when:** `outline: none` or `outline: 0` applied globally with no replacement focus style; focus indicator has insufficient contrast (see SC 1.4.11 and SC 2.4.11).

**WCAG 2.2 change:** SC 2.4.11 and 2.4.13 add further requirements in 2.2. 2.4.7 only requires focus to be *visible* — not a specific size or contrast level (that is 2.4.11/2.4.13).

**Related SC:** 2.4.11, 2.4.12, 2.4.13, 1.4.11

---

### SC 2.4.8 — Location (Level AAA)
**Intent:** Information about the user's location within a set of pages is available (e.g. breadcrumbs, site map highlighting current page).

**WCAG 2.2 change:** No change.

---

### SC 2.4.9 — Link Purpose (Link Only) (Level AAA)
**Intent:** The purpose of each link can be identified from the link text alone (stricter than 2.4.4 — no surrounding context allowed).

**WCAG 2.2 change:** No change.

---

### SC 2.4.10 — Section Headings (Level AAA)
**Intent:** Section headings are used to organise content.

**WCAG 2.2 change:** No change.

---

### SC 2.4.11 — Focus Not Obscured (Minimum) (Level AA) ← NEW in WCAG 2.2
**Intent:** When a UI component receives keyboard focus, it is not entirely hidden by author-created content (e.g. sticky headers, cookie banners, chat widgets).

**Passes when:** At least part of the focused component is visible (not entirely covered by another element).

**Fails when:** A sticky footer or header completely covers the focused element; a cookie consent banner sits over the focused component.

**Note:** This SC allows *partial* obscuring — the component just must not be *entirely* hidden. SC 2.4.12 (AAA) requires the focused element to be fully visible.

**WCAG 2.2 change:** NEW in WCAG 2.2.

**Related SC:** 2.4.7, 2.4.12, 2.4.13

---

### SC 2.4.12 — Focus Not Obscured (Enhanced) (Level AAA) ← NEW in WCAG 2.2
**Intent:** When a UI component receives keyboard focus, no part of it is hidden by author-created content (stricter than 2.4.11).

**WCAG 2.2 change:** NEW in WCAG 2.2.

---

### SC 2.4.13 — Focus Appearance (Level AAA) ← NEW in WCAG 2.2
**Intent:** The keyboard focus indicator meets minimum size and contrast requirements.

**Requirements:**
- The focus indicator area is at least as large as a 2px perimeter around the unfocused component
- The focus indicator has at least 3:1 contrast ratio between focused and unfocused states

**Passes when:** A 2px outline with ≥ 3:1 contrast against the adjacent colours.

**Fails when:** A 1px outline with low contrast; an indicator that is too small to be meaningful.

**WCAG 2.2 change:** NEW in WCAG 2.2.

**Related SC:** 2.4.7, 2.4.11, 1.4.11

---

## Guideline 2.5 — Input Modalities

### SC 2.5.1 — Pointer Gestures (Level A)
**Intent:** All functionality that uses multipoint or path-based gestures (pinch-to-zoom, swipe) has a single-pointer alternative.

**Passes when:** Map zoom available via +/− buttons; carousel navigable by button as well as swipe.

**Fails when:** Swipe-only interaction with no button alternative; pinch-zoom required with no alternative.

**WCAG 2.2 change:** No change.

---

### SC 2.5.2 — Pointer Cancellation (Level A)
**Intent:** For single-pointer actions, at least one of: no down-event trigger, ability to abort/undo, up-event reversal, or essential exception.

**Intent:** Prevent accidental activation — actions should fire on the up-event (mouse-up, touch-end), not down-event, so users can cancel by moving the pointer away.

**Passes when:** Click fires on mouseup/pointerup; user can drag away before releasing to cancel.

**Fails when:** Action fires immediately on mousedown/touchstart with no cancellation option.

**WCAG 2.2 change:** No change.

---

### SC 2.5.3 — Label in Name (Level A)
**Intent:** For UI components with visible text labels, the accessible name includes the visible label text.

**Passes when:** A button labelled "Search" has `aria-label="Search"` or no aria-label (uses visible text). The visible text is contained within the accessible name.

**Fails when:** A button with visible text "Search" has `aria-label="Find"` — the visible text is not in the accessible name, breaking speech input ("click Search" won't work).

**WCAG 2.2 change:** No change.

---

### SC 2.5.4 — Motion Actuation (Level A)
**Intent:** Functionality triggered by device motion (shake, tilt) can also be activated via UI controls, and the motion response can be disabled.

**Passes when:** Shake-to-undo has a UI button alternative; motion control can be turned off.

**Fails when:** Only way to trigger an action is device motion; motion cannot be disabled (problematic for users who mount devices or have tremors).

**WCAG 2.2 change:** No change.

---

### SC 2.5.5 — Target Size (Enhanced) (Level AAA)
**Intent:** The size of the target for pointer inputs is at least 44×44 CSS pixels.

**Exception:** Inline links within text; target size determined by user agent; essential styling.

**WCAG 2.2 change:** No change. (SC 2.5.8 in 2.2 is the new AA-level target size requirement.)

---

### SC 2.5.6 — Concurrent Input Mechanisms (Level AAA)
**Intent:** Content does not restrict use of input modalities available on a platform, except where essential.

**Passes when:** User can switch between keyboard, mouse, and touch without the application restricting or disabling any.

**WCAG 2.2 change:** No change.

---

### SC 2.5.7 — Dragging Movements (Level AA) ← NEW in WCAG 2.2
**Intent:** All functionality that uses a dragging movement can also be achieved with a single pointer without dragging, unless dragging is essential.

**Applies to:** Drag-and-drop interfaces, range sliders dragged by thumb, sortable lists.

**Passes when:**
- Drag-and-drop sortable list also has up/down buttons for reordering
- Slider thumb can be moved by clicking a position, not only by dragging
- Drag target has a click or keyboard alternative

**Fails when:** Dragging is the only way to complete an action with no single-pointer or keyboard alternative.

**WCAG 2.2 change:** NEW in WCAG 2.2.

**Related SC:** 2.1.1, 2.5.1

---

### SC 2.5.8 — Target Size (Minimum) (Level AA) ← NEW in WCAG 2.2
**Intent:** The size of the target for pointer inputs is at least 24×24 CSS pixels.

**Requirements:** Target is at least 24×24 CSS pixels, OR there is at least 24px of spacing around the target such that the spacing + target covers a 24×24 area.

**Exception:**
- Inline links in text (target size determined by line height)
- User agent controls not modified by author
- Essential presentation (the size is required by the information)

**Passes when:** Buttons, links, checkboxes, and interactive controls are at least 24×24px; OR adequate spacing around smaller targets.

**Fails when:** Icon buttons are 16×16px with no spacing; small checkbox targets with insufficient padding.

**Note:** The AAA equivalent (SC 2.5.5) requires 44×44px. 2.5.8 is the new minimum AA threshold.

**WCAG 2.2 change:** NEW in WCAG 2.2.

**Related SC:** 2.5.5
