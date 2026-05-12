# Laurence-wcag-referencing-skill-for-LLMs

A structured WCAG 2.2 accessibility reference guide designed to be used with AI assistants. Covers all 78 success criteria across Levels A, AA, and AAA, with supporting references for auditing, code generation, and conformance questions.

---

## What this is

This is a prompt package — a set of plain Markdown files that give an AI assistant accurate, structured knowledge of WCAG 2.2. When provided as context or a system prompt, the assistant uses these files to:

- Answer accessibility questions with citations to specific success criteria
- Audit code or designs and produce structured findings
- Generate accessible UI components with inline SC annotations
- Explain what any WCAG 2.2 criterion means, requires, and looks like in practice
- Answer conformance questions (what AA requires, partial conformance, legal context)

It is designed to be **LLM-agnostic** — the core content works with any AI assistant. LLM-specific setup instructions are in the [Installation](#installation) section below.

---

## Coverage

- **Specification:** WCAG 2.2 (W3C Recommendation, October 2023)
- **Levels:** A, AA, and AAA
- **Criteria:** All 78 success criteria
- **Includes:** The 9 criteria new or changed in WCAG 2.2, and the removal of SC 4.1.1

> **Note on Level AAA:** Most organisations target Level AA, which is the standard required by law and policy in most countries. Level AAA criteria are included for reference and represent best practice. They are not expected as part of a standard conformance target unless explicitly required.

---

## File Structure

```
Laurence-wcag-referencing-skill-for-LLMs/
├── SKILL.md                          Claude-specific entry point (required by Claude's skills
│                                     system). Contains YAML frontmatter and a pointer to GUIDE.md.
│                                     Ignored by all other LLMs — start with GUIDE.md instead.
├── GUIDE.md                          Main reference — task workflows, validation checklist,
│                                     audit format, communication standards
├── INDEX.md                          All 78 SC mapped to files; component → SC routing table
└── references/
    ├── principles/
    │   ├── 1-perceivable.md          SC 1.1.1 – 1.4.13
    │   ├── 2-operable.md             SC 2.1.1 – 2.5.8
    │   ├── 3-understandable.md       SC 3.1.1 – 3.3.9
    │   └── 4-robust.md               SC 4.1.2 – 4.1.3
    ├── sc/                           Individual file per success criterion (78 files + 4.1.1 removal)
    │   ├── 1.1.1.md
    │   ├── 1.4.3.md
    │   └── ... (one file per SC)
    ├── wcag-22-new.md                The 9 new/changed criteria in WCAG 2.2 (detailed)
    ├── audit-workflow.md             Structured audit process and findings template
    └── conformance.md                Levels, partial conformance, legal context
```

> **Why two entry point files?** `SKILL.md` is required by Claude's skills system and contains Claude-specific YAML metadata. `GUIDE.md` is the LLM-agnostic content that all assistants — including Claude — use for actual instructions. This keeps the core package neutral while satisfying Claude's technical requirement.

Each principle file covers its success criteria in full — intent, what passes, what fails, common mistakes, and related criteria. The assistant reads only the file(s) relevant to the question rather than loading everything at once.

---

## Installation

### Claude (claude.ai)

1. Download or clone this repository
2. Package the `Laurence-wcag-referencing-skill-for-LLMs/` folder as a ZIP file if not already
3. Go to [Customize → Skills](https://claude.ai/customize/skills)
4. Click the **+** button → **Create skill**
5. Upload the ZIP file
6. The skill will appear in your skills list and can be toggled on or off

To replace an existing version: click the **...** menu next to the old skill → **Delete**, then upload the new ZIP.

For Claude Code or API use, pass `GUIDE.md` as a system prompt and make the `references/` folder available in the working directory.

### ChatGPT / GPT-4 (OpenAI)

**Custom GPT:**
1. Go to [chat.openai.com/gpts](https://chat.openai.com/gpts) and create a new GPT
2. In the Instructions field, paste the contents of `GUIDE.md`
3. Upload the files from `references/` as knowledge files
4. Save and use the custom GPT for accessibility questions

**Standard conversation:**
Paste the contents of `GUIDE.md` at the start of a conversation, then paste the relevant principle file when asking a specific question.

### Gemini (Google)

**Gemini Gems:**
1. Open Gemini and create a new Gem
2. Paste the contents of `GUIDE.md` into the system instructions
3. Add the reference files as attached context
4. Save the Gem for reuse

**Standard conversation:**
Paste `GUIDE.md` and the relevant principle file at the start of a conversation.

### Copilot / Other assistants

Paste the contents of `GUIDE.md` as a system prompt or at the start of your conversation. Include the relevant `references/principles/` file for the criteria you are working with. The package is plain Markdown and works in any assistant that accepts text context.

### API / Custom integrations

Include `GUIDE.md` as your system prompt. Serve the reference files from your file system or storage and provide them to the model when the relevant topic is identified using the routing logic in `INDEX.md`.

---

## Usage examples

**Advisory question**
> "Does using placeholder text as a form label pass WCAG?"

The assistant consults SC 3.3.2 (Labels or Instructions) and SC 1.3.1 from `references/principles/3-understandable.md` and `1-perceivable.md`, and explains why placeholder-only labels fail.

**Code generation**
> "Build an accessible modal dialog in HTML."

The assistant checks the Component → SC mapping in `INDEX.md`, reads SC 2.1.1, 2.1.2, 2.4.3, and 4.1.2, builds the component, runs the validation checklist, and annotates the code with SC references.

**Audit**
> "Audit this form for accessibility issues."

The assistant follows the workflow in `references/audit-workflow.md` and returns a structured findings table with SC citations, pass/fail status, and evidence.

**Conformance question**
> "What do we need to meet WCAG 2.2 Level AA?"

The assistant reads `references/conformance.md` and explains the Level AA requirements in plain language.

---

## Contributing

Corrections, additions, and improvements are welcome.

- **Found an error in a criterion?** Open an issue with the SC number, the incorrect text, and a link to the relevant W3C documentation.
- **Missing a component in the routing table?** Open a pull request adding it to the Component → SC Mapping in `INDEX.md`.
- **WCAG update?** When a new version of WCAG is published, open an issue to track what needs updating.

Please keep all content LLM-agnostic. Any assistant-specific guidance belongs in this README only, not in `GUIDE.md` or the reference files.

---

## Licence

MIT — free to use, modify, and distribute. Attribution appreciated but not required.

---

## Maintainer

[Laurence] — contributions and corrections welcome via issues and pull requests.
