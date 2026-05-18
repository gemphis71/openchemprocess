---
snapshot_id: "TLC-PRE-002-SAMPLE-PREPARATION-GATE"
status: "stable"
language: en  
canonical_id: TLC-PRE-002-SAMPLE-PREPARATION-GATE
technique: "Thin Layer Chromatography"
topic: "Entry Gate: Sample Preparation & Quench"
dependencies:
  - "TLC-PRE-000-APPLICABILITY-STABILITY"
  - "TLC-PRE-001-REPRESENTATIVENESS-SAMPLING"
priority: "High"
---

# TLC-PRE-001 Sample Preparation & Quench Gate

## 1. Gate Definition
Provided that the sample has met the criteria for TLC applicability (TLC-PRE-000-APPLICABILITY-STABILITY) and representativeness (TLC-PRE-001-REPRESENTATIVENESS-SAMPLING), this Gate determines: **Whether the sample must undergo pre-processing (such as quenching, dilution, or matrix adjustment) within the "sampling → spotting → development" timeframe to prevent ongoing reaction or informational distortion caused by system factors.**

This Gate only adjudicates **Requirement / Permission / Prohibition**; it does not define specific operational methods (detailed procedures are covered in subsequent process documentation).

## 2. Implicit Time and Environmental Scales (Decision Basis)
All judgments are based on the following unavoidable experimental facts:
- **Time Scale**: Sampling → Spotting → Entry into the developing chamber typically takes **30–60 seconds**.
- **Environmental Factors**:
  - Rapid temperature rise to Room Temperature (RT).
  - Exposure to ambient air and humidity.
  - **Silica Surface Activity**: Contains mildly acidic silanol groups (Si–OH), which possess catalytic or reactive properties.

**If a sample undergoes non-negligible chemical changes within these scales, pre-processing is mandatory.**

---

## 3. Quench Decision Logic

### 3.1 Mandatory Quenching
If any of the following conditions are met, **spotting without quenching = Gate Failure**:
- Extremely fast reaction rates (half-life $t_{1/2}$ in minutes or faster).
- Presence of highly reactive intermediates (strong nucleophiles/electrophiles, organometallic species, active redox species).
- High sensitivity to trace moisture, protons, or thermal transitions to RT.

**Decision Conclusion**: TLC results without quenching merely reflect "stochastic transformations after spotting" and do not represent the true state of the reaction system.

### 3.2 Legal Quench Forms
When Section 3.1 is triggered, the following two forms are permitted:
- **In-situ (On-plate) Quench**: Only applicable for low concentrations where the quenching exotherm is negligible.
- **Ex-situ (In-vial) Rapid Quench**: Reacting with a quenching agent in a sampling vial prior to spotting.

### 3.3 Allowed without Quench
- The reaction has been clearly terminated or quenched.
- The sample is a thermodynamically stable product or intermediate inert to air and silica.

---

## 4. Concentration & Dilution Gate

### 4.1 Standard Working Window
- **0.1–0.5 M**: Regarded as the standard TLC concentration window. Direct spotting is permitted.

### 4.2 Mandatory Dilution
Dilution (or ex-situ quenching) is mandatory if:
- Reaction concentration is **≥ 0.5 M**.
- High concentration leads to suspension, overloading, or uncontrollable spot diameter.
- **Decision Conclusion**: Spotting without dilution = Gate Failure.

### 4.3 Constraints on In-situ Quenching
- **Mandatory Constraint**: On-plate quenching is only permitted for equivalent concentrations of **0.1–0.5 M**.
- For high-concentration systems, relying solely on in-situ quenching is prohibited (leads to incomplete quenching and "ghost spots"); ex-situ complete quenching is required.

---

## 5. Solvent and System Matrix Judgment

Pre-processing (e.g., evaporation, displacement, or neutralization) is mandatory if system factors significantly distort migration behavior (Rf shift, spot diffusion, severe tailing):

- **High-boiling/Highly Polar Solvents**: e.g., DMSO, DMF, NMP.
- **Interfering Components**: Free water, strong acids, or strong bases.
- **Compatibility Principle**: Solvents introduced during pre-processing must be compatible with the eluent; neutralization must maintain a homogeneous system. If pre-processing itself introduces uncontrollable precipitation or new reactions, TLC is no longer applicable.

---

## 6. Gate Outputs

