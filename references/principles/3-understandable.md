# Principle 3 — Understandable

Information and the operation of the user interface must be understandable.

---

## Guideline 3.1 — Readable

### SC 3.1.1 — Language of Page (Level A)
**Intent:** The default human language of each web page can be programmatically determined.

**Passes when:** `<html lang="en">` (or appropriate language code) is present and correct on every page.

**Fails when:** `lang` attribute is missing; `lang` is set to the wrong language; `lang` is set to an invalid code.

**Why it matters:** Screen readers use `lang` to select the correct voice and pronunciation engine. Without it, content may be read in the user's system language regardless of the actual page language.

**Common language codes:** `en` (English), `en-AU` (Australian English), `fr` (French), `de` (German), `ja` (Japanese), `ar` (Arabic — also add `dir="rtl"`), `zh` (Chinese).

**WCAG 2.2 change:** No change.

**Related SC:** 3.1.2

---

### SC 3.1.2 — Language of Parts (Level AA)
**Intent:** The human language of each passage or phrase that differs from the page language can be programmatically determined.

**Passes when:** Inline content in a different language uses the `lang` attribute: `<span lang="fr">Bonjour</span>`.

**Exception:** Proper names, technical terms, words of indeterminate language, words that are part of the vernacular of the surrounding text.

**Fails when:** A French quotation on an English page has no `lang="fr"`, causing a French screen reader voice not to activate.

**WCAG 2.2 change:** No change.

---

### SC 3.1.3 — Unusual Words (Level AAA)
**Intent:** A mechanism is available for identifying specific definitions of unusual or specialist terms (jargon, idioms).

**Passes when:** Glossary provided; terms linked to definitions; `<abbr title="">` used for abbreviations.

**WCAG 2.2 change:** No change.

---

### SC 3.1.4 — Abbreviations (Level AAA)
**Intent:** A mechanism for identifying the expanded form or meaning of abbreviations is available.

**Passes when:** First use expands the abbreviation: "Web Content Accessibility Guidelines (WCAG)"; or `<abbr title="Web Content Accessibility Guidelines">WCAG</abbr>`.

**WCAG 2.2 change:** No change.

---

### SC 3.1.5 — Reading Level (Level AAA)
**Intent:** When text requires more than a lower secondary education reading level (approx. age 11–12), a supplemental version or visual aid is provided.

**WCAG 2.2 change:** No change.

---

### SC 3.1.6 — Pronunciation (Level AAA)
**Intent:** A mechanism for identifying pronunciation of words where meaning is ambiguous without pronunciation is available.

**WCAG 2.2 change:** No change.

---

## Guideline 3.2 — Predictable

### SC 3.2.1 — On Focus (Level A)
**Intent:** Receiving focus does not automatically trigger a context change.

**Context change:** Change of user agent, viewport, focus, or content that significantly changes the page meaning — e.g. a new window opening, content reordering, form submission.

**Passes when:** Focusing a dropdown does not submit the form; focusing a link does not open a new page; tooltip appearing on focus is acceptable (not a context change).

**Fails when:** A select element submits a form as soon as an option is focused; focusing a nav link opens a new window without warning.

**WCAG 2.2 change:** No change.

**Related SC:** 3.2.2

---

### SC 3.2.2 — On Input (Level A)
**Intent:** Changing the setting of a UI component does not automatically cause a context change unless the user is advised in advance.

**Passes when:**
- A form auto-submits after the last field, but users are warned beforehand
- Selecting a radio button updates a price display (not a context change — no navigation or major content shift)
- A "Go" button initiates navigation after a select input

**Fails when:**
- Selecting a country from a dropdown immediately redirects to a country-specific page without prior warning
- Checking a checkbox reloads the page without user initiation

**WCAG 2.2 change:** No change.

**Related SC:** 3.2.1

---

### SC 3.2.3 — Consistent Navigation (Level AA)
**Intent:** Navigation mechanisms repeated across pages appear in the same relative order each time, unless changed by the user.

**Passes when:** Site-wide navigation, breadcrumbs, and search appear in the same position and same order on every page.

**Fails when:** Primary navigation moves to a different position on interior pages; navigation items appear in a different order on some pages.

**Note:** This applies to the *order* of repeated items, not the content of each page. Adding page-specific nav items is acceptable as long as the shared items keep their relative order.

**WCAG 2.2 change:** No change.

---

### SC 3.2.4 — Consistent Identification (Level AA)
**Intent:** Components with the same functionality are identified consistently throughout content.

**Passes when:** A search field is always labelled "Search" (or always has the same accessible name); a print icon always has the same label.

**Fails when:** A search field is labelled "Search" on one page and "Find" on another; a "Close" button is labelled "Dismiss" in some dialogs and "Close" in others.

**WCAG 2.2 change:** No change.

---

### SC 3.2.5 — Change on Request (Level AAA)
**Intent:** Changes of context are only initiated by user request, or a mechanism to turn off such changes is available.

**WCAG 2.2 change:** No change.

---

### SC 3.2.6 — Consistent Help (Level A) ← NEW in WCAG 2.2
**Intent:** If a web page provides any help mechanisms (human contact, chat, FAQ, self-help), these appear in the same relative order across pages.

**Applies to:** Chat widgets, "Contact us" links, help phone numbers, self-help links, automated chat bots.

**Passes when:** The help widget or help link appears in the same position (e.g. bottom right, top navigation) consistently across all pages that include it.

**Fails when:** Chat widget appears in the footer on some pages and in the sidebar on others; help link moves between header and footer.

**Note:** This SC does not require help to be provided — it only requires that *if* help is provided, it appears consistently.

