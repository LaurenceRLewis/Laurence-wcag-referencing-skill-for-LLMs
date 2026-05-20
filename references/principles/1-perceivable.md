# Principle 1 — Perceivable

Information and user interface components must be presentable to users in ways they can perceive.

---

## Guideline 1.1 — Text Alternatives

### SC 1.1.1 — Non-text Content (Level A)
**Intent:** Provide text alternatives for non-text content so it can be changed into other forms (large print, braille, speech, symbols, simpler language).

**Applies to:** Images, icons, charts, graphs, infographics, audio, video, CAPTCHA, decorative content, controls with visual labels only.

**Passes when:**
- Informative images have descriptive `alt` text conveying the same information
- Functional images (e.g. image buttons) have `alt` describing the function, not the appearance
- Decorative images use `alt=""` (empty alt) and/or `aria-hidden="true"`
- Complex images (charts, diagrams) have a short `alt` and a long description accessible nearby or via link
- CAPTCHAs provide a text alternative explaining the purpose, plus an alternative modality

**Fails when:**
- `alt` attribute is missing entirely
- `alt` is the filename (e.g. `alt="image001.jpg"`)
- `alt` says "image of" or "photo of" (redundant — screen readers already announce "image")
- Decorative images have descriptive `alt` text (adds noise)
- Icon buttons have no accessible name

**Common mistakes:** Using `alt` to stuff keywords; writing identical alt for multiple unique images; forgetting alt on linked images (the link has no accessible name).

**WCAG 2.2 change:** No change from 2.1.

**Related SC:** 1.3.1, 4.1.2

---

## Guideline 1.2 — Time-based Media

### SC 1.2.1 — Audio-only and Video-only (Prerecorded) (Level A)
**Intent:** Provide alternatives for prerecorded audio-only and video-only content.

**Passes when:**
- Audio-only: transcript provided with all spoken content and relevant sounds
- Video-only (no audio): text transcript or audio description provided

**Fails when:** No alternative provided for standalone audio or silent video.

**WCAG 2.2 change:** No change.

---

### SC 1.2.2 — Captions (Prerecorded) (Level A)
**Intent:** Provide captions for all prerecorded audio content in synchronised media.

**Passes when:** Captions are synchronised, include all dialogue, identify speakers, and include relevant non-speech audio (music cues, sound effects).

**Fails when:** Auto-generated captions used without correction; captions missing; captions not synchronised.

**WCAG 2.2 change:** No change.

---

### SC 1.2.3 — Audio Description or Media Alternative (Prerecorded) (Level A)
**Intent:** Provide audio description or full text alternative for prerecorded video with audio.

**Passes when:** Audio description track available, OR full text alternative provided describing all visual content that is not in the audio.

**Note:** SC 1.2.5 (Level AA) requires the audio description specifically; 1.2.3 allows a text alternative as a fallback.

**WCAG 2.2 change:** No change.

---

### SC 1.2.4 — Captions (Live) (Level AA)
**Intent:** Provide captions for all live audio content in synchronised media.

**Passes when:** Real-time captions provided (CART or equivalent).

**WCAG 2.2 change:** No change.

---

### SC 1.2.5 — Audio Description (Prerecorded) (Level AA)
**Intent:** Provide audio description for all prerecorded video content in synchronised media.

**Passes when:** An audio description track describes all significant visual information not available from the audio alone.

**WCAG 2.2 change:** No change.

---

### SC 1.2.6 — Sign Language (Prerecorded) (Level AAA)
**Intent:** Provide sign language interpretation for all prerecorded audio content in synchronised media.

**WCAG 2.2 change:** No change.

---

### SC 1.2.7 — Extended Audio Description (Prerecorded) (Level AAA)
**Intent:** Where pauses in foreground audio are insufficient for audio descriptions, provide extended audio description (video paused to allow description).

**WCAG 2.2 change:** No change.

---

