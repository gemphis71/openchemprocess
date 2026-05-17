---
snapshot_id: "TLC-000-ORIGIN-LINE"
status: "stable"
language: en  
canonical_id: TLC-000-ORIGIN-LINE
technique: "Thin Layer Chromatography"
topic: "Physical Baseline"
dependencies: ["TLC-PRE-001-REPRESENTATIVENESS-SAMPLING"]
priority: "Critical"
---

## 1. Definition and Purpose
The Origin Line is the physical baseline of a TLC experiment. It provides a uniform starting Y-coordinate for all samples, which is a logical prerequisite for calculating $R_f$ values and performing cross-lane comparisons.

## 2. Physical Specifications

### 2.1 Vertical Offset
- **Core Principle**: The height of the origin line must be high enough to **prevent the sample spots from being submerged** by the mobile phase.
- **Reference Value**: Typically set at **1.0 cm** from the bottom of the plate.
- **Invalidation Criteria**: If sample spots are submerged in the solvent, the data for those lanes will be marked as `Invalid`.

### 2.2 Horizontal Alignment
- **Standard**: The centers of all sample spots must be aligned on the same horizontal line.
- **Tolerance**: The vertical deviation between any two spots should be controlled within **2.0 mm**.
- **Impact**: Deviations exceeding this tolerance introduce artificial errors in relative $R_f$ calculations for AI models.

### 2.3 Marking Requirements
- Use a 2B pencil to mark the plate very lightly. 
- **Prohibited**: Do not score the silica layer (which disrupts capillary action) or use ink pens (which introduce chemical interference).

## 3. Spot Diameter
- **Ideal Range**: The initial diameter of the spot should be strictly controlled between **0.5 mm and 1.5 mm**.
- **Logical Significance**: Small initial diameters yield higher separation resolution and are critical for precise **Centroid Localization** in machine vision.
---

## Machine Annotation

```yaml
schema_version: risk_annotation_schema_v0.2
canonical_id: TLC-000-ORIGIN-LINE
annotation_scope: chapter_level
process_stage: tlc_coordinate_baseline_definition
source_language: en
machine_review_role: coordinate_system_validity_gate

transition_model: physical_origin_line_to_rf_coordinate_baseline

core_judgment: >
  The TLC origin line is the physical coordinate baseline required for Rf
  calculation, cross-lane comparison, and machine-readable spatial interpretation.
  If the origin line is submerged, misaligned, chemically contaminated, or unable
  to support reliable centroid localization, downstream Rf comparison and lane
  interpretation lose coordinate validity.

risk_signals:
  - sample spot is submerged by mobile phase
  - origin line does not provide a uniform starting Y-coordinate
  - vertical deviation between spot centers creates artificial Rf error
  - origin mark disrupts silica capillary behavior
  - ink or chemically interfering marker is used on the plate
  - initial spot diameter is too large for reliable centroid localization
  - cross-lane comparison is performed despite invalid origin-line geometry
  - Rf values are calculated from lanes with invalid physical baseline

reasoning_anchors:
  - coordinate_baseline_integrity
  - origin_line_validity
  - rf_coordinate_validity
  - cross_lane_comparison_validity
  - centroid_localization_validity
  - physical_marker_noninterference

tlc_specific_review_triggers:
  origin_line_reference_height: "typically 1.0 cm from plate bottom"
  lane_invalid_if_submerged: "sample spot submerged by mobile phase invalidates the lane"
  vertical_alignment_tolerance: "spot-center vertical deviation should be controlled within 2.0 mm"
  initial_spot_diameter_reference: "initial spot diameter ideally 0.5-1.5 mm"
  marker_constraint: "use light pencil marking; avoid scoring silica or using ink"

expert_judgment_patterns:
  - Treat the origin line as the physical baseline of the TLC coordinate system before interpreting Rf.
  - Treat submerged spots or invalid physical baseline as lane-level data invalidation.
  - Treat vertical misalignment as artificial Rf error rather than chemical migration difference.
  - Treat marker interference or silica damage as coordinate-system contamination.
  - Do not use TLC-specific geometric values as global chromatography rules.

uncertainty_and_exceptions:
  - A non-standard origin-line height may still be valid if sample spots remain above the solvent and coordinate geometry is preserved.
  - Small geometric deviations may be tolerated only when they do not affect the intended interpretive resolution.
  - Spot-diameter references are TLC visual-coordinate triggers, not general analytical requirements.

machine_use: >
  Use this annotation to check whether a TLC plate has a valid physical coordinate
  baseline before Rf calculation, cross-lane comparison, or machine-vision
  interpretation. If origin-line geometry, marker integrity, or spot localization
  validity fails, invalidate or downgrade affected lanes before downstream
  interpretation.
```