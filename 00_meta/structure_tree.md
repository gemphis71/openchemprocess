# OpenChemProcess — Structure Tree (v0.1)

> **Status:** exploratory, intentionally flexible
>
> This structure tree represents the *current working map* of OpenChemProcess.
> It is expected to evolve as real problems are encountered.
> No directory or naming choice in this document should be considered final.

---

## 1. Purpose of the Structure Tree

The goal of this structure tree is **not completeness or correctness**, but:

* to separate *different types of knowledge* early
* to avoid mixing observations, interpretations, and decisions
* to provide enough scaffolding so content can grow without chaos

This is a **navigation aid**, not a frozen architecture.

---

## 2. Top-Level Structure (v0.1)

```
OpenChemProcess/
├─ 00_meta/
├─ 01_process/
├─ 02_observation/
├─ 03_data_schema/
├─ 04_rules/
├─ 05_cases/
└─ README.md
```

Only these seven entries are proposed at the top level.
They are intentionally broad and may be renamed, merged, or split later.

---

## 3. Top-Level Directories — Intent (Not Specification)

### 00_meta/  (🟢 conceptually stable)

**What belongs here:**

* project-level descriptions
* glossary drafts
* evolution notes

**What does NOT belong here:**

* chemical content
* schemas
* rules

This directory anchors *why* the project exists, not *what it contains*.

---

### 01_process/  (🟡 likely to evolve)

**What belongs here:**

* reaction steps
* unit operations
* process sequences

This directory describes **what is done**, independent of how success or failure is judged.

Sub-structure is intentionally undefined at v0.1.

---

### 02_observation/  (🟢 stable concept, flexible contents)

**What belongs here:**

* TLC observations
* HPLC / LCMS results
* physical observations (color, phase, gas evolution)

This directory contains **what is observed or measured**, without interpretation.

Example future subfolders (not commitments):

```
02_observation/
├─ tlc/
├─ hplc/
├─ lcms/
└─ physical/
```

---

### 03_data_schema/  (🟡 experimental)

**What belongs here:**

* CSV / JSON / YAML schemas
* field definitions
* controlled vocabularies

Schemas are expected to change frequently during v0.x.
Backward compatibility is *not* a requirement at this stage.

---

### 04_rules/  (🟡 deliberately postponed)

**What belongs here (later):**

* heuristics
* interpretation rules
* decision logic

At v0.1, this directory may remain empty.
Its existence prevents premature mixing of rules into data or observations.

---

### 05_cases/  (🟡 organic growth)

**What belongs here:**

* real project excerpts
* anonymized case studies
* end-to-end examples

Cases serve as *integration tests* for the structure.
If cases do not fit, the structure—not the case—should be questioned.

---

## 4. README.md (Root)

The root README should answer only:

1. What OpenChemProcess is
2. What kind of problems it addresses
3. How this repository is expected to evolve

It should not document internal schemas or rules.

---

## 5. Explicit Non-Goals (v0.1)

At this stage, the structure tree does **not** attempt to:

* optimize for regulatory submission
* mirror LIMS or ELN systems
* predict future AI implementations
* enforce strict naming conventions

---

## 6. Evolution Notes

* Directory names may change
* Directories may be merged or split
* Empty directories are acceptable

The only requirement is that **different knowledge types remain separable**.

---

*End of Structure Tree — v0.1*
