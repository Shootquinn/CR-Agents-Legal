# CR-Agents-Legal: Collaborative Reasoning for Contract Drafting, Redlining, and Legal Writing
By: Quinn Morley, Unleashed Robotics

A version of [CR-Agents](https://github.com/Shootquinn/CR-Agents) adapted for contract drafting, redlining, and legal writing. It drafts and reviews agreements, amendments, policies, acknowledgment forms, and compliance documents; redlines the counterparty's paper; and writes memos and legal-adjacent pieces such as articles. It works through AI-simulated expert teams and test-driven quality assurance. Runs on Claude Code.

**Scope.** The team drafts and reviews. It does not replace a lawyer. Anything that will be signed or relied on goes to licensed counsel in the governing jurisdiction.

CR-Agents-Legal works on United States law only. Its default company profile, which examples and Ground truth assume, is a Delaware corporation registered as a foreign corporation in Washington, where it does business.

Based on Nelson (2026), "Activating Expertise: Human-AI Teams for Collaborative Reasoning," implemented via spawned sub-agents with clean context windows per persona, with accumulated judgement calls to enable a persistent "pseudo-ego." Nelson's method is further augmented with the Test Driven Documentation method developed by the author in late 2025.

---

## Quickstart

Point Claude Code at CLAUDE.md. The entry point for every session is:

```
Read CLAUDE.md. Work through prompt0. Here is my work order: [paste work order or point to file]
```

Or more simply:

```
Read CLAUDE.md. Work through prompt0. Today we're drafting a mutual NDA from this term sheet.
```

That is the entire entry point. CLAUDE.md bootstraps the session: it tells the orchestrator where to find the operational guide, the gameplan, and the accumulator. prompt0 verifies tools and establishes session capabilities. The team assembles, builds a gameplan for your review, writes a test suite, and begins executing. You approve each step before the next one starts.

After compaction or a new session, the recovery incantation is the same: "Read CLAUDE.md, work through prompt0, and read the gameplan."

---

## Why prompt0 Exists

Claude Code arrives relatively unskilled compared to browser Claude. It cannot open PDFs without help, does not know your formatting rules, and has no document production skills out of the box. It relies on web-fetches for capabilities that browser Claude has built in. prompt0 bridges this gap by verifying tool availability (Python, Node.js, Pandoc, LibreOffice), loading the document production toolkit, and confirming the method documents are present. Without it, you spend the first 15 minutes of every session watching Claude Code fumble with basic file operations.

---

## The Team

Fifteen personas anchored to biographical reference material form the standing roster. Each runs as a spawned sub-agent with its own clean context window, receiving only the material relevant to its task. The biographical anchors are the mechanism: a persona grounded in a specific practitioner's published work and documented approach activates that domain knowledge with precision.

| Persona | Anchor | Role | Wave |
|---------|--------|------|------|
| The Manager | W. Edwards Deming | Opens and closes each working loop cycle. | Bookends |
| The Software Engineer | Kent Beck | Test suite design, workflow architecture. | 1 |
| The Engineer | Adam Steltzner | Tooling, technical exhibits, empirical verification, engineering reporting copy. | 1 |
| The Drafter | Tina L. Stark | Translates the deal into contract concepts; writes operative text. | 1 / Drafting |
| The Doctrinalist | Arthur L. Corbin | Formation, interpretation, conditions, remedies. | Drafting / 1 |
| The Commercial Lawyer | Karl N. Llewellyn | Uniform Commercial Code (UCC) Article 2, sale of goods, course of dealing, usage of trade. | Drafting / 1 |
| The Government Contracts Lawyer | Ralph C. Nash Jr. and John Cibinic Jr. | Federal Acquisition Regulation (FAR), agency supplements, clause flow-down. | Drafting / 1 |
| The Contract Editor | Kenneth A. Adams | Contract language: categories, defined terms, ambiguity. | Drafting |
| The Writer | Denis Diderot | Manuscript composition: arc, order, and prose. | Writing |
| The Editor | John McPhee | AI-writing detection and removal, sentence-level editing. | Writing / 1 (audit mode) |
| The Systems Engineer | Frederick P. Brooks Jr. | Conceptual integrity. | 2 |
| The Designer | Don Norman | Design review of structure and rendered pages; judges echo-site script output. | 2 |
| The Fact-Checker | Snopes managing editor | Citation and source verification. | 2 |
| The Litigator | Joseph D. Jamail Jr. | Reads the draft as opposing counsel. | 2 |
| The Judge | Ruth Bader Ginsburg | Reads the draft as the tribunal; enforceability, dispute resolution. | 2 / 1 on a named question |

The seven legal personas (The Drafter, The Doctrinalist, The Commercial Lawyer, The Government Contracts Lawyer, The Contract Editor, The Litigator, and The Judge) are untested: none has yet run on a real task, so treat their output as a first draft for the counsel review the Scope line requires.

Four waves run a step. Wave 1 does technical analysis and writes the first draft and the reporting copy. The **drafting wave** handles operative text: the legal reviewers review The Drafter's first draft, The Drafter revises, and The Contract Editor edits. The **writing wave** handles prose and is unchanged from CR-Agents: terse reporting copy from the specialists, composed by The Writer, polished by The Editor. Wave 2 reviews both.

Productive tensions are structural: The Drafter vs. The Litigator, The Litigator vs. The Judge, The Doctrinalist vs. The Contract Editor, The Government Contracts Lawyer vs. The Fact-Checker, The Contract Editor vs. The Writer, plus the CR-Agents pairs. Do not resolve these, except The Litigator vs. The Judge and The Fact-Checker vs. the domain persona, which The Manager settles (operational guide A.9). Disagreement between the other pairs is information.

**The Recruiter.** Spawned when a task requires expertise outside the standing roster (for example, a patent specialist anchored to Giles S. Rich). For genre gaps a standing persona can cover, the guide's tuning blocks (A.13.4) sharpen the persona instead.

---

## Workflow

```
Work Order / Change Order / Ask
        |
        v
   CLAUDE.md ---------> Bootstraps session, pointers to all files
        |
        v
   prompt0.md --------> Environment setup, tool checks, method docs
        |
        v
   Gameplan -----------> Created BEFORE execution; user reviews
        |
        v
   Test Suite ---------> Pass/fail criteria; The Software Engineer reviews before production
        |
        v
   Execution ----------> Wave 1, integration, drafting and writing waves, Wave 2 review
        |
        v
   Inter-Step Gate ----> The Manager closes; user approves before next step
        |
        v
   Delivery
```

Every step produces reviewable documents on disk. The accumulator preserves persona history across spawns and sessions. If the context window compacts mid-session, CLAUDE.md provides the recovery sequence.

---

## Files Included

| File | Purpose |
|------|---------|
| `CLAUDE.md` | Bootstrap. Read first. File pointers, process rules, recovery protocol. |
| `prompt0.md` | Environment setup. Windows/encoding rules, tool checks, document toolkit. |
| `method/operational_guide.md` | How to run the method. Standing roster, spawn templates, working loop, wave rules. |
| `method/tdd_method.md` | Test-driven documentation. Defines how test suites are built and used. |
| `supplements/contract-drafting.md` | Building blocks, categories of contract language, defined terms, ambiguity, compliance-document rules, scriptable checks. Loaded into every Drafter and Contract Editor spawn. |
| `supplements/signs_of_ai_writing.md` | AI writing detection. Severity-ordered categories. Loaded into every Editor spawn. |
| `supplements/writing-guides/style.md` | Prose style and register. Loaded into every Writer spawn. |
| `supplements/writing-guides/style-reference.md` | Punctuation, quoting, abbreviations, usage glossary. Lookup only, loaded on demand. |
| `supplements/writing-guides/structure.md` | Document architecture: arc, openings, resolutions, information order. |
| `supplements/writing-guides/structure-reference.md` | Condensing, verb and word lists, revision checklists, limitations placement. Lookup only. |
| `supplements/writing-guides/reporting-copy.md` | Ordering rules for reporting copy. Loaded into Engineer spawns that produce prose, into The Drafter's drafting notes, and into The Contract Editor's notes. |
| `templates/gameplan.md` | Blank gameplan. Ground truth, Author decisions, objectives, steps, progress log. |
| `templates/accumulator.md` | Blank accumulator. Per-persona contribution history. |
| `templates/persona_tunings.md` | Blank tuning-block file (guide A.13.4). |
| `templates/work_order_drafter.md` | Prompt for drafting work orders in web chat before handing to Claude Code. |
| `claude-docx-bundle/` | Document production toolkit. docx and pdf creation, validation, comments, tracked changes. |
| `claude-docx-bundle/docx_style.md` | Formatting rules. Default: Times New Roman 12pt. |

---

## Customizing the Document Style

The default formatting style is defined in `claude-docx-bundle/docx_style.md` (Times New Roman 12pt, specific heading hierarchy, APA 7 citations). To use your own style:

1. Place a .docx file in the project root with "STYLE" in the filename (e.g., "USE THIS STYLE.docx").
2. The toolkit detects it automatically and uses it as the formatting reference.
3. If no user style file is found, the default applies.

You can also edit `claude-docx-bundle/docx_style.md` directly to change the defaults.

---

## What You Need to Know

The human is a team member, not a director. Your job is creative origination, evaluative judgment, and reflective practice. The team handles execution. You approve or redirect at each gate.

Gameplans are created before execution and may take a couple iterations to get right. This is normal and cheap. Fixing a missing section in a gameplan costs minutes; fixing it in a draft costs hours.

The one-step gate is enforced: after The Manager closes a step, Claude Code stops and reports. It does not open the next step until you say so. Use this time to provide feedback, adjust the gameplan, or flag issues.

Work orders can be drafted in Claude web chat using `templates/work_order_drafter.md` before handing them to Claude Code for execution.
