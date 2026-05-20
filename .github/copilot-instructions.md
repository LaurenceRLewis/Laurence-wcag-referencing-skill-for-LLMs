# Accessibility Standards and Code Conventions

## Conformance Target

This project targets **WCAG 2.2 Level AA** conformance.

All new components and modifications to existing components must be assessed against WCAG 2.2 AA. Do not assume WCAG 2.1 equivalence without checking for new 2.2 criteria (2.4.11, 2.4.12, 2.4.13, 2.5.7, 2.5.8, 3.2.6, 3.3.7, 3.3.8, 3.3.9).

Specification reference: https://www.w3.org/TR/WCAG22/

---

## ARIA Specification Versions

- Normative ARIA reference: **WAI-ARIA 1.2** — https://www.w3.org/TR/wai-aria-1.2/
- ARIA in HTML (role/attribute allowances): https://www.w3.org/TR/html-aria/
- Accessible Name computation: **AccName 1.2** — https://www.w3.org/TR/accname-1.2/
- ARIA Authoring Practices Guide (patterns, non-normative): https://www.w3.org/WAI/ARIA/apg/

WAI-ARIA 1.3 is a Working Draft. Do not treat it as normative. If referencing it, flag it explicitly.

---

## Priority WCAG Success Criteria

These criteria are most relevant to the component types in this project. Apply them by default when writing or reviewing UI code.

| SC | Name | Level |
|---|---|---|
| 1.1.1 | Non-text Content | A |
| 1.3.1 | Info and Relationships | A |
| 1.3.5 | Identify Input Purpose | AA |
| 1.4.3 | Contrast (Minimum) | AA |
| 1.4.4 | Resize Text | AA |
| 1.4.10 | Reflow | AA |
| 1.4.11 | Non-text Contrast | AA |
| 1.4.13 | Content on Hover or Focus | AA |
| 2.1.1 | Keyboard | A |
| 2.1.2 | No Keyboard Trap | A |
| 2.4.3 | Focus Order | A |
| 2.4.7 | Focus Visible | AA |
| 2.4.11 | Focus Appearance | AA |
| 2.5.3 | Label in Name | A |
| 3.2.2 | On Input | A |
| 3.3.1 | Error Identification | A |
| 3.3.2 | Labels or Instructions | A |
| 4.1.2 | Name, Role, Value | A |
| 4.1.3 | Status Messages | AA |

Full criterion text: https://www.w3.org/TR/WCAG22/

---

## AT Behaviour Notes

These notes reflect real-world AT behaviour that is not fully defined by specification. Treat them as tested observations, not normative requirements.

### aria-activedescendant

- Only valid on elements with roles: `combobox`, `grid`, `group`, `listbox`, `menu`, `menubar`, `radiogroup`, `row`, `rowgroup`, `textbox`, `tree`, `treegrid`.
- JAWS and NVDA differ in how they announce `aria-activedescendant` changes. NVDA reads the referenced element directly; JAWS may announce the container role first. Test both.
- Do not use `aria-activedescendant` as a substitute for actual focus management unless the pattern genuinely requires it (e.g. combobox listbox).

### aria-live and status messages (4.1.3)

- `aria-live="polite"` is preferred for most status messages. Use `assertive` only for genuine errors or time-sensitive information.
- Inject live region content dynamically after the region is rendered, not simultaneously. Some AT will not announce content present in the DOM on page load.
- Render the live region container on page load and update its text content. Do not insert and remove the container dynamically, as AT may miss the announcement if the region was not present in the DOM when the content appeared.
- iOS VoiceOver does not reliably announce `role="status"` without an explicit `aria-live="polite"` attribute. Always pair them.

### dialog element

- Native `<dialog>` exposes the `dialog` role to AT automatically. Do not add `role="dialog"` redundantly.
- `aria-modal="true"` on `<dialog>` is required for some AT (particularly JAWS) to restrict the virtual cursor to the dialog. However, iOS VoiceOver has inconsistent support. Test on both platforms.
- When `showModal()` is used, the browser manages focus trapping in some user agents. Do not assume it is complete. Implement explicit focus management for all modal dialogs.
- Blocking `Escape` key dismissal should be scoped to specific dialogs where it is intentional. Do not suppress it globally.

### Popover API

