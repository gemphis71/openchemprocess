---
snapshot_id: "TLC-002-SPOTTING-OPERATION"
status: "stable"
language: en  
canonical_id: TLC-002-SPOTTING-OPERATION
technique: "Thin Layer Chromatography"
topic: "Spotting Methodology"
dependencies: ["TLC-001-SPOTTING-LAYOUT", "TLC-PRE-002-SAMPLE-PREPARATION-GATE"]
---

## 1. Scope
This Snapshot defines the standard specifications for **TLC Spotting Operations**. It assumes sample stability, representativeness, and a single-phase homogeneous solution.

## 2. Tools and Concentration Standards

### 2.1 Capillary Selection
- **Preferred ID**: **0.5 mm** (Optimal balance between anti-clogging and stability).
- **Optional**: 0.3 mm.

### 2.2 Recommended Concentration
- **Target Range**: **0.2–0.3 M** (Working range: 0.1–0.5 M).
- **High Concentration**: Systems >0.5 M should be diluted to the target range to prevent uncontrolled spot expansion.

## 3. Spotting Motion and Control
- **Standard Motion**: Light contact → Micro-pause → Rapid vertical lift. Rely on capillary action; avoid pressing or lateral friction.
- **Qualified Spot Size**: Initial diameter ~**0.5 mm**; ideal post-development diameter **1–2 mm**.
- **Failure Criteria**: Spots >2 mm are considered signal distortion and lack semi-quantitative value.

### 3.1 Pre-processing Integration
If chemical pre-processing is mandated by `TLC-PRE-002-SAMPLE-PREPARATION-GATE`:
- **In-situ Processing**: Follow the recipe sequence defined in `TLC-TECH-001-QUENCH-RECIPES`. The **quench agent must be spotted first** to pre-wet the silica; the sample is then **over-spotted** on the same position before the agent fully evaporates.
- **Ex-situ Processing**: After completion of the chemical transformation defined in `TLC-TECH-001-QUENCH-RECIPES` within a sampling vial, the resulting homogeneous solution is treated as a standard sample following the spotting protocols of this document.

## 4. Re-spotting (Multiple Loading)
- **Limits**: Generally ≤3 times; strictly **never exceed 5 times**.
- **Modes**:
  - **Continuous Touch**: For $R_f < 0.3$ where the spotting solvent has low propelling power.
  - **Point-Dry-Point**: For high polarity solvents or samples prone to rapid diffusion.

## 5. Drying Criteria
- **Physical Indicator**: Flip the plate; the **wet mark on the back of the glass** must completely disappear.
- **Methods**: Cold air is preferred. Hot air (50–60 °C) for heat-stable samples. Prolonged drying (5–15 min) for high-boiling solvents like DMSO/DMF.

## 6. Diagnostic Flags
To be recorded for AI or manual analysis:
- **Overload**: Excessive spot size causing saturation.
- **Tailing**: Long tailing or Inverted Triangle/Tear-drop shapes.
- **Lateral Drift**: Non-vertical migration of the spot.

> **Core Definition**: Spotting is the process of encoding a chemical system into a controlled, interpretable spatial signal.
---

## Machine Annotation Candidate

```yaml
candidate_status: candidate_only_not_indexed
schema_version: risk_annotation_schema_v0.2
canonical_id: TLC-002-SPOTTING-OPERATION
annotation_scope: operation_validity_candidate
source_language: en
candidate_parent: TLC-PRE-002-SAMPLE-PREPARATION-GATE
candidate_secondary_parent: TLC-004-PLATE-VISUAL-OBSERVATION
jsonl_status: not_added
registry_status: not_added
taxonomy_status: operation_terms_not_promoted

candidate_decision: >
  This chapter contains useful review logic about spotting as spatial signal
  encoding, but the current text is operation-heavy and includes capillary size,
  spotting motion, spot diameter, re-spotting limits, and drying method details.
  It should remain candidate-only until its review value can be separated from
  TLC operating specifications and reused by diagnostic examples.

reused_reasoning_anchors:
  - sample_preparation_gate
  - visual_data_object_generation
  - migration_distortion_control

candidate_example_terms_watchlist:
  - spatial_signal_encoding
  - spot_size_distortion
  - spotting_overload
  - repeated_spotting_distortion
  - drying_completeness_check
  - lateral_drift

directly_supported_review_signals:
  - spotting assumes sample stability, representativeness, and homogeneous solution state
  - excessive spot size causes signal distortion
  - high concentration may cause uncontrolled spot expansion
  - repeated spotting can distort spatial signal encoding
  - incomplete drying may create migration distortion
  - overload, tailing, and lateral drift should be recorded as diagnostic flags

machine_review_boundary: >
  Use this candidate only as a supporting operation-validity reference. Do not
  convert capillary selection, spotting motion, re-spotting limits, drying method,
  or concentration recommendations into Machine Reviewer SOP instructions or
  global taxonomy rules. Consider future promotion only if diagnostic examples
  repeatedly reuse spotting-related validity logic.
```