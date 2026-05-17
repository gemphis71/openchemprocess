---
snapshot_id: "TLC-001-SPOTTING-LAYOUT"
status: "stable"
language: en  
canonical_id: TLC-001-SPOTTING-LAYOUT
technique: "Thin Layer Chromatography"
topic: "Spotting Layout"
dependencies: ["TLC-000-ORIGIN-LINE"]
---

## 1. Core Discussion
This Snapshot defines the horizontal layout and logical semantics of a TLC plate. This layout establishes a "Relative Coordinate System" to infer the relationship between the reaction mixture and the starting materials.

## 2. Standard 4-Lane Layout

Based on best practices, spotting should follow this standard sequence (from left to right):

| Lane       | Label       | Composition                     | Logical Function                                                                                                                                                             |
| :--------- | :---------- | :------------------------------ | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Lane 1** | **Ref**     | Starting Material (SM)          | Provides absolute reference for $R_f$ and visualization.                                                                                                                     |
| **Lane 2** | **Spike**   | SM + Reaction Mixture           | **Co-localization & Calibration**: Eliminates $R_f$ shifts caused by matrix effects (e.g., pH, salts) to confirm the identity of spots in Lane 3 via synchronized migration. |
| **Lane 3** | **Sample**  | Reaction Mixture                | **Core Observation**: Monitors conversion rate, byproduct formation speed, and crude ratios.                                                                                 |
| **Lane 4** | **Product** | Product/Impurity Std (Optional) | Anchors the target product position to complete the coordinate system.                                                                                                       |

## 3. Spatial Constraints
- **Pitch (Lane Spacing)**: Recommended **3 mm - 6 mm**. High-density spotting allows more logical controls per plate but requires strict control of spot diameter to prevent overlapping.
- **Margin**: The distance from the outermost spots to the edge of the plate should be $\ge 5$ mm to minimize distortion caused by the **Edge Effect (Smiling Effect)**.

## 4. Machine Reasoning Logic
- **Matrix Shift Compensation**: Due to pH, salts, or byproducts in the reaction mixture, the migration of the SM in Lane 3 might shift slightly compared to Lane 1.
- **Spike Decision Rule**:
  - If a spot in Lane 3 shows a slight $R_f$ deviation, but the corresponding spot in Lane 2 (Spike) remains a single, cohesive, and unsplit spot, the AI shall conclude the displacement is caused by the matrix environment rather than a chemical change.
  - If Lane 2 displays two distinct spots or an elongated "double-spot" shape, they are identified as different chemical entities.
- **Conversion Inference**: The AI estimates conversion by calculating the intensity/area ratio between the SM spot and the Product spot in Lane 3.
---

## Machine Annotation

```yaml
schema_version: risk_annotation_schema_v0.2
canonical_id: TLC-001-SPOTTING-LAYOUT
annotation_scope: chapter_level
process_stage: tlc_lane_layout_and_reference_anchoring
source_language: en
machine_review_role: reference_layout_validity_gate

transition_model: lane_layout_to_relative_coordinate_and_reference_system

core_judgment: >
  TLC spotting layout defines the relative coordinate and reference system used
  to compare starting material, reaction mixture, co-spot, and optional product
  or impurity standards. Ref, Spike, Sample, and Product lanes create anchoring
  logic for identity consistency and matrix-shift compensation; without valid
  reference layout, presence/absence and identity interpretation become unstable.

risk_signals:
  - TLC plate lacks a starting-material reference lane
  - reaction sample is interpreted without co-spot anchoring when matrix shift is possible
  - sample lane Rf shift is interpreted as chemical change without spike comparison
  - spike lane splits into two spots or elongated double-spot morphology
  - product or impurity standard is missing when target position anchoring is required
  - lane spacing is too narrow and causes overlap
  - outer lanes are too close to plate edge and affected by edge distortion
  - matrix effect is ignored during identity consistency judgment
  - intensity or area ratio is used for precise conversion inference

reasoning_anchors:
  - reference_layout_validity
  - relative_coordinate_system
  - co_spot_anchoring
  - matrix_shift_compensation
  - identity_consistency_check
  - lane_geometry_validity
  - edge_effect_control
  - prohibited_quantitative_conversion

tlc_specific_review_triggers:
  standard_lane_set: "Ref / Spike / Sample / Product-or-impurity-standard"
  lane_spacing_reference: "recommended pitch 3-6 mm"
  edge_margin_reference: "outermost spots should be at least 5 mm from plate edge"
  spike_single_spot_logic: "single cohesive spike spot supports matrix-shift explanation"
  spike_split_logic: "two distinct spots or elongated double-spot shape indicates different entities"
  conversion_inference_boundary: "intensity/area ratio can support only rough trend or relative estimate, not precise conversion"

expert_judgment_patterns:
  - Treat TLC layout as a reference and anchoring system before interpreting spot identity.
  - Use spike behavior to distinguish matrix-shift displacement from chemical identity change.
  - Treat missing reference or missing co-spot as reduced identity-consistency authority.
  - Treat lane overlap and edge distortion as layout-level threats to interpretation.
  - Do not convert Lane 3 intensity or area ratio into precise conversion percentage.

uncertainty_and_exceptions:
  - Product or impurity standard lane may be optional if target identity is not being anchored in that plate.
  - Co-spot anchoring is most critical when matrix shift from pH, salts, byproducts, or reaction mixture effects is plausible.
  - Layout-based identity consistency is not definitive structural confirmation and must remain within TLC interpretation limits.

machine_use: >
  Use this annotation to check whether a TLC plate has a valid lane-reference
  layout before interpreting presence/absence, identity consistency, matrix shift,
  or reaction trend. If reference lanes, spike logic, lane spacing, or edge-margin
  validity are insufficient, downgrade identity and conversion-related conclusions.
```