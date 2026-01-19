---
snapshot_id: "TLC-DIAG-EX-005-STARTING-MATERIAL-STAGNATION-AND-POLARITY-GAP"
status: "stable"
technique: "Thin Layer Chromatography"
topic: "Interpretability revoked due to absence of starting material migration"
dependencies:
  - "TLC-001-SPOTTING-LAYOUT"
  - "TLC-003-ELUENT-SELECTION"
  - "TLC-004-PLATE-VISUAL-OBSERVATION"
related:
  - "TLC-DIAG-EX-001-FRONTING-BAND-AND-BASELINE-COMPRESSION"
  - "TLC-DIAG-EX-003-LOW-RF-TRIANGULAR-TAILING-SURFACE-INTERACTION"
---

# TLC-DIAG-EX-005 Starting Material Stagnation: Interpretability Revoked Due to Missing Starting Projection

## 1. Visual Observation

Through visual observation, the plate exhibits the following **decisive starting material failure characteristics**, accompanied by high-end morphological anomalies:

- **Starting Material Stagnation**: In Lane 1 (SM), the vast majority of the signal remains at the spotting origin, with only a very small amount of tailing moving upward. No definable migration center is formed, $R_f \approx 0$.
- **Accompanying Morphological Anomalies in Samples (Secondary Feature)**: Signals in the Co-spot and Sample lanes have migrated to the extremely high $R_f$ zone ($> 0.8$), with spot shapes showing flame-like or fronting compression trends. The concentration at the front is significantly higher, indicating a high probability of multi-component overlap.
- **Missing Effective Interval**: The plate fails to form stable references simultaneously associating the starting material and the samples within the high-resolution projection interval of 0.2–0.7.

Among these, the **failure of the starting material to form effective migration** constitutes the primary and sufficient condition for the non-interpretability of this plate.

## 2. Diagnostic Conclusion and Logical Rationale

- **Interpretability Status**: **REVOKED**
- **Failure Type**: **Starting Material Projection Failure**

In this case, because the starting material failed to leave the origin, the minimum physical projection required for reaction monitoring was not generated, directly leading to:

- Inability to confirm whether the starting material actually participated in the reaction or merely stagnated due to solubility/surface interaction factors;
- Inability to establish a comparable relationship between any migration signals in the sample lane and the starting material;
- Any inferences regarding "reaction occurred / not occurred / completed" lack a physical basis.

Even if visible migration signals exist in the sample lane, this plate logically **does not qualify to enter the interpretation process**.

## 3. Relation to Related Patterns

- **EX-001 (Axis Compression)**: Both the starting material and the sample can migrate, but both fall into the information compression zone, leading to resolution failure.
- **EX-005 (Starting Material Projection Failure)**: The starting material side fails to form any usable migration projection, and the reaction monitoring logic terminates at the starting point.

Therefore, EX-005 can be regarded as an **earlier and more stringent failure mode than EX-001**:  
Interpretability is directly revoked before even entering the discussion of "axis compression".

## 4. Mandatory Blocking Rules

- **Rule-001 (Starting Material Migration Prerequisite)**: If the starting material control spot fails to form a repeatable and definable migration (i.e., the vast majority of the signal remains at the baseline), the interpretability of the entire plate is directly revoked.
- **Rule-002 (Non-remediability of Sample Signals)**: Under the premise of starting material migration failure, any migration signals appearing in the sample or co-spot lanes shall not be used to compensate for or infer the reaction state.
- **Rule-003 (Priority Principle)**: Starting material projection failure is a pre-emptive failure for reaction monitoring; its blocking priority is higher than eluent selection, visualization methods, or surface interaction adjustments.

## 5. Corrective Actions

The following measures are intended only to **reacquire interpretability qualification** and do not constitute an interpretation of the current plate:

1. **Prioritize Restoring Starting Material Migration**: Enable the starting material spot to form stable migration by adjusting the development system or surface interaction conditions.
2. **Split Observation Axes Instead of Compromising**: Split the observation of starting materials and samples into different polarity systems to avoid attempting to cover both ends with a single compromised condition.
3. **Regenerate Data**: Before starting material migration conditions are met, the current plate data is logically non-reusable.

## 6. Physical Evidence

- **Origin Anchoring Failure**: The starting material did not leave the origin, resulting in the absence of the physical reference for reaction monitoring at the most fundamental level.
- **Information Irrecoverability**: Since the starting material projection was not generated, this development cannot obtain interpretative value through any visual post-processing or empirical remedies.