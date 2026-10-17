# Persona tuning blocks: [project name]

See operational guide A.13.4. Each block is appended to the named persona's spawn prompt after the "Your role on this team" line and before SESSION HISTORY (A.3.1), for the waves in its header. The persona stays the same person; the block adds practice background and a working stance.

**Source of the material:** [files on disk that support each block; no biographical fact without a source]

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
- The Manager writes each block from sources on disk, and the human approves it before its first load. The Manager greps this file when building spawn prompts and lists the blocks loaded in his step-open file (`cr_scratch/step{N}_manager_open.md`).
- No block asserts regulatory text. A regulatory statement routes to a quoted source on disk or to The Fact-Checker.
- Do not add biographical facts to a block unless a source on disk supports them.