- Native popover elements do not automatically expose tooltip semantics to AT. ARIA is required if the popover serves as a tooltip (`role="tooltip"`, `aria-describedby` on the trigger).
- Browser AT exposure of popover without ARIA is not yet consistent. If AT announcement is required, do not rely on native exposure alone.

### iOS VoiceOver

- Dynamic toggling of `aria-expanded`, `aria-hidden`, and `aria-disabled` is generally supported but can be slow to announce. Test with actual VoiceOver, not emulated.
- `aria-modal="true"` has known support gaps on older iOS versions. Verify against the minimum supported iOS version for this project.

---

## Testing Stack

When advising on AT behaviour or suggesting implementation approaches, use this testing matrix as the reference environment.

| AT | Browser | Platform |
|---|---|---|
| NVDA (latest) | Chrome (latest) | Windows |
| JAWS (latest) | Chrome (latest) | Windows |
| VoiceOver | Safari (latest) | iOS (latest) |
| VoiceOver | Safari (latest) | macOS (latest) |
| TalkBack | Chrome (latest) | Android (latest) |

If a suggested pattern has known issues in any of these environments, state that explicitly before recommending it.

---

## Code Style and Conventions

These conventions apply to all HTML, TypeScript, JavaScript, and SCSS in this project.

### First Rule of ARIA

If a native HTML element exists that provides the required semantics and behaviour, use it. Do not use ARIA to replicate what native HTML already does. ARIA is for filling gaps that native HTML cannot cover.

### Native Elements Over ARIA Roles

- Always use native `<button>` for interactive controls. Never use `<div role="button">` or `<span role="button">`.
- Never add `role="button"` to a native `<button>` element. The role is implicit and the redundant attribute adds noise without benefit.
- Never add `role="dialog"` to a native `<dialog>` element. The role is implicit.
- Never add `role="navigation"` to `<nav>`, `role="main"` to `<main>`, `role="banner"` to `<header>`, or `role="contentinfo"` to `<footer>`. All landmark roles are implicit on their native elements.
- Use `<a href>` for navigation to a URL. Use `<button>` for triggering an action. Do not use `<a>` without an `href` as a button substitute.
- Do not use `placeholder` as a label substitute. Always provide a visible `<label>` element associated via `for` and `id`.

### Why native `<button>` is required

A native `<button>` provides all of the following without additional code:

- Focusable by default, no `tabindex` required.
- Activated by both Enter and Space keys natively.
- Correct `button` role exposed to the accessibility tree automatically.
- `disabled` attribute sets AT semantics, removes from tab order, and blocks click events simultaneously.
- Participates in form submission and reset without JavaScript.
- Click events fire on keyboard activation without additional handlers.
- Consistent AT announcements across NVDA, JAWS, VoiceOver, and TalkBack.

A `<div role="button">` requires manual implementation of every item in the list above and is still less reliable across AT.

### General

- Prefer minimal, targeted changes over broad rewrites. Change only what is necessary to achieve the outcome.
- Prefer CSS-only solutions where they are sufficient and do not compromise accessibility.
- Do not introduce new dependencies to solve problems that can be solved with existing browser APIs or native HTML elements.

### Focus Management

- After a modal or dialog opens, move focus to the first focusable element or the dialog container.
- After a modal or dialog closes, return focus to the trigger element that opened it.
- After dynamic content updates that change the page context, move focus to a consistent landmark or heading so AT users are oriented.
- Update `document.title` to reflect the current page or view on every significant navigation or context change.
- Hold references to trigger elements before opening overlays or dialogs so focus can be reliably returned on close.

### TypeScript and JavaScript

- Use named `const` references for DOM elements rather than repeated `querySelector` calls.
- Apply null guards on all DOM queries before use. Do not assume an element exists.
- Use capture-phase event listeners (`addEventListener(type, handler, true)`) where event delegation or ordering requires it. Document why capture phase is used in a comment.
- Remove attributes cleanly using `removeAttribute()` rather than setting empty strings or `null`.
- Prefer `addEventListener` and `removeEventListener` over inline event handlers.
- Clean up event listeners when the component or view is destroyed to prevent memory leaks and duplicate handler registration.

### HTML

- Use native HTML elements and their built-in semantics before reaching for ARIA. See Native Elements Over ARIA Roles above.
- Do not use ARIA to override native semantics unless there is a documented, tested reason.
- Dynamic ARIA attribute changes (`aria-expanded`, `aria-hidden`, etc.) should be driven by state. Centralise attribute updates rather than scattering them across multiple event handlers.

