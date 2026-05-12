# WCAG 2.2 — New and Changed Success Criteria

WCAG 2.2 was published as a W3C Recommendation on 5 October 2023. It introduced 9 new success criteria and removed 1.

---

## Removed Criterion

### SC 4.1.1 — Parsing (REMOVED)
**Previously:** Level A requirement to ensure HTML is well-formed (unique IDs, correct nesting, complete start/end tags).
**Why removed:** Modern browsers parse and repair malformed HTML consistently. The SC no longer has meaningful accessibility impact.
**Action:** Do not test 4.1.1 when auditing to WCAG 2.2. If auditing to WCAG 2.1, it still applies.

---

## New Criteria — Level A

### SC 3.2.6 — Consistent Help (Level A)
**Guideline:** 3.2 Predictable

**Intent:** If a web page includes any help mechanism (contact details, chat, FAQ link, self-help), it appears in the same relative order on every page that includes it.

**Key points:**
- Does not require help to be provided — only requires consistency IF it is provided
- Applies to: human contact details, chat interfaces, self-help tools, automated contact mechanisms
- "Same relative order" — other items may be added or removed around the help mechanism, as long as its position relative to other help mechanisms stays constant

**Passes when:**
- Live chat widget consistently in the bottom-right corner of every page
- "Contact us" link consistently the last item in the footer navigation
- Help phone number consistently in the top-right header

**Fails when:**
- Chat widget in the footer on the homepage, in the sidebar on product pages
- "Get help" link appears in the primary nav on some pages and the footer on others

---

### SC 3.3.7 — Redundant Entry (Level A)
**Guideline:** 3.3 Input Assistance

**Intent:** Information previously provided by the user in the same process must be auto-populated or selectable for re-use, unless re-entering is essential, a security requirement, or the data is no longer valid.

**Key points:**
- Applies to multi-step processes within a single session
- "Same process" = a series of steps to complete one task (checkout, registration, application)
- Prevents unnecessary cognitive load of re-entering the same data

**Passes when:**
- "Same as shipping address" checkbox auto-fills billing address
- Name from step 1 pre-filled in a summary/confirmation step
- Previously selected options retained when navigating back in a wizard
- Username pre-filled in a confirmation email field

**Fails when:**
- Multi-step checkout asks for name and email again in step 3 despite being entered in step 1
- User must re-enter their delivery address on a returns form within the same session

**Exceptions:**
- Password re-entry for security confirmation (e.g. "confirm new password")
- CAPTCHA / OTP — inherently single-use
- Previously entered data is now invalid (expired session token)
- Re-entering is part of the essential purpose of the task (e.g. a data-entry training exercise)

---

## New Criteria — Level AA

### SC 2.4.11 — Focus Not Obscured (Minimum) (Level AA)
**Guideline:** 2.4 Navigable

**Intent:** When a UI component receives keyboard focus, it is not entirely hidden by author-created content.

**Key points:**
- "Entirely hidden" = no part of the focused component is visible
- Partial obscuring is allowed at AA — the component just must not be completely covered
- "Author-created content" = sticky headers, floating footers, cookie banners, chat widgets, overlays
- Does not apply to content the user has opened (e.g. a dropdown the user opened that now covers something)

**Common causes of failure:**
- Sticky/fixed header covers the focused form field when user tabs down the page
- Cookie consent banner sits over the focused "Accept" / "Decline" buttons
- Floating chat widget overlaps focused content in the bottom of the viewport
- A modal's backdrop covers focused content behind it (though this is usually intentional and acceptable)

**Passes when:**
- At least a portion of the focused element is visible on screen
- Sticky header uses `scroll-margin-top` or JavaScript scroll adjustment so focused elements appear below the header
- Cookie banner is dismissed before keyboard navigation reaches obscured areas, or repositions

**Relationship to other SC:**
- SC 2.4.12 (AAA) is the stricter version — no part of the focused element may be hidden
- SC 2.4.13 (AAA) requires the focus indicator itself to meet size/contrast requirements
- SC 2.4.7 (AA) requires focus to be *visible* — 2.4.11 adds the requirement that it not be *covered*

---

### SC 2.5.7 — Dragging Movements (Level AA)
**Guideline:** 2.5 Input Modalities

**Intent:** All functionality that uses a dragging movement can also be achieved with a single pointer (no dragging), unless dragging is essential.

**Key points:**
- Dragging = pressing, moving, releasing a pointer in a path (mouse drag, touch drag)
- Alternatives must be available for users who cannot perform dragging (motor disabilities, switch access, voice control)
- "Essential" exemption is narrow — e.g. a freehand drawing app where the path is the product

**Common components affected:**
- **Drag-and-drop lists:** Add move up/down buttons, or a "move to position" input
- **Range sliders:** Allow clicking directly on the track to set a value; allow arrow key input
- **Kanban boards:** Add "move to column" button or dropdown
- **File upload areas:** Must also accept a file picker button (most do already)
- **Sortable tables:** Add sort buttons or controls

**Passes when:**
- Drag-and-drop kanban card also has a "Move to" button
- Slider can be positioned by clicking anywhere on the track
- Sortable list has up/down arrow controls
- Single-tap/click achieves the same result as a drag gesture

**Fails when:**
- The only way to reorder items is by dragging
- Slider thumb can only be moved by click-drag, not by clicking a track position or using keyboard

