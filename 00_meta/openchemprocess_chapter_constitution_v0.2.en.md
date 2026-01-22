# OpenChemProcess — Chapter Constitution & Writing Principles (v0.2)

> **Status:** active constitution  
> **Scope:** This document defines the _structural constitution_ of OpenChemProcess.  
> It constrains how Chapters are defined, how snapshots are organized, and how revisions are permitted.

---

## 0. Purpose and Scope

OpenChemProcess is **not** a knowledge taxonomy and **not** a process handbook.

Its goal is:

> **To record, in an engineering-verifiable manner, the recurring structural failure modes that emerge during scale-up of real chemical processes.**

Therefore:

- Chapters are **process stages with high failure density**, not topic collections
    
- Snapshots are **failure coordinate systems**, not compilations of best practices
    
- The project must actively resist degradation into SOPs, HAZOPs, or generic “process guidelines”
    

---

## 1. Primary Axis of Chapters: Irreversible Commitment

Top-level Chapters are organized around **process stages where irreversible commitment occurs**.

An irreversible commitment is defined as a point in real scale-up or production where:

- The system transitions from reversible experimentation to a committed state
    
- Subsequent adjustments, even if available, can no longer alter the final outcome
    

Typical examples include:

- **Early diagnostics (e.g., TLC):** No material commitment yet, but false confidence and decision paths are already locked in
    
- **Charging:** The first irreversible commitment, where addition sequence, mode, or rate eliminates effective control leverage
    
- **Quench / Workup:** The second irreversible commitment, often mistaken as “termination” but in fact a renewed bet
    

---

## 2. Two Global Meta-Axes (Mandatory Across All Chapters)

The following two axes are **not Chapters and not standalone content objects**.  
They are **mandatory evaluative dimensions** that every Chapter and snapshot must explicitly address.

### 2.1 T-axis: Tolerance Envelope

The T-axis answers:

- How much deviation can the system tolerate at this stage and still survive?
    
- How does deviation transition from _recoverable_ to _irrecoverable_?
    

Tolerance envelopes must be expressed as **conditional ranges and failure boundaries**, not as vague experiential judgments.

---

### 2.2 S-axis: Scale Sensitivity

The S-axis answers:

- Under scale-up, does the tolerance envelope shrink linearly, collapse nonlinearly, or disappear entirely?
    
- Which control levers that exist at small scale become nominally present but functionally ineffective at larger scale?
    

The focus of the S-axis is not the existence of scale effects, but **systematic deformation of the tolerance envelope during scale-up**.

---

## 3. Three Mandatory Criteria for Chapter Eligibility

A concept may be elevated to an **independent Chapter** only if **all three** of the following criteria are satisfied:

1. **Stage Criterion**  
    Does it correspond to an independent process stage in which failures can recur, rather than a single variable or condition?
    
2. **Envelope Criterion**  
    Does this stage possess its own tolerance envelope, with clearly definable survival conditions and failure boundaries?
    
3. **Scale Criterion**  
    Does this envelope undergo systematic collapse or deformation under scale-up, creating a structural disadvantage?
    

> If any criterion is not met, the concept should normally remain a risk dimension, structural axis, or subsection within an existing Chapter, rather than becoming a standalone Chapter.

---

## 4. Elements That Do Not Normally Constitute Independent Chapters

The following elements are often **critically important**, but by default should **not** be promoted to standalone Chapters.  
They must be embedded within the structural risk logic of relevant Chapters.

### 4.1 Thermal / Safety Variables (TMP / SAF)

- Classification: outcome variables
    
- Proper placement:
    
    - Failure boundaries within Chapters
        
    - Physical criteria for post-commitment recoverability
        
- Allowed structured representations:
    
    - Q_exo vs Q_cooling
        
    - ΔT_ad
        
    - Response surfaces mapping condition space to outcome space
        

---

### 4.2 Materials and Specifications (MAT / RAW)

- Classification: condition variables
    
- Proper placement:
    
    - Survival conditions
        
    - Failure boundaries
        
    - Concrete cases at the 002 level
        

Materials do not create failure by themselves; **failure emerges from how materials are used within specific process stages**.

---

### 4.3 Atmosphere and State Constraints (ATM)

- Classification: state constraints
    
- Proper placement:
    
    - Boundary conditions within specific Chapters
        
    - Descriptions of irreversible nodes
        

They should not be generalized into a standalone “environmental conditions” Chapter.

---

## 5. Internal Writing Rules for Chapters and Snapshots

All Chapters and snapshots must follow these uniform rules:

- **Level 001:** Structural risk and risk envelopes (non-binary, non–yes/no gates)
    
- **Level 002:** Concrete failure modes, experiential cases, and reproducible examples
    
- Failure-first orientation: start from scale-up failure structures, not best practices
    
- Survival is allowed, but survival conditions must be explicitly stated
    
- Files must remain open and appendable; closure is prohibited
    

---

## 6. Versioned Revision Rules (Strict Constraint)

This constitution may be revised only under the following constraints:

1. The full text and original reasoning of the prior version must be retrieved before revision
    
2. All revisions must result in a new version number (vX.Y)
    
3. Each revision must document:
    
    - Motivation for change
        
    - New evidence or counterexamples
        
    - Impact on existing Chapter classifications
        

> Unversioned structural changes or silent redefinitions are explicitly prohibited.

---

## 7. Runtime Self-Check Mechanism (Project-Level Convention)

During writing and extension, the following questions must be repeatedly enforced:

- Does the current content violate established Chapter boundaries?
    
- Have both the T-axis and S-axis been explicitly addressed?
    
- Is “importance” being incorrectly used as a substitute for stage-level qualification?
    

This document exists to **constrain the author and future collaborators (including AI systems)**, not for instructional purposes.

---

**End of Constitution (v0.2)**