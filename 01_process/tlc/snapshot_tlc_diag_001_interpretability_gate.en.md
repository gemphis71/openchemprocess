---
snapshot_id: "TLC-DIAG-001-INTERPRETABILITY-GATE"
status: "stable"
technique: "Thin Layer Chromatography"
topic: "Interpretability gate for TLC plate diagnostics"
dependencies:
  - "TLC-004-PLATE-VISUAL-OBSERVATION"
---

# TLC-DIAG-001 TLC Interpretability Gate

## 0. Definition and Scope

This Gate is used to determine whether a **developed and visualized TLC plate** is qualified to enter the subsequent interpretation process (DIAG-002). This document only adjudicates the status of the interpretability (PASS / DOWNGRADED / REVOKED / VOID) and is not responsible for interpreting specific chemical reaction results.

> **Important Note (Data Object Boundary)** > The object of adjudication for this Gate is the "visual data object generated on the current plate surface." Any change of staining reagent, re-staining, or re-development should be treated as a **new data input** and must be re-evaluated through this Gate.

---

## Gate-0 Visualization Validity

**Judgment Rules**
- A status of **REVOKED** is assigned if:
  - The contrast between the spot signal and the local background is extremely low, making it impossible for the human eye or machine to extract clear contours.
  - Background noise (e.g., excessive staining reagent, charring from over-baking) covers more than 30% of the effective area of the plate.

**Logical Rationale**
- This is the lowest-level physical gateway. If the visual object itself is unidentifiable, all subsequent morphological and logical judgments lose their material basis.

---

## Gate-1 Starting Material Projection Integrity

**Judgment Rules**
- If the Starting Material (SM) reference spot fails to form a definable and repeatable migration behavior (i.e., the vast majority of the signal remains at the origin, $R_f \approx 0$).
- **Result**: **Interpretability REVOKED**.

**Logical Rationale**
- Failure of the starting material to migrate means the origin projection was not generated, and the minimum physical reference for reaction monitoring is missing. 
- This is a **preemptive circuit-breaker gateway**; once triggered, no subsequent Gates are checked.

---

## Gate-2 Projection Axis Capacity Validity

**Judgment Rules**
- If critical spots fall entirely into information compression zones:
  - Low end: $R_f < 0.2$.
  - High end: $R_f > 0.8$.
- AND no distinguishable structures can be established within the effective projection interval of 0.2–0.7.
- **Result**: **Interpretability REVOKED**.

**Logical Rationale**
- There is a mismatch between the projection axis capacity and the system polarity; information entropy has been compressed at the physical layer, rendering inferences about spot count and relative proportions invalid.

---

## Gate-3 Spot Morphology Integrity

**Judgment Rules**
- If systemic physical failure morphologies appear: Banding, Streaking, or global shifting caused by residual high-boiling solvents.
- **Result**: **Interpretability REVOKED**.

**Logical Rationale**
- Chromatographic equilibrium was not established; physical failure takes precedence over any chemical interpretation or empirical judgment.

---

## Gate-4 Protocol Anchoring Integrity (Anchoring & Co-spot)

**Judgment Rules**
- In a reaction monitoring scenario, if the Co-spot (Spike) reference is missing, and the sample signal cannot be explicitly anchored or calibrated.
- **Result**: **Interpretability VOID (Logical Nullification)**.

**Logical Rationale**
- This is a protocol-layer failure. It is impossible to distinguish between mutually exclusive states: "Sample not spotted," "SM disappeared," or "$R_f$ shift caused by matrix effects".

---

## Gate-5 Surface Interaction and Low Rf Tailing

**Judgment Rules**
- If critical spots in the low $R_f$ zone ($< 0.2$) exhibit stable, directionally consistent triangular or flame-like tailing, and the **extension length of the tail along the migration direction** exceeds **0.2 $R_f$ units**.
- **Result**: **Interpretability DOWNGRADED**.

**Logical Rationale**
- Signal reliability is limited; quantitative inference or purity judgment based on spot morphology is prohibited. Only limited qualitative observation rights are retained.

---

## Gate-6 Numerical Judgment of Co-spot Anchoring Deviation

**Judgment Intervals (Based on $|\Delta R_f|$ between the SM reference spot and the SM component in the Co-spot)**
- **Strongly Anchored**: $|\Delta R_f| < 0.05$ → **PASS**.
- **Acceptable**: $0.05 \le |\Delta R_f| < 0.1$ → **CAUTION**.
- **Downgraded**: $0.1 \le |\Delta R_f| < 0.2$ → **DOWNGRADED**.
- **Unacceptable**: $|\Delta R_f| \ge 0.2$ → **REVOKED**.

> **Status Semantic Note** > **CAUTION** is a sub-state of **DOWNGRADED**, used to indicate that anchoring is unstable but still usable; it does not constitute an independent final status type.

---

## Priority Rules and Output Summary

| Triggered Gate | Priority | Final Status | Core Semantics |
| :--- | :--- | :--- | :--- |
| **Gate-0/1/2/3** | Ultra High | **REVOKED** | Physical/Chromatographic failure; interpretation prohibited |
| **Gate-4** | High | **VOID** | Logical reference broken; data invalid |
| **Gate-5/6** | Medium | **DOWNGRADED** | Signal distortion; interpretability restricted |
| **No Triggers** | - | **PASS** | Proceed to DIAG-002 for normal interpretation |

---

## Boundary Statement

This Gate only adjudicates whether interpretability is established; it does not provide any reaction mechanism, conversion rate, or structural judgment. All choice of interpretation pathways and chemical inferences belong to the scope of **DIAG-002**.