### ✅ Passed
- The sample is chemically inert within the TLC timeframe, and system factors do not cause migration distortion. Proceed to `TLC-002-SPOTTING-OPERATION` (Physical Operation).

### ⚠️ Conditional
- Must undergo specific pre-processing (Quench/Dilution/Solvent Swap) before spotting. 
- **Cross-reference**: For specific chemical quench recipes (e.g., MeOH, AcOH), refer to **`TLC-TECH-001-QUENCH-RECIPES`**.
- Details must be noted in experimental records.

### ❌ Failed
- Continuous transformation or system-induced uncontrollable distortion. TLC use is prohibited.

> **Gate Motto**: The prerequisite for TLC is not "spotting well," but "ensuring that both chemistry and migration behavior are controlled the moment the sample hits the plate."

---

## Machine Annotation

```yaml
schema_version: risk_annotation_schema_v0.2
canonical_id: TLC-PRE-002-SAMPLE-PREPARATION-GATE
annotation_scope: chapter_level
process_stage: tlc_pre_sample_preparation
source_language: en
machine_review_role: evidence_admissibility_gate

transition_model: admissible_sample_to_controlled_spotting_input

core_judgment: >
  TLC sample preparation is an evidence-admissibility gate. After applicability
  and representativeness have been established, the sample must be chemically and
  physically controlled within the sampling-to-spotting-to-development timeframe.
  If ongoing reaction, high concentration, incomplete quench, solvent matrix, or
  system components distort the chemical state or migration behavior, the TLC
  result cannot be treated as a faithful diagnostic projection.

risk_signals:
  - sample undergoes non-negligible chemical change during TLC preparation window
  - unquenched fast reaction is spotted directly
  - highly reactive intermediate remains active during sampling or spotting
  - sample is highly sensitive to trace moisture, protons, or room-temperature transition
  - unquenched TLC result reflects stochastic transformation after spotting
  - reaction concentration exceeds TLC working concentration window
  - high concentration causes suspension, overload, or uncontrolled spot diameter
  - in-situ quench is used beyond its concentration applicability boundary
  - high-boiling or highly polar solvent distorts migration behavior
  - free water, strong acid, or strong base distorts Rf or spot morphology
  - pre-processing introduces precipitation or new reaction

reasoning_anchors:
  - observation_validity_gate
  - sample_state_projection
  - sample_preparation_gate
  - quench_requirement_check
  - dilution_requirement_check
  - matrix_compatibility_check
  - migration_distortion_control

tlc_specific_review_triggers:
  preparation_time_window: "sampling to spotting to development typically takes 30-60 seconds"
  mandatory_quench_context: "fast reactions, highly reactive intermediates, or strong sensitivity to moisture, protons, or thermal transition"
  working_concentration_window: "0.1-0.5 M as TLC working concentration window"
  high_concentration_trigger: "reaction concentration >= 0.5 M or uncontrolled spot diameter / suspension / overload"
  in_situ_quench_constraint: "on-plate quench permitted only within low equivalent concentration where quench heat and incomplete quench do not dominate"
  matrix_distortion_context: "DMSO, DMF, NMP, free water, strong acid, or strong base may distort Rf, diffusion, or tailing"

expert_judgment_patterns:
  - Treat sample preparation as a precondition for TLC evidence admissibility, not as a downstream interpretation step.
  - Treat quench, dilution, and matrix adjustment as controls over chemical-state preservation and migration-state validity.
  - Do not interpret unquenched fast-reaction TLC as the original reaction state.
  - Do not use a high-concentration or matrix-distorted spot as semi-quantitative TLC evidence.
  - Separate requirement / permission / prohibition review from specific quench or spotting recipes.

uncertainty_and_exceptions:
  - Direct spotting may be admissible when the sample is chemically inert within the TLC time window and matrix effects do not distort migration.
  - Conditional pre-processing restores TLC admissibility only if it yields a homogeneous and chemically defined sample input.
  - TLC-specific concentration and time windows should not be generalized as global analytical rules.

machine_use: >
  Use this annotation after TLC-PRE-000 and TLC-PRE-001 have passed. Decide whether
  the sampled material must be quenched, diluted, or matrix-adjusted before
  spotting. If chemical state preservation or migration validity is not controlled,
  downgrade or reject downstream TLC interpretation rather than treating the plate
  as reliable evidence.
```