### SCSS

- Use the `@use` / `@forward` module system. Do not use `@import`.
- Keep accessibility-related styles (focus rings, forced-colors overrides, `prefers-reduced-motion`) in clearly named partials, not mixed into component styles.
- `:focus-visible` is preferred over `:focus` for keyboard focus styles. Use both only where legacy browser support requires it.

---

## Component Standards: Forms

### Relevant WCAG Success Criteria

| SC | Name | Level |
|---|---|---|
| 1.3.1 | Info and Relationships | A |
| 1.3.5 | Identify Input Purpose | AA |
| 2.4.6 | Headings and Labels | AA |
| 3.3.1 | Error Identification | A |
| 3.3.2 | Labels or Instructions | A |
| 3.3.3 | Error Suggestion | AA |
| 3.3.4 | Error Prevention | AA |
| 4.1.2 | Name, Role, Value | A |
| 4.1.3 | Status Messages | AA |

### Labels

- Every input must have a visible, persistent label associated via `<label for>` and the input `id`. Never rely on `placeholder` as a label substitute.
- Do not use `aria-label` or `aria-labelledby` as a replacement for a visible label unless the design explicitly and intentionally omits a visible label and there is a documented reason.
- Group related inputs (radio buttons, checkboxes) in a `<fieldset>` with a `<legend>`.
- For composite inputs (e.g. date split across day, month, year fields), wrap in a `<fieldset>` and `<legend>` to provide the group context to AT.

### Input Purpose (1.3.5)

- Apply `autocomplete` attributes to all inputs that collect personal information.
  Common values: `name`, `email`, `tel`, `street-address`, `postal-code`, `bday`, `current-password`, `new-password`.
- Do not suppress autocomplete on personal data fields without a documented security reason.

### Instructions and Hints

- Place format instructions or hints in a visible element before the input, not after.
- Associate hints with the input using `aria-describedby`. The hint element must have a unique `id`.
- Do not put critical instructions only in `placeholder`. Placeholder disappears on input and is not reliably announced by all AT on focus.
- Example pattern:

```html
  <label for="dob">Date of birth</label>
  <p id="dob-hint">Use the format DD/MM/YYYY</p>
  <input type="text" id="dob" aria-describedby="dob-hint" autocomplete="bday">
```

### Inline Validation and Error Handling

- Do not validate on every keystroke. Validate on blur or on form submission.
- Error messages must be visible, persistent, and specific. State what is wrong and how to fix it.
- Associate error messages with their input using `aria-describedby`. Append the error id to any existing `aria-describedby` value as a space-separated list.
- Set `aria-invalid="true"` on the input when an error is present. Remove it when the error is resolved. Omit `aria-invalid` entirely until validation has run.
- Error messages must be injected into the DOM dynamically after validation runs, not pre-rendered with empty content.
- Example pattern:

```html
  <label for="email">Email address</label>
  <input type="email" id="email" aria-describedby="email-hint email-error"
    aria-invalid="true" autocomplete="email">
  <p id="email-hint">We will use this to send your confirmation.</p>
  <p id="email-error" role="alert">
    Enter an email address in the format name@example.com
  </p>
```

### Summary Error Pattern

- On form submission with multiple errors, inject a summary at the top of the form listing all errors as links that move focus to the relevant input when activated.
- The summary container should use `role="alert"` or `aria-live="assertive"` so AT announces it immediately on injection.
- Move focus to the summary container after injection so keyboard users are oriented.

### Required Fields

- Use the native `required` attribute on inputs.
- Do not use only `aria-required="true"` in place of the native `required` attribute unless a specific support issue requires it. Document the reason if so.
- Indicate required fields visually. If using an asterisk, include a legend above the form explaining the convention.
- Do not mark every field as required if all fields are required. State "All fields are required" once at the top of the form instead.

### Disabled and Read-only States

- Use the native `disabled` attribute for inputs the user cannot interact with.
- Do not use `aria-disabled="true"` as a substitute for `disabled` unless you need the element to remain focusable. Document the reason if so.
- Use `readonly` for inputs the user can read and copy but not edit.

### Select and Custom Dropdowns

- Use native `<select>` wherever possible.
- Only build a custom dropdown when the native `<select>` genuinely cannot meet the design requirement. Document the reason.
- Custom dropdowns must implement the ARIA combobox or listbox pattern per the APG: https://www.w3.org/WAI/ARIA/apg/patterns/combobox/

