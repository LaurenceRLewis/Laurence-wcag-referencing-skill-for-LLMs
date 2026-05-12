# Principle 4 — Robust

Content must be robust enough to be interpreted by a wide variety of user agents, including assistive technologies.

---

## Important: SC 4.1.1 Removed in WCAG 2.2

**SC 4.1.1 — Parsing** has been **removed** from WCAG 2.2. It is no longer a testable criterion.

**Reason:** Modern browsers handle malformed HTML gracefully and consistently. Validating HTML against the spec no longer has a meaningful accessibility impact. The W3C formally removed this SC in the WCAG 2.2 October 2023 Recommendation.

**Action required:** If you are auditing against WCAG 2.2, do not test or report SC 4.1.1 as a criterion. If you are auditing against WCAG 2.1, it still applies.

---

## Guideline 4.1 — Compatible

### SC 4.1.2 — Name, Role, Value (Level A)
**Intent:** For all UI components, the name and role can be programmatically determined; states, properties, and values that can be set by the user can be programmatically set; and notification of changes is available to user agents and assistive technologies.

**The three parts:**

**1. Name** — Every interactive element must have an accessible name:
- `<button>`: text content, `aria-label`, or `aria-labelledby`
- `<input>`: associated `<label>`, `aria-label`, or `aria-labelledby`
- `<img>` used as a link: `alt` on the image
- Icon button with no text: `aria-label` on the button
- `<svg>` icon: `<title>` inside the SVG, or `aria-label` on the parent

**2. Role** — Every interactive element must have a correct role:
- Use native HTML elements where possible (`<button>`, `<a>`, `<input>`, `<select>`)
- Custom widgets must use ARIA roles: `role="dialog"`, `role="tab"`, `role="combobox"`, etc.
- Do not add redundant roles: `<button role="button">` is incorrect

**3. Value / State** — Dynamic state changes must be reflected in the accessibility tree:
- Expanded/collapsed: `aria-expanded="true/false"` on the toggle control
- Selected: `aria-selected="true/false"` on tabs, options
- Checked: `aria-checked="true/false"` on custom checkboxes/radios
- Pressed: `aria-pressed="true/false"` on toggle buttons
- Current page: `aria-current="page"` on navigation links
- Disabled: `aria-disabled="true"` (or native `disabled` attribute)
- Required: `aria-required="true"` (or native `required` attribute)
- Invalid: `aria-invalid="true"` on inputs with errors
- Hidden: `aria-hidden="true"` on decorative or redundant content

**Passes when:**
- All interactive elements have an accessible name
- All custom widgets use correct ARIA roles
- All dynamic states are reflected in ARIA attributes

**Fails when:**
- Icon button has no accessible name (`aria-label` missing, no text)
- Custom modal uses `<div>` without `role="dialog"` and `aria-modal="true"`
- Toggle button changes visually but `aria-expanded` is not updated
- `aria-labelledby` references an ID that does not exist in the DOM
- `aria-hidden="true"` applied to a focusable element (hides it from AT but it still receives focus)

**Common patterns:**

```html
<!-- Button: accessible name from text content -->
<button type="button">Save changes</button>

<!-- Icon button: accessible name from aria-label -->
<button type="button" aria-label="Close dialog">
  <svg aria-hidden="true">...</svg>
</button>

<!-- Expandable section: state via aria-expanded -->
<button aria-expanded="false" aria-controls="panel-1">
  Show details
</button>
<div id="panel-1" hidden>...</div>

<!-- Custom checkbox: role + state -->
<div role="checkbox" aria-checked="false" tabindex="0">
  Subscribe to newsletter
</div>

<!-- Invalid input: error state + description -->
<input aria-invalid="true" aria-describedby="email-error" />
<span id="email-error">Enter a valid email address</span>
```

**WCAG 2.2 change:** No change. (SC 4.1.1 was removed; 4.1.2 and 4.1.3 unchanged.)

**Related SC:** 1.3.1, 2.1.1, 3.3.1

---

### SC 4.1.3 — Status Messages (Level AA)
**Intent:** Status messages that are not given focus can be programmatically determined through role or property so they can be announced by assistive technology without receiving focus.

**Applies to:** Dynamic status messages, alerts, confirmations, error summaries, loading indicators, search result counts, and cart update notifications that appear without moving focus.

**Passes when:**
- Success message uses `role="status"` (polite — announces after current speech finishes)
- Error alert uses `role="alert"` (assertive — interrupts current speech immediately)
- Loading state uses `aria-live="polite"` or `role="status"`
- Search results count update uses `role="status"` or `aria-live="polite"`

**Fails when:**
- A "Changes saved" message appears visually but is a plain `<div>` with no live region role
- An error summary appears after form submission but focus is not moved to it and it has no `role="alert"`
- A cart "Item added" notification has no programmatic announcement mechanism

**Live region guidance:**
| Role / Property | Politeness | Use for |
|---|---|---|
| `role="alert"` | Assertive | Errors, critical warnings, destructive confirmations |
| `role="status"` | Polite | Success messages, loading complete, search result counts |
| `aria-live="polite"` | Polite | Dynamic content updates that are informational |
| `aria-live="assertive"` | Assertive | Use sparingly — only time-critical interruptions |
| `role="log"` | Polite | Appended content (chat log, activity feed) |
| `role="timer"` | Off | Countdown timers (do not auto-announce) |

**Rules for live regions:**
- Do not move focus AND use a live region for the same content (double announcement)
- Inject content into an already-rendered live region — do not inject the live region element itself
- Keep assertive announcements short and infrequent — they interrupt the user immediately
- `aria-atomic="true"` announces the entire region on any change; `aria-atomic="false"` (default) announces only the changed node

**Example:**

```html
<!-- Correct: status region already in DOM, message injected dynamically -->
<div role="status" aria-live="polite" aria-atomic="true" id="save-status"></div>

<script>
  // On save success:
  document.getElementById('save-status').textContent = 'Changes saved successfully.';
</script>

<!-- Correct: error alert -->
<div role="alert">
  Your session has expired. Please log in again.
</div>
```

**WCAG 2.2 change:** No change.

**Related SC:** 4.1.2, 3.3.1
