---
snapshot_id: "WRKUP-003-SOLVENT-REMOVAL-DRIVEN-ACCUMULATION-AND-THERMAL-EXPOSURE-CONTROL"
status: "draft"
domain: "Process"
process: "Workup"
topic: "Solvent Removal–Driven Accumulation and Thermal Exposure Control (Hard Gate + Route Priority)"
level: "001"
language: en  
canonical_id: WRKUP-003-SOLVENT-REMOVAL-DRIVEN-ACCUMULATION-AND-THERMAL-EXPOSURE-CONTROL
dependencies:
  - "WRKUP-001-WORKUP-CONTROL-AUTHORITY"
  - "WRKUP-002-PARTITION-RATIO-DRIFT-INVENTORY-CONTROL"
  - "THR-001-THERMAL-CONTROL-AUTHORITY"
---

# WRKUP-003 | Solvent Removal–Driven Accumulation and Thermal Exposure Control

## 1 Design Intent and Review Objective

Concentration and solvent exchange are the last operations that still remain in the liquid-phase domain during workup. The control authority objective of this chapter is not simply solvent evaporation, but management of an irreversible trajectory: removal of volatile components forces the system composition to move along a defined path.

Along this trajectory the system may experience:

- nonvolatile accumulation  
- phase-behavior rewriting  
- thermal exposure accumulation  
- operational constraints imposed by equipment or transfer boundaries  

Concentration is therefore considered a high-risk and structurally unfavorable operation.

The dominant hazard pattern is:

High concentration + accumulated thermal exposure + enrichment of nonvolatile species (salts / acids / bases / high-boiling residues) + rewritten phase behavior or speciation.

### Process design objectives

- reduce total concentration time  
- minimize thermal exposure  
- reduce impurity interaction with the product during concentration  
- eliminate unnecessary heavy concentration through upstream design  

### Core review principle

Prefer reducing or bypassing the irreversible pathway:

extraction → concentration

If concentration cannot be avoided, thermal exposure and accumulation must be controlled by reducing CF and introducing **early solvent exchange** so that late-stage high-concentration risk windows are avoided.

### Upstream coupling requirement

Machine review of WRKUP-003 must include evaluation of extraction-solvent selection and, when necessary, upstream reaction-solvent choice.

Downstream workup safety constraints therefore feed back to earlier solvent-selection decisions.

---

## 2 Review Fields and Accounting Basis

All blocking and review decisions rely on the following audit fields.

During scheme review the system must verify:

- fields are completed  
- stated basis is reasonable  
- minimal sub-items are present  

---

## 2.1 Core Metric

### CF (Concentration Factor)

Definition

CF = Initial liquid-phase volume / Final liquid-phase volume

Purpose

CF acts as a shared dependency metric across several risk modes:

- nonvolatile accumulation  
- thermal exposure  
- acid/base enrichment  

CF thresholds used in this chapter (>3, >5, >10) represent **initial engineering guidelines** and may be tuned based on:

- product properties  
- company standards  
- acceptable loss or risk tolerance  

---

## 2.2 Core Field List

| Field | Definition | Mandatory Condition | Minimal Checkable Sub-Items | Review Focus |
|---|---|---|---|---|
| Volatile Removal Trajectory (VRT) | Order in which volatile components evaporate and whether azeotropy or co-distillation exists | Required for mixed-solvent or water-containing systems | volatility order; azeotrope/co-distillation declaration | confirm volatile components identified |
| Nonvolatile Inventory (NV) | Species that remain and accumulate during concentration | Required when NV species exist | NV list; accumulation/precipitation risk statement | confirm NV list completeness |
| Composition Evolution Path (CEP) | Trajectory describing solvent composition change during concentration | Required for mixed-solvent systems | ratio drift description; instability-zone warning; morphology-change point | detect phase-behavior change |
| Thermal Exposure (TE) | Temperature/time window experienced during concentration | Required for heated concentration | Tmax; heating window; degradation-study statement | confirm scale-relevant study |
| Operational Constraints (OC) | Equipment limits affecting concentration | Required for scale-up | minimum stirrable volume; dryness policy; transfer plan; wet-product solvent target | verify equipment feasibility |

---

## 3 Risk Modes and Blocking Rules

Only two blocking levels are used:

Soft Block  
Hard Block

Missing or null fields automatically trigger review.

---

## 3.1 Nonvolatile Accumulation Mode

Mechanism

Nonvolatile species accumulate as solvent is removed.