**WCAG 2.2 change:** NEW in WCAG 2.2.

---

## Guideline 3.3 — Input Assistance

### SC 3.3.1 — Error Identification (Level A)
**Intent:** If an input error is detected, the item in error is identified and the error is described in text.

**Passes when:**
- Error message identifies which field has the error ("Email address is required")
- Error is communicated in text, not colour alone
- `aria-invalid="true"` set on the erroneous field
- Error message associated with the field via `aria-describedby`

**Fails when:**
- Only a red border indicates the error (colour alone — fails SC 1.4.1 as well)
- Generic error message "Please fix the errors above" without identifying specific fields
- Error not associated with the input programmatically

**WCAG 2.2 change:** No change.

**Related SC:** 3.3.2, 3.3.3, 1.4.1, 4.1.2

---

### SC 3.3.2 — Labels or Instructions (Level A)
**Intent:** Labels or instructions are provided when content requires user input.

**Passes when:**
- Every form input has a visible `<label>` or equivalent accessible name
- Required fields indicated (via text, asterisk with legend, or aria-required)
- Format instructions provided where needed (e.g. "Date format: DD/MM/YYYY")
- Placeholder text used only as a supplement, not as the sole label

**Fails when:**
- Placeholder text is the only label (disappears when user types)
- No indication of required fields
- No format instruction for constrained inputs (phone, date, postcode)

**WCAG 2.2 change:** No change.

**Related SC:** 3.3.1, 1.3.1

---

### SC 3.3.3 — Error Suggestion (Level AA)
**Intent:** If an input error is detected and suggestions are known, they are provided — unless doing so would jeopardise security or purpose.

**Passes when:**
- "Email address format is invalid. Enter in format: name@example.com"
- "Password must be at least 8 characters and include one number"
- Security questions: acceptable to not provide the answer as a suggestion

**Fails when:**
- Error says "Invalid input" with no guidance on what is valid
- Format error with no example or hint

**Exception:** Security-sensitive fields (passwords, CAPTCHAs) — suggestions not required.

**WCAG 2.2 change:** No change.

---

### SC 3.3.4 — Error Prevention (Legal, Financial, Data) (Level AA)
**Intent:** For pages that cause legal commitments, financial transactions, or modify/delete data: submissions are reversible, checked, or confirmed.

**Passes when:**
- Order confirmation step before final purchase
- Ability to cancel or modify an order after submission
- Explicit confirmation dialog before deleting data
- Data is checked for input errors and user has opportunity to correct before final submission

**Applies to:** E-commerce checkout, account deletion, form submissions that create legal records, data deletion.

**WCAG 2.2 change:** No change.

**Related SC:** 3.3.7, 3.3.8

---

### SC 3.3.5 — Help (Level AAA)
**Intent:** Context-sensitive help is available.

**Passes when:** Help text, tooltips, or links to help content provided in context of form fields or complex tasks.

**WCAG 2.2 change:** No change.

---

### SC 3.3.6 — Error Prevention (All) (Level AAA)
**Intent:** For all pages with user submissions: submissions are reversible, checked, or confirmed. (Stricter than 3.3.4 — applies to all inputs, not just legal/financial.)

**WCAG 2.2 change:** No change.

---

### SC 3.3.7 — Redundant Entry (Level A) ← NEW in WCAG 2.2
**Intent:** Information previously entered by the user that is required again in the same process is either auto-populated or available for the user to select, unless re-entering is essential, the information is a security requirement, or the previously entered data is no longer valid.

**Applies to:** Multi-step forms and processes (checkout, registration, applications).

**Passes when:**
- Billing address auto-populated from shipping address with a "same as shipping" option
- User's name pre-filled in a confirmation step
- Previously selected options retained when navigating back in a wizard

**Fails when:**
- Multi-step checkout requires the user to re-enter their name and email on a confirmation page
- Address entered in step 1 must be manually re-entered in step 3

**Exception:** Re-entry required for security (password confirmation), or data is inherently temporary (OTP, CAPTCHA).

**WCAG 2.2 change:** NEW in WCAG 2.2.

---

### SC 3.3.8 — Accessible Authentication (Minimum) (Level AA) ← NEW in WCAG 2.2
**Intent:** A cognitive function test (memorising a password, solving a puzzle, transcribing characters) is not required for any step in an authentication process unless an alternative is available.

**Cognitive function tests include:** Remembering a password; solving a puzzle; identifying objects in images; transcribing characters.

**Passes when:**
- Password field allows paste (so password managers work)
- "Show password" toggle provided
- Copy-paste allowed into authentication fields
- Password manager can auto-fill the field (no autocomplete="off" blocking it)
- An alternative authentication method is available (e.g. magic link, biometric, passkey) alongside a password

**Fails when:**
- Copy-paste disabled on password fields (`oncopy`, `onpaste` blocked)
- `autocomplete="off"` on username/password fields (prevents password managers)
- Only authentication method is a puzzle or CAPTCHA with no alternative
- Only authentication method is recognising specific images with no alternative

**Exception:** Object recognition and personal content (e.g. "identify your own photo") are permitted if an alternative exists.

**WCAG 2.2 change:** NEW in WCAG 2.2.

**Related SC:** 3.3.9

---

### SC 3.3.9 — Accessible Authentication (Enhanced) (Level AAA) ← NEW in WCAG 2.2
**Intent:** A cognitive function test is not required for any step in an authentication process — stricter than 3.3.8 because the exceptions for object recognition and personal content do not apply.

**WCAG 2.2 change:** NEW in WCAG 2.2.

**Related SC:** 3.3.8
