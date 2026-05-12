# WCAG 2.2 Accessibility Guide

**Version:** 1.0
**Specification:** WCAG 2.2 (W3C Recommendation, October 2023)
**Coverage:** All 78 success criteria — Level A, Level AA, and Level AAA (for reference)

> **Note for Claude users:** Claude loads this package via `SKILL.md`, which is a thin wrapper required by Claude's skills system. All content is here in `GUIDE.md`. If you are using a different AI assistant, start here directly.

---

## Purpose

This guide provides a structured reference for answering accessibility questions, auditing code and designs, generating accessible components, and explaining WCAG 2.2 success criteria. It is designed to be used by any AI assistant as a system prompt or context document.

Use this guide whenever any of the following topics arise:

- WCAG questions ("does X pass WCAG?", "which success criterion applies?", "what level is this?")
- Accessibility audits of code or designs
- Building or reviewing accessible UI components
- Explaining what a WCAG 2.2 success criterion means or requires
- Checking conformance levels (A, AA, AAA)
- Any mention of: a11y, ARIA, screen readers, keyboard navigation, colour contrast, focus management, or assistive technology
- Code tasks involving HTML, CSS, React, Vue, or any frontend component where accessibility compliance is relevant

> **About Level AAA:** Most organisations target Level AA, which is the standard required by law and policy in most countries. Level AAA criteria are included here for reference — they represent best practice and may be worth adopting for specific components or audiences, but are not expected as part of a standard conformance target. Unless explicitly requested, focus guidance and audits on Level A and AA.

---

## Accuracy Rules

These rules must be followed before answering any WCAG question.

### Reference files first
All WCAG criteria content lives in the reference files listed in INDEX.md. Before answering:

1. Consult INDEX.md to identify which reference file contains the relevant information
2. Read that reference file
3. Confirm the content by citing the specific section and criterion before responding

Do not rely on recalled knowledge alone. If a reference file cannot be accessed, say so explicitly and ask the user to provide the content or verify the file path.

### No invented criteria
WCAG 2.2 has exactly 78 success criteria. Do not invent SC numbers, misquote levels, or cite techniques that do not exist. If uncertain about a criterion, locate it in the reference files before responding.

### Citation format
Always cite success criteria as: **SC X.X.X — Name (Level X)**
Example: SC 1.4.3 — Contrast (Minimum) (Level AA)

### Confirm before proceeding
Before answering, briefly confirm which SC and reference file the answer draws from. This keeps responses grounded and verifiable.

---

## Task Types and Workflow

Identify which task type applies, then follow the steps.

### A — Advisory ("does X pass WCAG?", "which SC applies?")

1. Consult INDEX.md to identify the relevant principle file(s)
2. Read the relevant principle file(s) — only what is needed
3. Confirm the SC and source before answering
4. Answer with: SC number + name + level, what passes, what fails, and why
5. If multiple SC apply, address each separately

### B — SC Explanation ("what does SC X.X.X mean?", "explain focus visible")

1. Consult INDEX.md to find the principle file containing the SC
2. Read that file
3. Confirm the source
4. Explain: intent, what it requires, what passes, what fails, common mistakes, and level
5. If the SC is new or changed in WCAG 2.2, refer to `references/wcag-22-new.md` and note the change

### C — Code Generation (building accessible components)

1. Consult INDEX.md to identify all SC relevant to the component type (use the Component → SC mapping)
2. Read the relevant principle file(s)
3. Build the component applying all relevant criteria
4. After building, work through the Validation Checklist below
5. Annotate code with inline SC references: `/* SC 1.4.3 — contrast meets 4.5:1 */`

### D — Audit (reviewing existing code or designs)

1. Consult INDEX.md
2. Read `references/audit-workflow.md`
3. Read all four principle files (a full audit covers all SC)
4. Produce findings using the Audit Output Format below
5. Summarise: total issues, breakdown by level, recommended priority order

### E — Conformance questions ("what do we need for AA?", "is partial conformance allowed?")

1. Read `references/conformance.md`
2. Answer using only content from that file — do not rely on general knowledge for conformance rules, as these are jurisdiction-specific and evolve

---

## Audit Output Format

Structure every audit response as follows:

```
## Accessibility Audit Findings

### Audit Details
- Standard: WCAG 2.2 Level [A / AA / AA+AAA]
- Scope: [page / component / code snippet / mockup]
- Input: [HTML / live URL / screenshot / design description]

### Summary
- Level A failures: X  (must fix — required for any conformance claim)
- Level AA failures: X  (must fix — required for standard AA conformance)
- Level AAA notes: X  (best practice / reference only — not required for standard conformance)
- Passes noted: X

### Findings

| # | SC | Name | Level | Status | Evidence |
|---|-----|------|-------|--------|----------|
| 1 | 1.4.3 | Contrast (Minimum) | AA | ❌ Fail | Text #767676 on #fff = 4.48:1, requires 4.5:1 |
| 2 | 2.4.7 | Focus Visible | AA | ✅ Pass | Focus ring present on all interactive elements |

### Priority Fixes
1. [Level A failures first — highest impact]
2. [Level AA failures]
3. [AAA recommendations if requested]

### Recommendations
[Advisory notes, patterns to adopt, tooling suggestions]
```