Approximate multiplier:

Accumulation ≈ CF

Possible consequences:

- salt precipitation  
- acid/base shift  
- viscosity increase  
- secondary reactions  

Control strategy

- remove NV upstream via aqueous washing  
- introduce early solvent exchange when necessary  

Trigger conditions

| Condition | Block Level |
|---|---|
NV exists and CF > 3 but NV accumulation risk not declared | Soft Block |
acid/base sensitive system + CF > 5 + heating to complete dryness | Hard Block |

---

## 3.2 Composition-Trajectory Instability

Mechanism

During concentration lower-boiling components leave first, causing solvent composition drift.

Crossing instability zones may trigger:

- oiling out  
- salt-out  
- crystallization  
- phase inversion  

Control strategy

1 identify instability regions experimentally  
2 design trajectory using solvent selection and solvent exchange  

Trigger conditions

| Condition | Block |
|---|---|
CEP missing | Soft Block |
VRT volatility order missing | Soft Block |

---

## 3.3 Thermal Exposure Mode

Scale-up commonly introduces

- higher temperature  
- longer duration  
- higher concentration  

Control strategy

- perform thermal degradation study  
- reduce CF  
- introduce early solvent exchange  

Trigger conditions

| Condition | Block |
|---|---|
TE degradation study missing | Soft Block |
study does not cover scale-up conditions | Soft Block |
known instability ignored | Hard Block |

---

## 3.4 Equipment and Transfer Boundary Mode

Lab scale may allow drying to completion.

Scale-up is constrained by:

- minimum stirrable volume  
- discharge path  
- solid transfer  
- wet product solvent effects  

Trigger conditions

| Condition | Block |
|---|---|
OC missing | Soft Block |
final volume below minimum stirrable volume with dryness planned | Hard Block |
solid residue without transfer plan | Hard Block |

---

## 3.5 Cross-Mode Safety Gate

Explosion hazard assessment must exist before concentration.

| Condition | Block |
|---|---|
no safety assessment | Hard Block |

---

## 4 Design Routes (Priority Order)

Machine review sequence

Route 1 > Route 2 > Route 3

### Route 1 — Product Disengagement

Evaluate whether the product can leave the system early.

### Route 2 — Concentration Reduction

Guideline

CF ≤ 5  
CF > 10 → Hard Block

Override allowed only with explicit audit trace.

### Route 3 — Concentration + Solvent Exchange

Principles

- avoid complete dryness  
- add next-step solvent early  
- induce precipitation if beneficial  

---

## 5 Audit Trace

#Audit: WRKUP-003
- CF:
- NV_complete:
- VRT_complete:
- CEP_complete:
- TE_complete:
- OC_complete:
- selected_route:
- hard_block_triggered:
- soft_block_triggered:
- override(if_any):

---

## 6 Vocabulary Evolution

| Concept | Definition |
|---|---|
concentration control authority | system control through solvent removal |
nonvolatile accumulation | NV enrichment during concentration |
composition evolution path | solvent-composition trajectory |
thermal exposure | temperature/time trajectory |
minimum stirrable volume | agitation threshold in scale-up |

---

## 7. Machine Annotation