### Checkboxes and Radio Buttons

- Use native `<input type="checkbox">` and `<input type="radio">`.
- Always wrap groups in `<fieldset>` and `<legend>`.
- Individual labels should describe the specific option, not repeat the group label.

---

## Component Standards: Dialog

### Relevant WCAG Success Criteria

| SC | Name | Level |
|---|---|---|
| 1.3.1 | Info and Relationships | A |
| 2.1.1 | Keyboard | A |
| 2.1.2 | No Keyboard Trap | A |
| 2.4.3 | Focus Order | A |
| 2.4.11 | Focus Appearance | AA |
| 4.1.2 | Name, Role, Value | A |

### Element Choice

- Use the native `<dialog>` element for all modal and non-modal dialog patterns.
- Do not build dialogs using `<div role="dialog">` unless there is a documented, tested reason. Document the reason.
- Do not add `role="dialog"` redundantly to a native `<dialog>` element.

### Modal vs Non-modal

- Use `dialog.showModal()` for modal dialogs.
- Use `dialog.show()` for non-modal dialogs.
- Never simulate modal behaviour on a non-modal dialog or vice versa.

### Labelling

- Every dialog must have an accessible name.
- Preferred pattern: a visible heading with `aria-labelledby` on the `<dialog>` pointing to the heading `id`.
- If the dialog has a description, associate it using `aria-describedby` on the `<dialog>` element.
- Example pattern:

```html
  <dialog aria-labelledby="dialog-title" aria-describedby="dialog-desc">
    <h2 id="dialog-title">Confirm deletion</h2>
    <p id="dialog-desc">
      This action cannot be undone. The item will be permanently removed.
    </p>
  </dialog>
```

### aria-modal

- Add `aria-modal="true"` to modal dialogs opened with `showModal()`.
- Do not add `aria-modal="true"` to non-modal dialogs.
- iOS VoiceOver has inconsistent support for `aria-modal="true"`. Test on the minimum supported iOS version. Document any workaround in the Known Gaps section below.

### Focus Management on Open

- Move focus inside the dialog immediately when it opens.
- Preferred target: the first interactive element inside the dialog.
- Alternative: the dialog container itself with `tabindex="-1"` if no interactive element is the logical first focus target.
- Do not move focus to the close button by default unless it is genuinely the most logical first action.
- Move focus only after the dialog is visible in the DOM.

### Focus Trapping in Modal Dialogs

- Implement explicit focus trapping as a supplement to native `showModal()` trapping.
- Focus trap must cycle between the first and last focusable elements on Tab and Shift+Tab.
- Do not use `tabindex` values greater than 0.

### Focus Management on Close

- Return focus to the trigger element when the dialog closes.
- Store a reference to the trigger before opening the dialog.
- If the trigger no longer exists on close, move focus to the nearest logical parent or the main heading. Document this fallback in code comments.

### Escape Key Handling

- Modal dialogs must close on Escape by default.
- Only block Escape when there is a specific documented reason. Scope the block to that dialog instance only.
- Never suppress Escape globally across all dialogs.

### Close Mechanism

- Every dialog must have an explicit close control.
- The close button must have an accessible name. An icon-only button with no accessible name fails 4.1.2.
- Place the close button in a consistent location, top right of the dialog header is the established convention.

### Backdrop Click Dismissal

- Backdrop click is an acceptable supplementary dismissal mechanism but must not be the only one.
- Distinguish between clicks on the `<dialog>` element itself (the backdrop) and clicks on its children (the content).

### Non-modal Dialog Specifics

- Non-modal dialogs must not trap focus.
- Do not add `aria-modal="true"` to non-modal dialogs.
- Non-modal dialogs should close when focus moves outside them or provide a clear close mechanism.

### AT Behaviour Notes Specific to Dialog

- NVDA in browse mode may read outside a modal dialog if `aria-modal="true"` is absent. Always include it on modal dialogs.
- JAWS requires `aria-modal="true"` to restrict the virtual cursor. Without it JAWS users can navigate outside the dialog using virtual cursor keys even when focus is trapped.
- VoiceOver on iOS may not fully respect `aria-modal="true"`. Test swipe navigation to confirm AT users cannot reach background content.
- TalkBack on Android generally respects focus trapping when `showModal()` is used. Test swipe navigation as well as linear focus order.

