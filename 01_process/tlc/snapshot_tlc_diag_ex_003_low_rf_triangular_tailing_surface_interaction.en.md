---
snapshot_id: "TLC-DIAG-EX-003-LOW-RF-TRIANGULAR-TAILING-SURFACE-INTERACTION"
status: "stable"
language: en  
canonical_id: TLC-DIAG-EX-003-LOW-RF-TRIANGULAR-TAILING-SURFACE-INTERACTION
technique: "Thin Layer Chromatography"
topic: "Interpretability downgraded due to surface interaction–induced low Rf triangular tailing"
dependencies:
  - "TLC-003-ELUENT-SELECTION"
  - "TLC-004-PLATE-VISUAL-OBSERVATION"
related:
  - "TLC-DIAG-EX-001-FRONTING-BAND-AND-BASELINE-COMPRESSION"
---

# TLC-DIAG-EX-003 Low Rf Triangular Tailing: Interpretability Downgraded Due to Uncoupled Surface Interaction

## 1. Visual Observation

Through visual observation, the plate exhibits the following composite failure characteristics:

- **Core Distortion**: Critical sample spots in the low $R_f$ zone (usually $< 0.2$) exhibit distinct **upward-pointing triangular or flame-like** structures. The signal base is broad and non-convergent, tapering toward the top, showing a stable and directionally consistent morphology.
- **High-end Banding (Fronting Band)**: The comparison Lane at higher $R_f$ is flattened into a horizontal line, indicating that non-polar components in this development system have approached the upper elution limit.
- **Comparative Features**: Compared to `TLC-DIAG-EX-001`, the low $R_f$ spot morphology in this case shows clearer **directional consistency (tapering upward)**, suggesting that surface interactions dominate the migration behavior.

## 2. Diagnostic Conclusion and Logical Rationale

- **Interpretability Status**: **DOWNGRADED**
- **Failure Type**: **Surface Interaction Not Decoupled**

In this case, although the TLC plate generates identifiable migration structures, the morphology of the critical sample spots indicates a significant enhancement of the interaction with the silica gel surface, leading to:

- Systemic tailing and morphological distortion of the spots.
- Critical sample spots stagnating in the low $R_f$ zone, failing to enter the high-resolution projection window of 0.2–0.7.

Therefore, this plate is **unsuitable for judgments regarding spot count, purity, or quantification**, but under clearly restricted conditions, it can still be used for qualitative presence or trend observations.

## 3. Logical Differentiation from Related Patterns

**Key differences used to distinguish this case from `TLC-DIAG-EX-001` are as follows:**

| Pattern | Primary Contradiction | Priority Correction Logic |
| :--- | :--- | :--- |
| **EX-001 (Axis Compression)** | Overall polarity scale mismatch | Adjust eluent polarity ratio |
| **EX-003 (Triangular Tailing)** | **Molecular/surface interaction not decoupled** | **Introduce acid/base modifiers for chemical decoupling** |

## 4. Blocking and Downgrading Rules

- **Rule-001 (Morphological Downgrade)**: When critical sample spots exhibit stable flame-like or triangular tailing and $R_f < 0.2$, quantitative conclusions regarding "spot count (presence of trace impurities)" or "purity" based on this signal are prohibited.
- **Rule-002 (Pathway Locking)**: If spot distortion is primarily concentrated in components with specific functional groups rather than full-plate physical failure, it should be prioritized as "Surface Interaction Not Decoupled" rather than directly changing the eluent ratio.

## 5. Corrective Actions

The following measures are intended only to **attempt recovery of a secondary interpretable projection** and do not constitute an extended interpretation or supplementary diagnosis of the current plate:

1. **Acidic Decoupling Example**: If the sample is suspected to contain acidic groups (e.g., $-COOH$), a trace amount of **AcOH** can be added to the eluent to competitively weaken the interaction between the sample and the silica gel surface.
2. **Basic Decoupling Example**: If the sample is suspected to contain basic groups (e.g., $-NH_2$), a trace amount of **$Et_3N$** or **$NH_3 \cdot H_2O$** can be added.
3. **Expected Outcome**: Triangular spots originally stagnated near the baseline tend to converge into compact spot shapes and migrate to the effective projection interval of $R_f \approx 0.2–0.7$, thereby restoring higher-quality diagnostic conditions.

## 6. Physical Evidence

- **Adsorption Indicativity**: Stable and directionally consistent triangular tailing is usually highly correlated with surface-dominated migration distortion.
- **Coordinate Axis Distortion**: Due to uncoupled interactions, the apparent $R_f$ of the substance is systemically suppressed, deviating from its migration performance under ideal chromatographic conditions.
---

## Machine Annotation Candidate

```yaml
candidate_status: candidate_only_not_indexed
schema_version: risk_annotation_schema_v0.2
canonical_id: TLC-DIAG-EX-003-LOW-RF-TRIANGULAR-TAILING-SURFACE-INTERACTION
annotation_scope: diagnostic_example_candidate
source_language: en
candidate_parent: TLC-DIAG-001-INTERPRETABILITY-GATE
candidate_secondary_parent: TLC-003-ELUENT-SELECTION
jsonl_status: not_added
registry_status: not_added
taxonomy_status: example_terms_not_promoted

candidate_decision: >
  This diagnostic example reuses established TLC gate-level logic around
  interpretability downgrade, projection-axis validity, non-inferable low-Rf zones,
  and surface-interaction decoupling. The dominant new content is example-specific
  morphology: low-Rf triangular or flame-like tailing caused by unresolved
  molecule/silica surface interaction. It should remain candidate-only until
  multiple diagnostic examples demonstrate that this morphology supports a
  reusable review category beyond the current gate-level anchors.

reused_reasoning_anchors:
  - interpretability_gate
  - interpretability_downgraded
  - projection_axis_validity
  - non_inferable_zone
  - surface_interaction_decoupling
  - migration_distortion_control

candidate_example_terms_watchlist:
  - low_rf_triangular_tailing
  - flame_like_tailing
  - surface_interaction_not_decoupled
  - adsorption_dominated_migration
  - apparent_rf_suppression
  - morphology_based_downgrade

directly_supported_review_signals:
  - critical sample spots remain in the low Rf zone
  - critical spots show stable triangular or flame-like tailing
  - spot morphology indicates unresolved surface interaction
  - quantitative spot count, purity, and trace-impurity conclusions are blocked
  - qualitative presence or trend observation may remain only under restricted conditions
  - interpretability is downgraded rather than fully passed

machine_review_boundary: >
  Use this candidate only as a supporting example for downgraded interpretability
  caused by unresolved surface interaction. Do not convert acid/base modifier
  examples into SOP recommendations. Do not promote low-Rf triangular tailing or
  surface-interaction morphology terms into taxonomy until reuse across later
  examples confirms cross-example review value.
```