```yaml
schema_version: "risk_annotation_schema_v0.2"
annotation_scope: "chapter_level"
canonical_id: "WRKUP-003-SOLVENT-REMOVAL-DRIVEN-ACCUMULATION-AND-THERMAL-EXPOSURE-CONTROL"
process_stage: "workup_concentration_solvent_exchange"

transition_model: "liquid_phase_workup_to_forced_composition_path_under_solvent_removal"

control_window: >
  Concentration and solvent exchange still occur in the liquid-phase domain, but solvent removal forces the system along an increasingly constrained composition path. Control authority is mainly exercised by avoiding concentration, reducing CF, selecting the extraction or reaction solvent appropriately, and introducing early solvent exchange before late-stage high-concentration risk windows form.

core_judgment: >
  The central machine-review task is to detect whether a proposed workup treats concentration as neutral solvent evaporation instead of an irreversible accumulation trajectory that may amplify nonvolatile inventory, thermal exposure, phase-behavior drift, and equipment or transfer-boundary constraints.

review_gates:
  hard_gate:
    - "CF > 10 without explicit audit override"
    - "acid/base sensitive system + CF > 5 + heating to complete dryness"
    - "known thermal or concentration instability ignored"
    - "final volume below minimum stirrable volume while dryness is planned"
    - "solid residue expected without transfer plan"
    - "no explosion hazard assessment before concentration"
  soft_gate:
    - "NV exists and CF > 3 but NV accumulation risk is not declared"
    - "CEP missing for a mixed-solvent system"
    - "VRT volatility order missing"
    - "TE degradation study missing for heated concentration"
    - "thermal study does not cover scale-up temperature, time, or concentration conditions"
    - "OC missing for scale-up concentration"

route_priority:
  - "Route 1: product disengagement before concentration"
  - "Route 2: concentration reduction, preferably CF <= 5"
  - "Route 3: concentration plus early solvent exchange, avoiding complete dryness when possible"

risk_signals:
  - "CF > 3 with nonvolatile inventory present and undeclared"
  - "CF > 5 in acid/base sensitive system with heating to complete dryness"
  - "CF > 10 without explicit override"
  - "nonvolatile salts, acids, bases, high-boiling residues, or modifiers remain during concentration"
  - "mixed-solvent system without VRT volatility order"
  - "mixed-solvent system without CEP composition-drift assessment"
  - "lower-boiling solvent removal may cross instability zone"
  - "oiling out during concentration"
  - "salt-out during concentration"
  - "unexpected crystallization during concentration"
  - "phase inversion during concentration"
  - "heated concentration without scale-relevant degradation study"
  - "thermal study does not cover higher temperature, longer duration, and higher concentration expected on scale-up"
  - "planned complete dryness"
  - "final volume below minimum stirrable volume"
  - "solid residue without transfer plan"
  - "wet-product solvent target not defined"
  - "explosion hazard assessment missing before concentration"

reasoning_anchors:
  - "control_authority_decay"
  - "misallocated_control_authority"
  - "forced_composition_path"
  - "nonvolatile_accumulation"
  - "composition_evolution_path"
  - "volatile_removal_trajectory"
  - "thermal_exposure_accumulation"
  - "early_solvent_exchange"
  - "equipment_transfer_boundary"
  - "upstream_solvent_selection_coupling"
  - "route_priority_review"

expert_judgment:
  - "Solvent removal should be reviewed as a forced composition trajectory, not as a neutral housekeeping operation."
  - "If nonvolatile inventory remains during concentration, its effective local level may scale approximately with CF and may create precipitation, acid/base shift, viscosity increase, or secondary reaction risk."
  - "If lower-boiling components leave first, solvent ratio drift may rewrite phase behavior even when the initial mixture appears acceptable."
  - "If thermal exposure data do not cover scale-up Tmax, duration, and concentration, small-scale stability evidence should not be treated as sufficient."
  - "If complete dryness is planned, review must distinguish laboratory convenience from scale-up feasibility, especially minimum stirrable volume, discharge path, and solid transfer."
  - "If concentration risk is high, the preferred review direction is upstream redesign, product disengagement, or CF reduction before accepting concentration plus solvent exchange."

uncertainty_and_exceptions:
  - "CF thresholds are initial engineering guidelines and may be tuned by product properties, company standards, and acceptable risk tolerance."
  - "Missing fields trigger review rather than automatic process rejection unless a defined hard-gate condition is met."
  - "Early precipitation during solvent exchange may be beneficial if intentionally designed, experimentally understood, and compatible with downstream handling."
  - "CF > 10 may be overridden only with explicit audit trace and a justified risk-control basis."
  - "The annotation should not infer degradation, oiling out, or phase inversion unless supported by observed data, known instability, or missing required review fields."

quantitative_triggers:
  cf_nv_soft_review: "NV exists and CF > 3 with undeclared accumulation risk"
  cf_acid_base_dryness_hard_block: "acid/base sensitive system + CF > 5 + heating to complete dryness"
  cf_hard_block: "CF > 10 unless explicit audit override"
  preferred_cf_target: "CF <= 5"
  thermal_study_required_when: "heated concentration"
  explosion_assessment_required_when: "before concentration"

required_review_fields:
  - "CF"
  - "VRT"
  - "NV"
  - "CEP"
  - "TE"
  - "OC"
  - "explosion_hazard_assessment"
  - "selected_route"
  - "override_trace_if_any"

machine_use: >
  Review whether a proposed concentration or solvent-exchange design has avoided unnecessary concentration, justified CF, declared nonvolatile inventory, mapped volatile-removal and composition-evolution trajectories, covered scale-relevant thermal exposure, and checked equipment or transfer-boundary constraints before accepting the workup route.