---

## Specification Sources

When in doubt, refer to the specification rather than blog posts or tutorials. These are the canonical sources for this project.

| Topic | Source |
|---|---|
| WCAG 2.2 | https://www.w3.org/TR/WCAG22/ |
| WAI-ARIA 1.2 | https://www.w3.org/TR/wai-aria-1.2/ |
| ARIA in HTML | https://www.w3.org/TR/html-aria/ |
| AccName 1.2 | https://www.w3.org/TR/accname-1.2/ |
| HTML Living Standard | https://html.spec.whatwg.org/multipage/ |
| DOM Living Standard | https://dom.spec.whatwg.org/ |
| CSS Anchor Positioning (WD) | https://www.w3.org/TR/css-anchor-position-1/ |
| Sass | https://sass-lang.com/documentation/ |

Expert opinion sources (Adrian Roselli, Scott O'Hara, Léonie Watson, TPGi) are useful for real-world AT behaviour guidance but are not normative. Distinguish between specification requirements and expert recommendations when advising.

---

---

## Content Writing Standards: WCAG AAA Guidance

This section covers WCAG 2.2 AAA success criteria that directly affect how content is
written. AAA is not the project conformance target. Apply these criteria where possible
and flag deliberate departures in the Known Gaps section below.

| SC | Name | Level |
|---|---|---|
| 3.1.3 | Unusual Words | AAA |
| 3.1.4 | Abbreviations | AAA |
| 3.1.5 | Reading Level | AAA |
| 3.1.6 | Pronunciation | AAA |

---

### 3.1.3 Unusual Words (AAA)

- Provide definitions for technical terms, jargon, idioms, and words used in an unusual
  or restricted way.
- Preferred approaches in order of preference: define the term inline on first use,
  provide a glossary linked from the page, use the HTML `<dfn>` element to mark the
  defining instance of a term.
- Do not assume familiarity with accessibility-specific terminology (WCAG, ARIA, AT,
  screen reader) on pages intended for a general audience. Define these terms on first use.
- Example:

```html
  <p>
    This page has been tested with a
    <dfn>screen reader</dfn>, software that converts
    text and interface elements to speech or braille output.
  </p>
```

---

### 3.1.4 Abbreviations (AAA)

- Provide the expanded form of abbreviations on first use on a page.
- Preferred approach: expand inline on first use ("Web Content Accessibility Guidelines
  (WCAG)"), then mark subsequent uses with the HTML `<abbr>` element and a `title`
  attribute.
- Do not rely solely on `<abbr title>` as the expansion mechanism. The `title` attribute
  is not accessible on touch devices and is not reliably announced by all AT.
- Example pattern:

```html
  <p>
    Web Content Accessibility Guidelines (WCAG) define how to make content accessible.
    All components are tested against
    <abbr title="Web Content Accessibility Guidelines">WCAG</abbr> 2.2.
  </p>
```

---

### 3.1.5 Reading Level (AAA)

- Write content at the lowest reading level appropriate for the audience without losing
  meaning or accuracy.
- Where content requires a reading level more advanced than lower secondary education
  (approximately age 11 to 14), provide a supplementary simplified version or summary.
- Use plain language principles: short sentences, active voice, common words, one idea
  per paragraph.
- Avoid nominalisations where possible. Use "we decided" rather than "a decision was
  made". Use "apply" rather than "make an application".
- Error messages, instructions, and help text are particularly important to write at a
  low reading level. A user struggling with a form does not need complex language
  compounding the difficulty.

---

### 3.1.6 Pronunciation (AAA)

- Where the meaning of a word depends on its pronunciation and is ambiguous in context,
  provide a mechanism to identify the correct pronunciation.
- Applies most often to proper nouns, technical terms with non-obvious pronunciation,
  and homographs (words spelled the same but pronounced differently, such as "lead" the
  metal versus "lead" the verb).
- Approaches: provide phonetic spelling in parentheses on first use, or link to an audio
  pronunciation.
- This criterion applies to a narrow set of content in most projects. Flag relevant
  instances in the Known Gaps section.

---

## Known Gaps and Project-Specific Notes

Add entries here as they are discovered during development or testing. Include the component name, the criterion affected, the reason for non-conformance, and any agreed workaround. Note any component libraries in use and their known AT support gaps.