### SC 1.2.8 — Media Alternative (Prerecorded) (Level AAA)
**Intent:** Provide a full text alternative for all prerecorded synchronised media and video-only media.

**WCAG 2.2 change:** No change.

---

### SC 1.2.9 — Audio-only (Live) (Level AAA)
**Intent:** Provide an alternative for live audio-only content (e.g. live captioning or text stream).

**WCAG 2.2 change:** No change.

---

## Guideline 1.3 — Adaptable

### SC 1.3.1 — Info and Relationships (Level A)
**Intent:** Information, structure, and relationships conveyed through presentation can be programmatically determined or available in text.

**Applies to:** Headings, lists, tables, form labels, groupings, emphasis, required fields, data relationships.

**Passes when:**
- Headings use `<h1>`–`<h6>` (not styled `<div>` or `<p>`)
- Lists use `<ul>`, `<ol>`, `<dl>`
- Data tables use `<th>` with `scope`, and `<caption>` where needed
- Form inputs are associated with `<label>` via `for`/`id` or wrapping
- Related inputs grouped with `<fieldset>` and `<legend>`
- Required fields indicated programmatically (e.g. `aria-required="true"` or `required`)
- Visual emphasis (bold, italic) conveyed via semantic elements (`<strong>`, `<em>`) where meaning is intended

**Fails when:**
- Headings created with CSS-styled `<div>` or `<p>` elements
- Table structure conveyed visually only (no `<th>`, no `scope`)
- Form labels are placeholder text only
- `<b>` or `<i>` used where semantic emphasis is intended (use `<strong>` / `<em>`)
- Layout tables used for data

**WCAG 2.2 change:** No change.

**Related SC:** 4.1.2, 2.4.6

---

### SC 1.3.2 — Meaningful Sequence (Level A)
**Intent:** When the sequence of content affects its meaning, the correct reading sequence can be programmatically determined.

**Passes when:** The DOM order reflects the logical reading order, so that when CSS is removed the content still makes sense.

**Fails when:** Visual layout achieved via CSS creates a reading order that differs from DOM order, causing confusion when CSS is absent (e.g. screen reader or reflow context).

**WCAG 2.2 change:** No change.

---

### SC 1.3.3 — Sensory Characteristics (Level A)
**Intent:** Instructions don't rely solely on sensory characteristics (shape, colour, size, location, orientation, sound).

**Passes when:** Instructions include non-sensory identifiers (e.g. "Click the Submit button" not "Click the green button").

**Fails when:** "Click the round icon on the right" with no other identifier; "See the red items" as the only way to find errors.

**Note:** SC 1.4.1 covers use of colour specifically.

**WCAG 2.2 change:** No change.

---

### SC 1.3.4 — Orientation (Level AA)
**Intent:** Content does not restrict its view and operation to a single display orientation (portrait or landscape), unless a specific orientation is essential.

**Passes when:** Page works in both portrait and landscape. If orientation is locked, there is an essential reason (e.g. piano app).

**Fails when:** CSS or JS forces a single orientation without an essential reason; content is inaccessible when device orientation changes.

**WCAG 2.2 change:** No change.

---

### SC 1.3.5 — Identify Input Purpose (Level AA)
**Intent:** The purpose of each input field collecting personal information can be programmatically determined.

**Passes when:** `autocomplete` attribute set to the appropriate token (e.g. `autocomplete="email"`, `autocomplete="given-name"`) for inputs collecting personal data.

**Fails when:** Personal data inputs lack `autocomplete` attributes, preventing autofill and assistive technology from identifying the field purpose.

