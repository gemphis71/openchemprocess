---
snapshot_id: "TLC-003-ELUENT-SELECTION"
status: "stable"
language: en  
canonical_id: TLC-003-ELUENT-SELECTION
technique: "Thin Layer Chromatography"
topic: "Eluent Selection Logic"
dependencies:
  - "TLC-PRE-002-SAMPLE-PREPARATION-GATE"
  - "TLC-000-ORIGIN-LINE"
  - "TLC-001-SPOTTING-LAYOUT"
  - "TLC-002-SPOTTING-OPERATION"
---

# TLC-003 Eluent Selection Logic

## 1. Core Definition
In TLC, the eluent is not a neutral medium but the core variable that determines **how material migration behavior is projected onto the plate coordinate system**. Selecting an eluent is essentially choosing an appropriate **"Information Projection Axis"** to reveal polarity differences between compounds in an interpretable manner.

## 2. Eluent as an "Information Projection Axis"
In standard silica systems, the eluent consists of a **highly polar component** (driving elution power) and a **low polarity component** (stretching the resolution range). Within a stable range, the eluent ratio and $R_f$ maintain a stable correlation, forming a predictable polarity scale.

## 3. Standard Non-Aqueous Systems: Predictable Polarity Scales

### 3.1 EtOAc / Heptane System
A highly regular projection axis used to establish the **relative polarity order of compounds**.
- **Failure Criteria**: Components remaining at the baseline in low-polarity ratios (exceeding range); all components running at the front in high-polarity ratios (information compression).
- **Applicable Boundaries**: The correlation between ratio and $R_f$ holds only when spot shapes are normal and free from tailing or strong surface adsorption. If spot shapes are abnormal, this correlation automatically expires and must not be used for polarity inference.

### 3.2 EtOAc / DCM System
A tighter mid-to-high polarity projection axis. Used to quickly cover the standard organic polarity zone within a shorter ratio-scanning range.

## 4. Aqueous High-Polarity System: Organic / Inorganic Discrimination

### 4.1 DCM / MeOH / H₂O (Triphasic Mixture)
An extreme high-polarity axis valued specifically for the rapid **discrimination of substance types (Organic vs. Inorganic)**.
- **Typical Ratio for Stable Homogeneous Window**: **DCM / MeOH / $H_2O$ = 3 / 2 / 0.5 (v/v)**.
- **Risk Warning**: Deviation from this window is prone to phase separation (heterogeneity), rendering interpretation invalid.
- **Interpretation Logic**: Organic compounds collectively shift upward, while inorganic salts and highly ionic species remain at the baseline.
- **Prohibited Logic**: Prohibited for the fine separation of organic compounds or conversion rate reasoning.

## 5. Eluent Acid/Base Modification: Decoupling Surface Interactions

### 5.1 Micro-Acidic Environment (Adding AcOH)
Used to weaken strong hydrogen bonding between acidic functional groups and silica Si–OH. The convergence of a spot into a round shape confirms the presence of strong polar acidic characteristics.

### 5.2 Micro-Basic Environment (Adding $NH_3$)
Used to mask acidic sites on the silica surface, reducing tailing for basic spots. If ammonia causes phase separation or $R_f$ drift, the system is deemed an unstable interpretation condition.

### 5.3 Logical Constraints
The addition of acid or base is intended solely to decouple projection distortions caused by plate surface interactions. It is not equivalent to substantive chemical treatment of the sample; results are valid only within the context of TLC interpretation.

## 6. Resolution & Non-inferable Zones

### 6.1 High Resolution Zone
- **Effective $R_f$ Range**: Prioritize information falling between **0.2 – 0.7**.
- **Rationale**: In regions near the baseline (< 0.2) or solvent front (> 0.7), resolution decreases significantly due to non-linear adsorption and edge effects; these regions are not recommended for precise reaction progress (conversion rate) inference.

### 6.2 Failure Criteria
The following cases are prohibited from entering subsequent DIAGNOSTIC logic:
- Extremum compression (all spots < 0.2 or all spots > 0.8).
- Physical drift (phase separation or loss of $R_f$ regularity due to excessive moisture).
- Severe tailing where acid/base decoupling has not been applied.

## 7. Boundary Statement
This Snapshot defines eluents as projection tools; it **does not** provide "optimal recipes" for specific compounds or explain reaction mechanisms.
---

## Machine Annotation

```yaml
schema_version: risk_annotation_schema_v0.2
canonical_id: TLC-003-ELUENT-SELECTION
annotation_scope: chapter_level
process_stage: tlc_projection_axis_selection
source_language: en
machine_review_role: projection_axis_validity_gate

transition_model: eluent_selection_to_information_projection_axis

core_judgment: >
  In TLC, eluent selection defines the information projection axis rather than
  serving as a neutral solvent choice. A TLC plate is interpretable only when the
  eluent system projects compound differences into a usable Rf range without
  compression, phase instability, unresolved surface interaction, or loss of Rf
  regularity.

risk_signals:
  - eluent system fails to project components into effective Rf range
  - all critical spots remain near the baseline
  - all critical spots run near the solvent front
  - Rf ratio correlation is used despite abnormal spot shape
  - spot tailing or strong surface adsorption invalidates polarity inference
  - aqueous or highly polar eluent mixture becomes phase-separated
  - organic versus inorganic discrimination axis is used for fine organic separation
  - eluent acid or base modification is treated as substantive sample chemistry
  - severe tailing remains without surface-interaction decoupling
  - projection-axis failure is used for conversion or mechanism inference

reasoning_anchors:
  - interpretability_gate
  - projection_axis_validity
  - information_projection_axis
  - projection_axis_compression
  - rf_regular_projection
  - surface_interaction_decoupling
  - non_inferable_zone

tlc_specific_review_triggers:
  effective_rf_range: "prioritize interpretable information between Rf 0.2 and 0.7"
  baseline_compression: "critical spots remain below Rf 0.2"
  front_compression: "critical spots run above Rf 0.8"
  phase_instability: "aqueous high-polarity system deviates from stable homogeneous window and phase-separates"
  dcm_meoh_water_reference_window: "DCM / MeOH / H2O = 3 / 2 / 0.5 as TLC-specific homogeneous-window reference"
  acid_base_modification_boundary: "acid/base additives decouple surface interactions and do not constitute sample-structure proof"

expert_judgment_patterns:
  - Treat eluent selection as projection-axis selection before using Rf values for inference.
  - Treat baseline compression, front compression, and phase instability as projection-axis failures.
  - Do not infer polarity order when spot shape is abnormal or strong surface interaction dominates.
  - Use acid/base modification only as TLC surface-interaction decoupling evidence, not as definitive chemical structure proof.
  - Do not use an organic/inorganic discrimination axis for fine organic separation or conversion inference.

uncertainty_and_exceptions:
  - Rf and eluent-ratio correlation is valid only under stable spot morphology and regular projection behavior.
  - High-polarity aqueous systems may be useful for organic/inorganic discrimination but not for fine organic-component interpretation.
  - TLC-specific eluent ratios and Rf intervals are review triggers, not universal chromatography rules.

machine_use: >
  Use this annotation to review whether the eluent system creates a valid
  information projection axis before TLC interpretation. If the eluent causes
  compression, phase instability, unresolved surface interaction, or loss of Rf
  regularity, restrict or reject downstream polarity, component-count, conversion,
  or mechanism inference.
```