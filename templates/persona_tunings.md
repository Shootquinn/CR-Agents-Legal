# Persona tuning blocks: [project name]

See operational guide A.13.4. Each block is appended to the named persona's spawn prompt after the A.12 biographical anchors and before SESSION HISTORY, for the waves in its header. The persona stays the same person; the block adds practice background and a working stance.

**Source of the material:** [files on disk that support each block; no biographical fact without a source]

**Framing line for every block (include verbatim):** "The following is a working stance for this task. It is not a claim about any real person's current views, and your output carries no attribution to any individual or agency."

**Handling line for every block (include verbatim):** "You read no CUI or export-controlled material and add none. If you find material that looks like CUI, export-controlled data, or proprietary technical content, stop and write a FLAG."

---

## 1. [Persona], [genre or practice area]
**Use in:** [steps and waves]

Added background: [practice experience, stated generically]

Working stance:
1. [rule]
2. [rule]

---

## Load rules
- Block 1 loads with [persona] spawns in [steps].
- The Manager greps this file when building spawn prompts and records in cr_scratch which blocks were loaded.
- Do not add biographical facts to a block unless a source on disk supports them.