**Reference:** [WHATWG autocomplete token list](https://html.spec.whatwg.org/multipage/form-control-infrastructure.html#autofill)

**WCAG 2.2 change:** No change.

---

### SC 1.3.6 — Identify Purpose (Level AAA)
**Intent:** The purpose of UI components, icons, and regions can be programmatically determined.

**Passes when:** Landmarks, icons, and components have unambiguous programmatic roles/labels. Icons supplemented with text or ARIA labels conveying their purpose.

**WCAG 2.2 change:** No change.

---

## Guideline 1.4 — Distinguishable

### SC 1.4.1 — Use of Colour (Level A)
**Intent:** Colour is not used as the only visual means of conveying information, indicating an action, prompting a response, or distinguishing a visual element.

**Passes when:**
- Required fields indicated by asterisk AND label text (not colour alone)
- Error states indicated by icon or text in addition to red colour
- Charts use both colour and pattern/label to distinguish data series
- Links distinguishable from surrounding text by underline or other non-colour indicator

**Fails when:**
- "Fields marked in red are required" — colour alone
- "The green bars show sales" — colour alone in a chart legend
- Links distinguished from body text only by colour (no underline, no other indicator)

**WCAG 2.2 change:** No change.

**Related SC:** 1.4.3, 1.4.11

---

### SC 1.4.2 — Audio Control (Level A)
**Intent:** If any audio plays automatically for more than 3 seconds, a mechanism to pause, stop, or control volume must be available.

**Passes when:** Auto-playing audio has a pause/stop control, or volume control independent of system volume, within reach at the top of the page.

**Fails when:** Background audio plays without a user control; control is not keyboard accessible.

**WCAG 2.2 change:** No change.

---

### SC 1.4.3 — Contrast (Minimum) (Level AA)
**Intent:** Text and images of text have sufficient contrast against their background.

**Requirements:**
- Normal text (< 18pt / < 14pt bold): **4.5:1 minimum**
- Large text (≥ 18pt or ≥ 14pt bold): **3:1 minimum**
- Logotypes: exempt
- Decorative text with no informational value: exempt
- Inactive UI components: exempt

**Passes when:** Contrast ratio at or above the required threshold for the text size.

**Fails when:** Contrast falls below threshold; placeholder text treated as normal text (placeholder is often exempt but should still aim for 4.5:1 for usability).

**How to calculate:** Use the WCAG relative luminance formula: Contrast = (L1 + 0.05) / (L2 + 0.05) where L1 is the lighter colour. Tools such as the Colour Contrast Analyser (TPGi) or browser DevTools implement this formula. Note: APCA is a separate algorithm proposed for WCAG 3.0 — do not use APCA values to assess WCAG 2.2 conformance.

**WCAG 2.2 change:** No change. (Note: WCAG 3.0 will replace this with APCA, but 2.2 retains the existing formula.)

**Related SC:** 1.4.6 (enhanced, AAA), 1.4.11 (non-text)

---

### SC 1.4.4 — Resize Text (Level AA)
**Intent:** Text can be resized up to 200% without loss of content or functionality, without requiring assistive technology.

**Passes when:** Browser text zoom to 200% does not cause text to be clipped, truncated, or overlapping to the point of losing content.

**Fails when:** Fixed pixel font sizes prevent browser zoom from working; overflow hidden clips text at zoom; content disappears.

**Best practice:** Use relative units (`rem`, `em`, `%`) rather than fixed `px` for font sizes.

**WCAG 2.2 change:** No change.

---

### SC 1.4.5 — Images of Text (Level AA)
**Intent:** Use actual text rather than images of text, unless the image is essential or customisable.

**Passes when:** Logotypes (brand images with text) are acceptable. Text in images where the visual presentation is essential (e.g. a specific font style that cannot be replicated in CSS) is acceptable.

**Fails when:** Regular body content, headings, or UI labels are rendered as images of text when the same visual result could be achieved with CSS-styled real text.

**WCAG 2.2 change:** No change.

---

### SC 1.4.6 — Contrast (Enhanced) (Level AAA)
**Intent:** Stricter contrast requirement than 1.4.3.

**Requirements:**
- Normal text: **7:1 minimum**
- Large text: **4.5:1 minimum**

**WCAG 2.2 change:** No change.

---

### SC 1.4.7 — Low or No Background Audio (Level AAA)
**Intent:** For prerecorded audio-only content that contains speech: no background audio, or background audio is 20dB lower than speech, or background audio can be turned off.

**WCAG 2.2 change:** No change.

---

### SC 1.4.8 — Visual Presentation (Level AAA)
**Intent:** For blocks of text, users can select foreground/background colours, width ≤ 80 characters, no full justification, line height ≥ 1.5× font size, and text resizable to 200% without horizontal scrolling.

**WCAG 2.2 change:** No change.

---

### SC 1.4.9 — Images of Text (No Exception) (Level AAA)
**Intent:** Images of text only used for pure decoration or where the presentation is essential (stricter than 1.4.5 — logotypes not exempt here).

**WCAG 2.2 change:** No change.

---

### SC 1.4.10 — Reflow (Level AA)
**Intent:** Content can be presented without horizontal scrolling or loss of information at a width equivalent to 320 CSS pixels (equivalent to 400% zoom on a 1280px-wide viewport).

**Passes when:** At 320px wide equivalent, content reflows to single column and all content and functionality is available without horizontal scrolling.

**Fails when:** Fixed-width layouts require horizontal scrolling at 320px; content hidden or removed at this width; two-dimensional scrolling required for content that is not a data table, map, diagram, or video.

**WCAG 2.2 change:** No change.

---

### SC 1.4.11 — Non-text Contrast (Level AA)
**Intent:** Visual presentation of UI components and graphical objects has at least 3:1 contrast against adjacent colours.

**Applies to:**
- UI component boundaries (form field borders, checkbox borders, button outlines)
- States of components (focus indicators, selected states, checked checkboxes)
- Informational graphical objects (chart lines, icons conveying information)

**Passes when:** The visual boundary or state indicator of a component has ≥ 3:1 contrast against adjacent background.

**Fails when:**
- Form field border is grey on white with < 3:1 contrast (invisible to low-vision users)
- Focus indicator has < 3:1 contrast against background
- Icon conveying meaning has < 3:1 contrast against background
- Disabled components: exempt

**WCAG 2.2 change:** No change (but SC 2.4.11 in 2.2 extends focus-indicator requirements).

**Related SC:** 1.4.3, 2.4.7, 2.4.11

---

### SC 1.4.12 — Text Spacing (Level AA)
**Intent:** Content and functionality are preserved when users override text spacing properties.

**Test:** Apply all of the following simultaneously and verify no content is lost:
- Line height: 1.5× font size
- Spacing after paragraphs: 2× font size
- Letter spacing: 0.12em
- Word spacing: 0.16em

**Passes when:** All content and functionality available after applying the above values; no text clipped or overlapping.

**Fails when:** Fixed-height containers clip text; overflow hidden hides content; absolute-positioned elements overlap reflowed text.

**WCAG 2.2 change:** No change.

---

### SC 1.4.13 — Content on Hover or Focus (Level AA)
**Intent:** Where receiving pointer hover or keyboard focus triggers additional content (tooltips, sub-menus), that content must be: dismissible, hoverable, and persistent.

**Three requirements:**
1. **Dismissible:** User can dismiss the content without moving focus/hover (e.g. Escape key closes tooltip)
2. **Hoverable:** User can move the pointer over the triggered content without it disappearing
3. **Persistent:** Content stays visible until focus/hover is moved away, or user dismisses it, or the information is no longer valid

**Passes when:** Tooltip appears on hover/focus, stays while pointer is over it, and can be dismissed with Escape.

**Fails when:** Tooltip disappears as soon as pointer moves toward it; tooltip cannot be dismissed; tooltip disappears after a timeout.

**Exception:** If the triggered content is purely decorative, or native browser tooltips (title attribute) — user agent handles these.

**WCAG 2.2 change:** No change.

**Related SC:** 2.1.1, 4.1.3
