# SC X.X.X — [Name] (Level X) — Manual Test Pattern

<!--
  HOW TO USE THIS TEMPLATE
  ─────────────────────────
  Copy this file to testing/X.X.X.md.
  Replace every placeholder (marked with < >) with SC-specific content.
  Delete this comment block before committing.

  PATTERN CONTRACT (do not deviate)
  ───────────────────────────────────
  Every testing file MUST contain all seven sections below, in order:
    1. Overview
    2. Scope — what to test
    3. Tools required
    4. Test steps
    5. Pass / Fail criteria
    6. Common false positives
    7. Related criteria

  Test steps MUST be numbered and atomic (one observable action per step).
  Each step MUST include: Action → Expected result.
  Pass / Fail criteria MUST map 1-to-1 to specific test steps.
-->

## 1 — Overview

**SC:** X.X.X — [Name] (Level [A / AA / AAA])
**Intent:** <One-sentence plain-language summary of what this SC requires a tester to verify.>
**Scope of this test:** <What kind of content or components does this test target? e.g. "All interactive UI components on the page.">

---

## 2 — Scope: what to test

Apply these tests to:

- <Component or content type 1>
- <Component or content type 2>
- <Component or content type 3 — add or remove as needed>

Do **not** test:

- <Out-of-scope item 1 — e.g. "Static text that has no interactive behaviour">
- <Out-of-scope item 2>

---

## 3 — Tools required

| Tool | Purpose | Free? |
|------|---------|-------|
| Browser DevTools (Chrome, Edge, or Firefox) | <What it is used for> | Yes |
| A11y Quick Check browser extension | <Which checks to run from the extension for this SC> | Yes |
| axe DevTools browser extension (or your preferred automation testing tool) | <What it is used for> | Yes (core) |
| NVDA + Chrome, Edge, or Firefox (Windows) | <Screen reader verification purpose> | Yes |
| JAWS + Chrome, Edge, or Firefox (Windows) | <Screen reader verification purpose> | No |
| VoiceOver + Safari (macOS / iOS) | <Screen reader verification purpose> | Yes (built-in) |

> **Note:** <Any version constraints, OS restrictions, or configuration steps needed before testing.>

---

## 4 — Test steps

Work through every step in sequence. Record a result (Pass / Fail / N/A) for each step.

### Step 1 — <Short imperative title, e.g. "Inspect accessible names">

**Action:** <Precisely what the tester does. Include which tool to open, which element to focus on, and which control to activate.>

**Expected result:** <What a conformant page shows, announces, or returns. Be specific enough that a tester cannot mis-score.>

**Fail signal:** <What a non-conformant page shows, announces, or returns.>

---

### Step 2 — <Short imperative title>

**Action:** <…>

**Expected result:** <…>

**Fail signal:** <…>

---

### Step 3 — <Short imperative title>

**Action:** <…>

**Expected result:** <…>

**Fail signal:** <…>

<!-- Add or remove steps as required. Aim for 4–8 steps per SC. -->

---

## 5 — Pass / Fail criteria

| Step | Passes when | Fails when |
|------|-------------|------------|
| 1 | <Concise pass condition> | <Concise fail condition> |
| 2 | <Concise pass condition> | <Concise fail condition> |
| 3 | <Concise pass condition> | <Concise fail condition> |

**Overall result:** The page **passes** this SC only when every applicable step passes.
A single step failure = **SC failure**.

---

## 6 — Common false positives

These situations can look like failures but are not:

- **<Situation 1>:** <Explanation of why it is not a failure.>
- **<Situation 2>:** <Explanation of why it is not a failure.>

These situations can look like passes but are not:

- **<Situation 3>:** <Explanation of why it is still a failure.>

---

## 7 — Related criteria

Failures here often co-occur with failures in:

- SC X.X.X — [Name] — <Brief note on the relationship>
- SC X.X.X — [Name] — <Brief note on the relationship>