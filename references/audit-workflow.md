# Audit Workflow

Use this file when performing a structured accessibility audit (Task Type D in GUIDE.md).

---

## Audit Scope

Before beginning, establish:

1. **Standard:** WCAG 2.2 — which levels? (A only / A+AA / A+AA+AAA)
2. **Scope:** Full page / specific component / code snippet / design mockup
3. **Input type:** Live URL / HTML code / screenshot / design file description

Declare the scope in your audit output header.

---

## Step 1 Structural Review

Before testing individual SC, review the overall structure:

- Is there a `<html lang="...">` attribute?
- Does the page have a `<title>`?
- Is there a `<main>` landmark? `<nav>`? `<header>`? `<footer>`?
- Is there a skip link or other bypass mechanism?
- Does heading hierarchy make sense (`<h1>` → `<h2>` → `<h3>`, no skips)?

These quick checks catch Level A failures early.

---

## Step 2 Component Inventory

List all interactive and content components present:

- Forms and inputs (text fields, checkboxes, radios, selects, date pickers)
- Buttons and links
- Navigation (primary nav, breadcrumbs, pagination)
- Images (informative, decorative, complex/charts)
- Tables (data tables, layout tables)
- Custom widgets (modals, tabs, accordions, tooltips, carousels)
- Media (video, audio, animations)
- Dynamic content (live regions, toast notifications, loading states)

---

## Step 3 Test Against SC

For each component, test against the relevant SC from the INDEX.md Component → SC Mapping.

**Testing method per input type:**

| Input type | Testing approach |
|---|---|
| HTML code | Review code directly; check ARIA, labels, roles, attributes |
| Live URL | Keyboard navigation test + code review + contrast check |
| Screenshot/mockup | Visual checks only — note which SC cannot be tested without code |
| Design description | Advisory assessment — flag likely risks, note assumptions |

**What to check per SC category:**

### Perceivable checks
- All images: `alt` present and appropriate (SC 1.1.1)
- All text/background colour combinations: contrast ≥ 4.5:1 normal, ≥ 3:1 large (SC 1.4.3)
- All UI component borders and focus indicators: ≥ 3:1 contrast (SC 1.4.11)
- `lang` attribute on `<html>` (SC 3.1.1)
- No information conveyed by colour alone (SC 1.4.1)
- Text reflows at 320px equivalent (SC 1.4.10)
- Hover/focus triggered content: dismissible, hoverable, persistent (SC 1.4.13)

### Operable checks
- Keyboard: Tab through all interactive elements; every one reachable and activatable (SC 2.1.1)
- No keyboard trap: can always navigate away (SC 2.1.2)
- Focus visible: every focused element has a visible indicator (SC 2.4.7)
- Focus not obscured by sticky headers/footers (SC 2.4.11) ← WCAG 2.2
- Tab order logical and matches reading order (SC 2.4.3)
- All links have descriptive purpose (SC 2.4.4)
- Skip link or landmark navigation available (SC 2.4.1)
- Target sizes: interactive elements ≥ 24×24px or adequate spacing (SC 2.5.8) ← WCAG 2.2
- Drag-and-drop has non-drag alternative (SC 2.5.7) ← WCAG 2.2
- Visible label text included in accessible name (SC 2.5.3)

### Understandable checks
- No context change on focus alone (SC 3.2.1)
- No context change on input without warning (SC 3.2.2)
- Navigation consistent across pages (SC 3.2.3)
- Help mechanisms in consistent location (SC 3.2.6) ← WCAG 2.2
- All form inputs labelled (SC 3.3.2)
- Errors identified in text and associated with inputs (SC 3.3.1)
- Error suggestions provided (SC 3.3.3)
- No redundant entry required in multi-step processes (SC 3.3.7) ← WCAG 2.2
- Authentication does not require cognitive test without alternative (SC 3.3.8) ← WCAG 2.2

### Robust checks
- Every interactive element has an accessible name (SC 4.1.2)
- Custom widgets have correct ARIA roles (SC 4.1.2)
- Dynamic states reflected in ARIA (aria-expanded, aria-selected, aria-checked) (SC 4.1.2)
- Status messages use live regions (SC 4.1.3)
- No ARIA reference IDs that don't exist in the DOM (SC 4.1.2)

---

## Step 4 Contrast Testing

For any visual UI work, check contrast:

**Text contrast (SC 1.4.3):**
- Normal text (< 18pt or < 14pt bold): minimum 4.5:1
- Large text (≥ 18pt or ≥ 14pt bold): minimum 3:1

**Non-text contrast (SC 1.4.11):**
- UI component boundaries: minimum 3:1 against adjacent colour
- Focus indicators: minimum 3:1 against adjacent colour
- Informational icons: minimum 3:1

**Enhanced text contrast (SC 1.4.6, AAA):**
- Normal text: 7:1; Large text: 4.5:1

Report each colour combination tested: foreground, background, ratio, result.

---

## Step 5 Output the Findings Table

Use the format from GUIDE.md Audit Output Format:

```
## Accessibility Audit Findings

### Audit Details
- Standard: WCAG 2.2 Level AA
- Scope: [describe]
- Date: [date]
- Input: [HTML / live URL / mockup]

### Summary
- Level A failures: X
- Level AA failures: X
- Level AAA failures (if tested): X
- Passes noted: X
- Cannot test (requires code/browser): X

### Findings

| # | SC | Name | Level | Status | Evidence |
|---|-----|------|-------|--------|----------|

### Priority Order
[Level A failures first, then AA, then AAA]

### Recommendations
[Advisory notes, patterns to adopt, tooling suggestions]
```

---

## Audit Limitations by Input Type

Always declare these in your audit output:

| Input type | Limitations |
|---|---|
| Code only | Cannot test actual keyboard behaviour, screen reader output, rendering |
| Screenshot/mockup | Can only test visual SC (contrast, layout, labels visible); cannot test keyboard, ARIA, live regions |
| Design description | Advisory only — all findings are risks and recommendations, not confirmed failures |
| Live URL (without browser access) | Cannot perform keyboard or screen reader testing; code review only |

---

## Common High-Priority Patterns to Check First

These are the most commonly failed SC in real-world audits — check these first:

1. **SC 1.4.3** — Text contrast (very commonly failed, especially for grey text and placeholders)
2. **SC 4.1.2** — Missing accessible names on icon buttons
3. **SC 1.3.1** — Form inputs without associated labels
4. **SC 2.4.7** — `outline: none` applied globally with no replacement focus style
5. **SC 3.3.1** — Errors indicated by colour only
6. **SC 1.1.1** — Missing or incorrect alt text on images
7. **SC 2.4.4** — "Read more" / "Click here" links without context
8. **SC 2.4.11** — Sticky headers covering focused elements ← WCAG 2.2
9. **SC 3.3.8** — Paste blocked on password fields ← WCAG 2.2
10. **SC 2.5.8** — Small touch targets without adequate spacing ← WCAG 2.2
