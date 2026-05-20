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
- Never add `role="navigation"` to a native `<nav>` element, `role="main"` to `<main>`, `role="banner"` to `<header>`, or `role="contentinfo"` to `<footer>`. All landmark roles are implicit on their native elements.
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

## Known Gaps and Project-Specific Notes

Add entries here as they are discovered during development or testing. Include the component name, the criterion affected, the reason for non-conformance, and any agreed workaround.