---

### SC 2.5.8 — Target Size (Minimum) (Level AA)
**Guideline:** 2.5 Input Modalities

**Intent:** Pointer input targets are at least 24×24 CSS pixels in size, or have sufficient spacing so the target area is 24×24.

**The spacing rule:** If the target itself is smaller than 24×24px, the target plus its offset (spacing from adjacent targets) must cover a 24×24 area. This means adequate padding around small targets can satisfy the criterion.

**Exceptions:**
- **Inline:** Links within a run of text (target size is determined by text size and line height)
- **User agent:** Target size set by the browser and not modified by the author
- **Essential:** A particular presentation of the target is essential (e.g. a small pin on a map)
- **Equivalent:** Another control on the same page performs the same function and meets the target size requirement

**Passes when:**
- A 32×32px icon button — passes (> 24×24)
- A 16×16px icon button with 8px spacing on each side — the spacing + target = 24×24 circle, passes
- Text links in body copy — exempt (inline exception)
- A small map marker with an equivalent zoom control meeting target size — passes via equivalent exception

**Fails when:**
- A 16×16px icon button with no padding or adjacent spacing
- A close "×" button that is 12×12px with only 2px margin
- Navigation links styled at 20px tall with no extra padding

**Difference from SC 2.5.5 (AAA):**
- SC 2.5.5 requires 44×44px with no spacing exception
- SC 2.5.8 requires 24×24px with a spacing allowance — this is the new AA minimum

---

### SC 3.3.8 — Accessible Authentication (Minimum) (Level AA)
**Guideline:** 3.3 Input Assistance

**Intent:** Authentication processes do not require users to solve a cognitive function test unless an alternative is available.

**What is a cognitive function test?**
- Memorising a password or PIN
- Transcribing characters from an image (traditional CAPTCHA)
- Solving a puzzle
- Recognising objects in images (image-based CAPTCHA)
- Recognising user-provided content (e.g. "which of these is your pet photo?")

**Passes when:**
- Password fields allow copy-paste (password manager can paste)
- `autocomplete` attributes set on username/password fields (password manager can autofill)
- No `autocomplete="off"` or JavaScript blocking paste on authentication fields
- An alternative authentication method is available alongside any cognitive test (e.g. magic link, biometrics, passkey)
- Object recognition CAPTCHA has an audio alternative

**Fails when:**
- Copy-paste is blocked on password fields
- `autocomplete="off"` on username and password fields preventing password manager use
- The only authentication option is solving a visual CAPTCHA with no audio or other alternative
- The only authentication option is a game or puzzle

**Exceptions allowed at AA (not at AAA):**
- Object recognition (e.g. "select all images with traffic lights") — allowed if an alternative exists
- Personal content recognition (e.g. "identify your pet photo") — allowed if an alternative exists

**Practical implementation:**
1. Remove `autocomplete="off"` from all authentication fields
2. Remove JavaScript that blocks paste events on password fields
3. Set `autocomplete="username"` and `autocomplete="current-password"` on login fields
4. If using CAPTCHA, always provide an audio alternative or a non-CAPTCHA fallback (magic link, etc.)
5. Consider passkeys as a future-proof alternative

---

## New Criteria — Level AAA

### SC 2.4.12 — Focus Not Obscured (Enhanced) (Level AAA)
**Intent:** When a component receives keyboard focus, no part of it is hidden by author-created content. (Stricter version of SC 2.4.11 — at AA, partial obscuring is allowed; at AAA, none is.)

---

### SC 2.4.13 — Focus Appearance (Level AAA)
**Intent:** The keyboard focus indicator meets minimum size and contrast requirements.

**Requirements:**
1. The focus indicator encloses the component or the component's text
2. The focus indicator area is at least as large as a 2 CSS px perimeter around the unfocused component
3. The colour change between focused and unfocused states has a contrast ratio of at least 3:1 against adjacent colours

**Practical guidance:**
- A 2px solid outline with ≥ 3:1 contrast against the adjacent background meets this criterion
- Outline offset can be used to ensure the outline does not merge with the component background

---

### SC 3.3.9 — Accessible Authentication (Enhanced) (Level AAA)
**Intent:** Authentication processes do not require solving a cognitive function test at any step — no exceptions. (Stricter than SC 3.3.8, which allows object recognition and personal content recognition if alternatives exist.)

---

## Migration from WCAG 2.1

| If you are moving from WCAG 2.1 to 2.2… | Action |
|---|---|
| Stop testing SC 4.1.1 (Parsing) | Remove from audit templates |
| Add SC 2.4.11 (Focus Not Obscured, AA) | Test sticky headers/footers and overlays |
| Add SC 2.5.7 (Dragging, AA) | Review all drag-and-drop, sliders, sortable lists |
| Add SC 2.5.8 (Target Size, AA) | Audit interactive element sizes and spacing |
| Add SC 3.2.6 (Consistent Help, A) | Check help widget consistency across pages |
| Add SC 3.3.7 (Redundant Entry, A) | Review multi-step forms and processes |
| Add SC 3.3.8 (Accessible Authentication, AA) | Audit login forms, CAPTCHA, paste blocking |
| Add SC 2.4.12, 2.4.13, 3.3.9 if targeting AAA | Extended focus and auth requirements |
