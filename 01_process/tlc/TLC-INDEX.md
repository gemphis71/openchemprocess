# Thin Layer Chromatography (TLC) — Module Index

This index enumerates all TLC-related snapshots in OpenChemProcess.
The authoritative identifier is `snapshot_id`; file paths and folder names are considered
implementation details and may change over time.

Unless otherwise noted, each snapshot is provided in paired `en` / `zh` variants
sharing the same `snapshot_id`.

---

## META Layer (Methodological Boundaries & System Positioning)

META snapshots define the interpretive scope, temporal limits, and system-level role
of TLC. They are not operational steps and apply globally to all TLC snapshots.

- **TLC-META-001-EARLY-DIAGNOSTIC-VALUE-AND-LIMITS**
- **TLC-META-002-DECISION-LATENCY-AND-FEEDBACK-STRATEGY**

---

## PRE Layer (Preconditions & Gates)

PRE snapshots define preconditions that must be satisfied before TLC observations
can be considered interpretable. They function as blocking or gating logic.

- **TLC-PRE-000-APPLICABILITY-STABILITY**
- **TLC-PRE-001-REPRESENTATIVENESS-SAMPLING**
- **TLC-PRE-002-SAMPLE-PREPARATION-GATE**

---

## CORE PROCESS Layer (Operational Snapshots)

These snapshots describe the core physical and procedural elements of TLC execution.

### Physical baseline (protocol level 000)
- **TLC-000-ORIGIN-LINE**

### Core operations
- **TLC-001-SPOTTING-LAYOUT**
- **TLC-002-SPOTTING-OPERATION**
- **TLC-003-ELUENT-SELECTION**
- **TLC-004-PLATE-VISUAL-OBSERVATION**

---

## DIAG Layer (Diagnostic Logic)

DIAG snapshots describe how TLC observations may (or may not) be interpreted.
They define diagnostic gates and structured interpretation pathways.

- **TLC-DIAG-001-INTERPRETABILITY-GATE**
- **TLC-DIAG-002-INTERPRETATION-PATHWAYS**

---

## DIAG-EX Layer (Diagnostic Examples)

DIAG-EX snapshots provide concrete diagnostic examples illustrating common
failure modes, artifacts, and misinterpretation patterns.

- **TLC-DIAG-EX-001-FRONTING-BAND-AND-BASELINE-COMPRESSION**
- **TLC-DIAG-EX-002-OVERLOAD-AND-SOLVENT-CARRYOVER**
- **TLC-DIAG-EX-003-LOW-RF-TRIANGULAR-TAILING-SURFACE-INTERACTION**
- **TLC-DIAG-EX-004-LOGIC-GAP-MISSING-SPIKE-AND-FRONTING-OVERFLOW**
- **TLC-DIAG-EX-005-STARTING-MATERIAL-STAGNATION-AND-POLARITY-GAP**

---

## TECH Layer (Technique Inserts)

TECH snapshots provide reusable technique-level inserts that may be referenced
by multiple process or diagnostic snapshots.

- **TLC-TECH-001-QUENCH-RECIPES**

---

## OBSERVATION Layer (Raw Experimental Assets)

Raw TLC plate images are stored under the observation layer
(e.g., `TLC_picture_ex_001–005`).

These assets:
- do **not** carry interpretive authority on their own
- are **not** indexed as snapshots
- should be referenced only from specific DIAG-EX snapshots or CASE narratives when needed

---

## Notes

- This index intentionally avoids hard-coded paths or folder names.
- If repository structure is reorganized, keep `snapshot_id` unchanged and this index remains valid.
- Bilingual (`en` / `zh`) files sharing the same `snapshot_id` are treated as one knowledge node.
