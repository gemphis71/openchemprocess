---
snapshot_id: "TLC-PRE-001-REPRESENTATIVENESS-SAMPLING"
status: "stable"
language: en  
canonical_id: TLC-PRE-001-REPRESENTATIVENESS-SAMPLING
technique: "Thin Layer Chromatography"
topic: "Entry Gate: Representativeness & Sampling"
dependencies: ["TLC-PRE-000-APPLICABILITY-STABILITY"]
priority: "High"
---

# TLC-PRE-001 Representativeness & Sampling Gate

## 1. Gate Definition
This Gate is used during the sampling stage to determine: **Whether the micro-sample intended for spotting truly represents the overall physical phase and composition of the reaction system.**

## 2. Core Assumption: Equivalency
The validity of TLC relies on the following assumption: **Sample composition at the spotting point = Total composition of the reaction system.**
Heterogeneous systems are the primary source of disruption to this assumption.

---

## 3. Mandatory Decision Logic for Heterogeneous Systems

### 3.1 Phase Separation Rule
- **Multi-phase Systems**: For solid-liquid or liquid-liquid systems, phases **must be spotted separately** (sampled individually) as a matter of principle.
- **Risk Warning**: "Mixed sampling" under high-speed stirring is generally non-representative. Such results should only be used as rough qualitative references, as they easily lead to directional errors in composition ratio.

### 3.2 Exemption Criteria: Irrelevant Phase Logic
Mixed sampling or single-phase sampling is permissible if the following conditions are met:
- The solid or second liquid phase is confirmed to be an **inert component** (e.g., inorganic salt precipitates, immiscible solvents).
- Target products and intermediates do not partition, adsorb, or react within the irrelevant phase.
- **Decision**: In this case, sampling bias does not constitute an informational misinterpretation.

### 3.3 High-Risk Alerts (Strictly Prohibited for Conversion Judgment)
TLC results will lead to systematic directional errors in the following scenarios:
- **Solubility Equilibrium Constraints**: Starting materials react while simultaneously dissolving.
- **Product Precipitation**: The product reaches saturation and precipitates during the reaction.
- **Surface Adsorption**: Components are strongly adsorbed onto catalysts (e.g., Pd/C) or inorganic supports, leading to artificially low liquid-phase signals.
- **Logical Conclusion**: In these cases, TLC represents only **"liquid-phase concentration changes"** rather than **"total conversion."**

---

## 4. Sampling Bias Management Principles

### 4.1 Statistical Sampling Recommendations (Scale-up Sampling)
When phase separation is impossible but qualitative monitoring is required, increase the sampling volume to reduce random error, followed by processing in `TLC-PRE-002-SAMPLE-PREPARATION-GATE`:
- **Laboratory Scale (≤1 L)**: Sample **1–5 mL** of the mixture.
- **Industrial Scale (≥1000 L)**: Sample **~1 L** of the mixture.



---

## 5. Gate Outputs

### ✅ Passed
- Sample possesses physical and proportional representativeness. Proceed to `TLC-PRE-002-SAMPLE-PREPARATION-GATE`.

### ⚠️ Conditional
- Sampling has only qualitative value. The experimental record must explicitly state: "Due to heterogeneity constraints, this TLC result is not used for quantitative conversion judgment."

### ❌ Failed
- Significant bias exists in the sampling process or phase monitoring is impossible. TLC results will lead to systematic misinterpretation; alternative analytical tools are required.

> **Core Motto**: The risk of TLC lies not in the "spotting," but in whether "this single drop represents the reaction."


## Machine Annotation

```yaml
schema_version: risk_annotation_schema_v0.2
canonical_id: TLC-PRE-001-REPRESENTATIVENESS-SAMPLING
annotation_scope: chapter_level
process_stage: tlc_pre_sampling_representativeness
source_language: en
machine_review_role: evidence_admissibility_gate

transition_model: reaction_system_to_spotted_micro_sample_projection

core_judgment: >
  The spotted micro-sample must represent the physical phase and composition of
  the reaction system. In heterogeneous systems, TLC may report only liquid-phase
  concentration or a biased sampled fraction rather than total conversion or total
  system composition.

risk_signals:
  - heterogeneous reaction system sampled as a single mixed spot
  - solid-liquid or liquid-liquid phases are not sampled separately
  - mixed sampling under high-speed stirring is treated as representative
  - starting material reacts while simultaneously dissolving
  - product precipitates during the reaction
  - product or intermediate partitions into another phase
  - target component adsorbs onto catalyst or inorganic support
  - liquid-phase TLC signal is treated as total conversion evidence
  - sampling bias may create directional error in composition ratio

reasoning_anchors:
  - representativeness_check
  - liquid_phase_only_projection
  - sample_state_projection

tlc_specific_review_triggers:
  heterogeneous_system: "solid-liquid or liquid-liquid system"
  mixed_sampling_risk: "high-speed stirred mixed sampling used as a composition proxy"
  solubility_equilibrium_constraint: "starting material dissolves while reacting"
  product_precipitation: "product reaches saturation and precipitates during reaction"
  surface_adsorption: "component adsorbs on catalyst or inorganic support"
  qualitative_only_record: "TLC result should not be used for quantitative conversion judgment under heterogeneity constraints"

expert_judgment_patterns:
  - Treat TLC sampling as an evidence-representativeness problem before interpreting reaction progress.
  - Treat heterogeneous-system TLC as phase-specific evidence unless physical and proportional representativeness is established.
  - Do not treat liquid-phase concentration changes as total conversion when dissolution, precipitation, adsorption, or partitioning is present.
  - Separate qualitative monitoring value from quantitative conversion judgment.

uncertainty_and_exceptions:
  - Mixed or single-phase sampling may be acceptable if the unsampled phase is demonstrated to be chemically irrelevant.
  - Sampling bias does not automatically invalidate all qualitative monitoring, but it can invalidate total conversion or composition-ratio inference.
  - Scale-up sampling volume guidance is TLC-specific and should not be generalized as a universal sampling rule.

machine_use: >
  Use this annotation to check whether a TLC sample is representative before using
  the plate as evidence for conversion, disappearance of starting material, product
  formation, or impurity ratio. If the sample does not represent the full physical
  and compositional state of the reaction system, restrict TLC interpretation to
  phase-specific or qualitative evidence.