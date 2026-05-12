# WCAG 2.2 Conformance

Reference for conformance levels, what conformance means, partial conformance, and exceptions.

---

## Conformance Levels

WCAG 2.2 defines three levels of conformance:

### Level A (Minimum)
The most basic web accessibility features. Failure to meet Level A SC creates barriers that make content inaccessible or unusable for many users.

**Required for:** Any claim of WCAG conformance. No organisation can claim WCAG conformance without meeting all Level A criteria.

**Number of SC in WCAG 2.2:** 30 Level A criteria.

---

### Level AA (Standard)
The level most widely adopted for legal compliance, public sector requirements, and accessibility policies worldwide.

**Required for:**
- EU Web Accessibility Directive (public sector)
- EN 301 549 (European accessibility standard for ICT)
- ADA / Section 508 (USA, for federal agencies and federally funded content)
- Australian WCAG obligations (government websites)
- Most corporate accessibility policies
- App Store accessibility guidelines (Apple, Google)

**Includes:** All Level A criteria + Level AA criteria.

**Number of SC in WCAG 2.2:** 20 Level AA criteria (50 total including Level A).

---

### Level AAA (For Reference)
The highest level of WCAG criteria. Level AAA is **not expected as a blanket conformance target** — the W3C itself notes that it is generally not possible to satisfy all Level AAA criteria for all types of content.

Level AAA criteria are included in this skill as a reference because they represent best practice, and some organisations choose to meet individual AAA criteria for specific components, audiences, or content types — for example, a government health service targeting users with cognitive disabilities might adopt SC 3.3.5 (Help) or SC 3.3.8 (Accessible Authentication Enhanced).

**Unless you or your organisation have specifically committed to Level AAA, you do not need to worry about AAA criteria.** When they come up in this skill, they are flagged clearly and noted as reference only.

**Number of SC in WCAG 2.2:** 28 Level AAA criteria (78 total including A and AA).

---

## What Conformance Requires

A page **conforms** to WCAG 2.2 at a given level when:

1. **All pages** satisfy all SC at the target level (and lower levels)
2. **All content** is included, unless it is third-party content outside the author's control
3. **Accessibility-supported technologies** are used to deliver the content (i.e. the techniques used are supported by user agents and assistive technologies users actually have access to)
4. **No accessibility-supported technology is required** that the user may not have

A single failure of a Level A SC means the page does not conform to WCAG 2.2 at any level.

---

## Partial Conformance

Where full conformance cannot be achieved, organisations can make a **partial conformance claim**:

### Partial Conformance — Third Party
A page does not conform because third-party content is included that is not under the author's control and is not relied upon.

> "This page would conform to WCAG 2.2 Level AA except that the embedded social media widget is third-party content outside our control."

**Requirements for this claim:**
- The non-conforming content must genuinely be outside the author's control
- It must not be relied upon (users can still access all core functions without it)

### Partial Conformance — Language
A page does not conform because it is translated into a language for which accessibility-supported content technologies do not exist for that language.

---

## Accessibility Statements

Organisations typically publish an **accessibility statement** that:

1. States the standard they target (e.g. WCAG 2.2 Level AA)
2. Identifies known non-conformances
3. Explains any disproportionate burden claims
4. Provides a contact mechanism for accessibility issues
5. States when the statement was last reviewed

**Note:** An accessibility statement is not itself a conformance claim. A conformance claim requires all pages to fully meet the criteria.

---

## Disproportionate Burden (EU / Public Sector)

Under the EU Web Accessibility Directive, public sector bodies may invoke a **disproportionate burden** exception where the cost or effort of making content accessible is disproportionate to the benefit, taking into account:

- The organisation's size and resources
- The estimated cost vs benefit
- The frequency of use of the content by disabled users
- The availability of alternatives

This is a legal/policy determination — not a technical accessibility question. Content claimed under disproportionate burden must still be made accessible where reasonably possible.

---

## Content Covered by WCAG

WCAG applies to:

- Web pages and web applications
- Documents published on the web (PDFs, Word documents available for download)
- Native mobile apps (via mobile accessibility standards that reference WCAG principles)
- Embedded media and tools

**WCAG does not apply to:**
- Third-party content not under the author's control and not relied upon
- Content archived more than 10 years ago (EU directive exception for public sector)
- Live broadcasts (real-time audio/video — though captions for live content are Level AA)

---

## WCAG 2.2 and Previous Versions

| Version | Status | Key difference |
|---|---|---|
| WCAG 2.0 | Superseded but still referenced in some laws | 61 SC, no mobile-specific criteria |
| WCAG 2.1 | Still valid; WCAG 2.2 is backward compatible | Added SC for mobile, cognitive, low vision |
| WCAG 2.2 | Current Recommendation (October 2023) | Removed 4.1.1; added 9 new SC |
| WCAG 3.0 | In development (not yet a Recommendation) | Will replace the pass/fail model with scoring |

**Backward compatibility:** If content meets WCAG 2.2, it also meets WCAG 2.1 and 2.0 (with the exception of SC 4.1.1, which was removed in 2.2 but existed in 2.1 and 2.0).

---

## Frequently Asked Questions

**Q: Do we need to meet AAA?**
No, unless your policy requires it or you are targeting specific audiences (e.g. older users, users with cognitive disabilities) for whom AAA SC provide significant benefit. AA is the standard expectation.

**Q: Does WCAG apply to PDFs?**
Yes. PDFs published on the web are in scope. PDF accessibility maps to WCAG principles (tagged PDFs, reading order, alt text, form labels, etc.) and is also covered by PDF/UA (ISO 14289).

**Q: Does WCAG apply to mobile apps?**
WCAG 2.2 is written for web content, but its principles apply to mobile. EN 301 549 (Europe) and Section 508 (USA) both reference WCAG principles for native mobile apps. WCAG 3.0 will have broader platform coverage.

**Q: Our site fails one AA criterion — can we still claim Level A conformance?**
Yes. Level A conformance only requires Level A criteria. A failure of an AA criterion does not affect an A conformance claim — but it does prevent an AA claim.

**Q: We use an overlay/widget that claims to fix accessibility — does that count?**
No. Automated overlay tools cannot achieve or guarantee WCAG conformance. Overlays may introduce additional barriers and have been widely rejected by the accessibility community. Conformance must be achieved in the base content.
