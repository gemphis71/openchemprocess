---
snapshot_id: "TLC-DIAG-002-INTERPRETATION-PATHWAYS"
status: "stable"
technique: "Thin Layer Chromatography"
topic: "Permitted interpretation pathways after interpretability gate"
dependencies:
  - "TLC-DIAG-001-INTERPRETABILITY-GATE"
---

# TLC-DIAG-002 TLC Interpretation Pathways and Permitted Logic

## 0. Mandatory Precondition

This document applies only to TLC plates that have successfully **passed the `TLC-DIAG-001-INTERPRETABILITY-GATE`**.

- Plates in **REVOKED / VOID** status are strictly prohibited from entering this interpretation layer.
- Plates in **DOWNGRADED** status are permitted to use only the interpretation pathways explicitly marked as "Limited Use" within this document.

---

## A. Presence / Absence Determination

### A-1 Interpretive Objective
To determine whether a known substance (e.g., starting material or target product) **is still present or has disappeared**.

### A-2 Permitted Interpretation Methods
- Based on the presence or absence of a signal at a specific $R_f$ position.
- Judging based on the consistency or divergence across multiple visualization methods:
  1. UV observation (254 nm / 365 nm).
  2. Iodine staining response.
  3. At least one general or specific chemical staining reagent.

### A-3 Co-elution Risks (Overlap)
- High vigilance is required regarding the possibility of different chemical entities overlapping at the same $R_f$ position.
- Increased caution is mandatory when:
  - A spot is visible under UV but shows a completely different response in chemical staining, or vice versa.
- **Next-Phase Action**: If co-elution is suspected, once the initial determination is complete, the signal bifurcation must be verified in the next experimental cycle by changing the eluent polarity (elution strength) or switching to a chromatography system based on different principles.

### A-4 Interpretive Boundary
- Presence/absence determination is the core and permitted output of TLC.
- It is strictly forbidden to reach a "single component" conclusion based solely on a single staining or observation method.

---

## B. Relative Migration Order and Morphology

### B-1 Meaning of Vertical Order
- The vertical order of spots on a TLC plate only represents their relative migration ability under the current eluent system.
- This order can flip in different polarities or types of solvent systems and does not represent the intrinsic "strength" or "weakness" of a compound.

### B-2 Limitations of Staining Intensity
- Different compounds have vastly different response sensitivities to UV, iodine, or chemical stains.
- **Staining intensity (color depth) cannot directly represent molar content or purity.**

### B-3 Conditional Area-Content Relationship
- **Only when $R_f$ values are identical or very close**:
  - There is a rough positive correlation between the spot area and the substance content.
- This logic is a local, relative estimate and lacks physical meaning for comparisons across different $R_f$ regions.

---

## C. Identity Consistency Determination

### C-1 Interpretive Objective
To judge whether a specific signal in a sample possesses **physical identity** with a known starting material or reference standard.

### C-2 Basis for Judgment
- Consistency of $R_f$ position (must have passed the anchoring deviation judgment in `DIAG-001`).
- Synchronization of typical staining behaviors under the following multiple modes:
  - UV response color and intensity.
  - Iodine staining color and adsorption rate.
  - Discoloration characteristics and morphology of chemical stains.

### C-3 Interpretation Logic
- If multiple staining behaviors remain consistent at the same $R_f$ position, the confidence in the identity consistency conclusion is strengthened.
- If systemic differences in staining behavior exist, the identity must be judged as inconsistent or overlapping, even if the $R_f$ is the same.

---

## D. Process Trend Interpretation

### D-1 Interpretive Positioning
TLC is not used to output precise reaction rate constants. Its proper use is for qualitative or semi-quantitative process trend monitoring.

### D-2 Permitted Trend Content
- Gradual weakening of the starting material spot over the time axis.
- Gradual strengthening of the product spot over the time axis.
- Evolution patterns of impurity spots: monotonic increase (byproduct) or increase followed by decrease (intermediate).

### D-3 Accuracy Intervals (Empirical Boundaries)
- **Early to Mid-reaction (10%–80% conversion)**: TLC trend interpretation is relatively reliable.
- **Late-reaction (>80% conversion)**: Due to staining sensitivity limits, the accuracy of TLC interpretation drops significantly. The disappearance of the starting material spot does not represent 100% chemical conversion.

---

## E. Negative Constraints (Prohibited Interpretations)

The following interpretation pathways are strictly prohibited in all cases:

### E-1 Prohibited Quantitative Conversion
- It is forbidden to output precise conversion percentages or kinetic parameters based on TLC.
- Only "qualitative trends" or "relative consumption speed" judgments are allowed.

### E-2 Prohibited Intensity-Content Equivalence
- It is strictly forbidden to directly equate UV intensity, iodine depth, or chemical stain vividness with concentration or content.

### E-3 Limited Structural Inference
- **Permitted**: Assisting in judging the **acidic, basic, or neutral** properties of a substance based on spot morphology response to polarity (e.g., convergence after adding acid/base).
- **Prohibited**: Directly inferring specific functional group details or complete chemical structures based on TLC signals.

---

## 6. Boundary Statement

This document defines the permitted output space for TLC once the right to interpret has been established. All interpretations are empirical and conditional conclusions. If precise quantification or structural confirmation is required, one must switch to precision tools such as HPLC, LC-MS, or NMR.