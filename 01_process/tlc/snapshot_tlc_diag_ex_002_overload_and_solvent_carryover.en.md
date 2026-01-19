---
snapshot_id: "TLC-DIAG-EX-002-OVERLOAD-AND-SOLVENT-CARRYOVER"
status: "stable"
technique: "Thin Layer Chromatography"
topic: "Non-interpretable plate due to spotting overload / high-boiling solvent carryover"
dependencies:
  - "TLC-PRE-002-SAMPLE-PREPARATION-GATE"
  - "TLC-002-SPOTTING-OPERATION"
  - "TLC-004-PLATE-VISUAL-OBSERVATION"
---

# TLC-DIAG-EX-002 Spotting Overload and Polar Solvent Carryover: Systemic Failure via Streaking

## 1. Visual Observations

Through visual inspection, this plate exhibits clear signs of physical failure morphology:

- **Longitudinal Streaking (Streak / Smear)**: Multiple lanes exhibit continuous, elongated columnar signals stretching upward from the baseline, completely losing a converged "spot" structure.
- **Boundary Annihilation**: Signal edges are blurred and overlap with one another, making it impossible to distinguish between different components or impurities; the plate surface lacks identifiable migratory structures.
- **Physical Traces**: Visible signs of abnormal moisture or deformation in the baseline area suggest residual solvent that has not fully evaporated from the spotting zone.

## 2. Diagnostic Status and Logical Rationale

- **Interpretability Status**: **REVOKED / Non-interpretable**
- **Failure Type**: **Spotting Confounder**

In this case, the failure is attributable to the overlap of several spotting-related factors:

- **High-Boiling Polar Solvent Carryover**: Spotting solvents were not sufficiently dried, significantly perturbing local migration behavior during development and causing signals to be stretched into continuous bands.
- **Sample Overload**: The sample load per unit area is too high, exceeding the effective adsorption and separation capacity of the silica gel surface, leading to physical smearing during migration.

## 3. Mandatory Blocking Rules

- **Rule-001 (Morphological Blocking)**: If signals exhibit "full-path streaking" and lack any converged spot structure, it is judged as a physical failure. Inferences regarding polarity, purity, or component counts are prohibited.
- **Rule-002 (Solvent Traceability)**: If traces of undried solvent or abnormal diffusion are observed in the spotting zone, refer back to `TLC-PRE-002-SAMPLE-PREPARATION-GATE` and revoke the interpretability of the plate.
- **Rule-003 (Resolution Failure)**: When the width of a streak is significantly larger than the original spotting scale, the method is judged unable to provide effective resolution under the current conditions.

## 4. Corrective Actions

The following actions are intended only to **restore observability** and do not constitute an extension of interpretation or supplementary diagnosis of the current plate:

1. **Dilution and Solvent Replacement**: Use a low-boiling, low-viscosity solvent with good solubility to significantly dilute the sample, reducing both the load per unit area and the impact of solvent carryover.
2. **Forced Drying**: Use warm air, vacuum, or extended standing time after spotting to ensure high-boiling solvents have completely evaporated before development.
3. **Technological Shift Evaluation**: If streaking persists despite proper dilution and drying, TLC should be judged to have insufficient information density for this system; consider alternative analytical methods such as HPLC or LC-MS.

## 5. Physical Evidence

- **Local Migratory Distortion**: Residual solvent in the spotting zone significantly alters the initial migratory environment, causing migration behaviors that should be controlled by silica gel adsorption to be dragged along, thereby stripping the plate of its chromatographic interpretability.