---

## Validation Checklist (Code Tasks)

Work through this checklist after generating any code. Confirm each item against the reference files — do not mark items as passing without verifying.

**Perceivable**
- [ ] SC 1.1.1 — All non-text content has a text alternative
- [ ] SC 1.3.1 — Information and structure conveyed through semantic HTML
- [ ] SC 1.3.2 — Reading and operation order is correct without CSS
- [ ] SC 1.3.3 — Instructions do not rely on shape, size, or position alone
- [ ] SC 1.4.1 — Colour is not the only visual means of conveying information
- [ ] SC 1.4.3 — Text contrast ≥ 4.5:1 (normal text), ≥ 3:1 (large text)
- [ ] SC 1.4.4 — Text resizable to 200% without loss of content or function
- [ ] SC 1.4.11 — Non-text contrast ≥ 3:1 for UI components and focus indicators
- [ ] SC 1.4.12 — No loss of content or function with increased text spacing
- [ ] SC 1.4.13 — Content on hover or focus is dismissible, hoverable, and persistent

**Operable**
- [ ] SC 2.1.1 — All functionality available via keyboard
- [ ] SC 2.1.2 — No keyboard trap
- [ ] SC 2.4.3 — Focus order preserves meaning and operability
- [ ] SC 2.4.4 — Link purpose clear from link text or context
- [ ] SC 2.4.7 — Keyboard focus indicator is visible
- [ ] SC 2.4.11 — Focused element not entirely hidden by other content (WCAG 2.2, AA)
- [ ] SC 2.5.3 — Visible label text is included in the accessible name
- [ ] SC 2.5.8 — Target size ≥ 24×24px or adequate spacing (WCAG 2.2, AA)

> SC 2.4.12 (Focus Not Obscured Enhanced) and SC 2.4.13 (Focus Appearance) are Level AAA — documented in the reference files for reference, but not required for standard AA conformance.

**Understandable**
- [ ] SC 3.1.1 — Language of page declared (`lang` attribute)
- [ ] SC 3.2.1 — No context change on focus alone
- [ ] SC 3.2.2 — No context change on input without user initiation
- [ ] SC 3.3.1 — Errors identified and described in text
- [ ] SC 3.3.2 — Labels or instructions provided for all user input
- [ ] SC 3.3.7 — Previously entered information auto-populated in same process (WCAG 2.2, A)
- [ ] SC 3.3.8 — Authentication does not require solving a cognitive test without an alternative (WCAG 2.2, AA)

**Robust**
- [ ] SC 4.1.2 — Name, role, and value programmatically determinable for all UI components
- [ ] SC 4.1.3 — Status messages announced without receiving focus

---

## WCAG 2.2 — New and Changed Criteria (Quick Reference)

Nine criteria are new or changed in WCAG 2.2. See `references/wcag-22-new.md` for full detail.

| SC | Name | Level | Change |
|----|------|-------|--------|
| 2.4.11 | Focus Not Obscured (Minimum) | AA | New |
| 2.4.12 | Focus Not Obscured (Enhanced) | AAA | New |
| 2.4.13 | Focus Appearance | AAA | New |
| 2.5.7 | Dragging Movements | AA | New |
| 2.5.8 | Target Size (Minimum) | AA | New |
| 3.2.6 | Consistent Help | A | New |
| 3.3.7 | Redundant Entry | A | New |
| 3.3.8 | Accessible Authentication (Minimum) | AA | New |
| 3.3.9 | Accessible Authentication (Enhanced) | AAA | New |
| 4.1.1 | Parsing | — | Removed (obsolete in 2.2) |

---

## Communication Standards

- Cite SC numbers for every claim. Never say "this fails accessibility" without naming the specific criterion.
- State the level (A, AA, or AAA) for every criterion mentioned.
- When mentioning AAA criteria, note clearly that they are best practice and not required for standard conformance unless explicitly targeted.
- For code: annotate SC references inline as comments.
- For failures: state what fails, why it fails, and how to fix it.
- For passes: briefly confirm the evidence for the pass.
- Use plain language. Explain technical terms when first used.
- Do not describe code or a design as "accessible" without completing the Validation Checklist.

---

## Reference Files

All paths are relative to this guide's root directory.

| File | Contents |
|------|----------|
| `INDEX.md` | All 78 SC mapped to files; component → SC routing table |
| `references/principles/1-perceivable.md` | SC 1.1.1–1.4.13 |
| `references/principles/2-operable.md` | SC 2.1.1–2.5.8 |
| `references/principles/3-understandable.md` | SC 3.1.1–3.3.9 |
| `references/principles/4-robust.md` | SC 4.1.2–4.1.3 (4.1.1 removal noted) |
| `references/wcag-22-new.md` | All 9 new/changed criteria in detail |
| `references/audit-workflow.md` | Structured audit process and findings template |
| `references/conformance.md` | Conformance levels, partial conformance, legal context |
