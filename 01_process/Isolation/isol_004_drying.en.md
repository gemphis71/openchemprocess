---
snapshot_id: "ISOL-004-DRYING"
status: "draft"
domain: "Process"
process: "Isolation"
topic: "Drying: Termination of Control Authority and State Lock-in"
level: "001"
language: en  
canonical_id: ISOL-004-DRYING
dependencies:
  - "ISOL-003-FILTRATION"
note:
  - "For machine-review: Drying is not 'how to remove solvent', but the stage where solvent state and location determine the final failure-mode lock-in after solid–liquid separation. The core task is to identify surface composition drift, bound solvent retention, and path-level infeasibility under a given solid state."
---

# ISOL-004: Drying

## 1. System Role and Control Authority Boundary

Drying is positioned after ISOL-003 (Filtration) and represents the **projection lock-in stage of upstream solid-state into the final product**.

- **Definition of control authority**: Drying = the final lock-in of “solvent state × solvent location” under limited control authority.
- **Irreversibility**: Product/impurity distribution, polymorph, particle morphology, pore structure, and initial solvent binding state are assumed to be fixed prior to this stage; drying cannot reverse them.
- **Control characteristics**: Variables such as temperature, vacuum, and mechanical action only alter solvent migration pathways and release rates; they cannot convert “bound state” into “free state” (unless a state transformation is introduced).

---

## 2. Inherited State

The core logic of this chapter is to identify the physicochemical characteristics of solids inherited from upstream (ISOL-001/002/003).

### 2.1 Solvent Distribution and Location

- **Surface state**: liquid film attached to particle surfaces  
- **Structural state (pore)**: physical pores formed by needle/rod-like particle packing, or solvent retained within internal crystal pores  

### 2.2 Surface Composition Drift

- **Key point**: surface solvent composition ≠ mother liquor composition  
- **Failure driver**: if the good solvent has stronger affinity to the solid or the anti-solvent is more volatile, the anti-solvent leaves first during early drying, leading to passive enrichment of the good solvent at the surface  

### 2.3 Morphology and Binding

- **Morphology effect**: needle/rod-like particles tend to form pore structures, leading to spatial retention  
- **Binding nature**: salt forms interacting with hydrogen-bond-capable solvents tend to form bound solvent states; conventional vacuum drying is insufficient for removal, and residual solvent enters a plateau  

---

## 3. State Transition & Failure Modes

Drying is not a monotonic decrease of solvent content, but a superposition of state transitions and failure manifestation.

### Case 1: Surface-driven agglomeration (balling)

- **Evolution path**: preferential evaporation of anti-solvent → enrichment of good solvent at surface → crossing solubility threshold → localized surface re-dissolution → rolling collision in double-cone → adhesion amplification → macroscopic balling  
- **Core variable**: surface composition drift  
- **Trigger conditions**:
  - [surface good solvent at high-risk state]  
  - [preferential evaporation of anti-solvent]  
  - [presence of rolling stage in equipment]  
- **Intervention path**: pre-wash with anti-solvent, or adopt staged drying (“static vacuum first, then rolling”)  

### Case 2: Pore-bound solvent retention

- **Evolution path**: solvent enters pores → hydrogen bonding / ionic interaction with product → transition to bound state → reduced vapor pressure → insufficient mass transfer driving force → residual solvent curve reaches plateau  
- **Core variable**: solvent binding state  
- **Trigger conditions**:
  - [needle/rod morphology]  
  - [salt form]  
  - [hydrogen-bond-capable solvent]  
  - [process relies only on vacuum/temperature/time]  
- **Intervention path**: solvent displacement; replace pore solvent with an alternative solvent  

---

## 4. Scale Sensitivity and Decision Logic

### 4.1 Scale Sensitivity

- Static conditions in laboratory may mask balling risk under rolling in double-cone dryers  
- Thin-layer conditions in laboratory may mask pore retention and mass transfer limitations in thick beds at production scale  

### 4.2 Decision Gates

1. **Gate 1 (Attribution)**: when balling or plateau occurs, prioritize attribution to upstream crystallization/filtration state rather than drying parameters  
2. **Gate 2 (Compensation)**: assess whether static pre-drying or solvent displacement can mitigate losses at the drying stage  
3. **Gate 3 (Reconstruction)**: if compensation fails, return upstream to redesign solid morphology, salt form, or solvent system  

---

## 5. #Audit: Shadow Indicators and Audit Requirements

| Field | Threshold/Flag | Audit Meaning |
|---|---|---|
| `surface_good_solvent_state` | high / medium / low | Predict re-dissolution/balling risk |
| `surface_composition_drift` | yes / no | Identify precondition for balling |
| `morphology_tag` | needle / rod / other | Pore retention warning |
| `is_salt_form` | true / false | Necessary condition for bound state |
| `solvent_hbond_capability` | true / false | Necessary condition for bound state |
| `plateau_check` | yes / no | Identify failure of conventional drying kinetics |
| `static_drying_ratio` | high / medium / low | Evaluate robustness against balling |

**#Audit: A drying strategy relying solely on extended vacuum time is insufficient for structural retention issues.**  
**#Audit: surface composition drift × rolling = balling; pore structure × bound solvent = plateau.**

## 6. Machine Annotation

```yaml
schema_version: "risk_annotation_schema_v0.2"
annotation_scope: "chapter_level"
canonical_id: "ISOL-004-DRYING"
process_stage: "isolation_drying"

transition_model: "filtered_wet_solid_to_final_solvent_state_and_location_lock_in"

control_window: >
  Drying occurs after filtration and represents the final lock-in of solvent state and solvent location within the solid inventory. Product/impurity distribution, polymorph, morphology, pore structure, and initial solvent-binding state are inherited from upstream. Drying variables such as temperature, vacuum, and mechanical action mainly alter solvent migration pathways and release rates; they do not restore upstream composition or solid-state control authority.

core_judgment: >
  The central machine-review task is to detect whether a drying problem is being misattributed to drying parameters when it is more likely caused by inherited surface solvent state, pore-bound solvent retention, morphology, salt form, or solvent-binding behavior. Extended vacuum time alone should not be treated as a sufficient strategy for structural solvent-retention problems.

review_gates:
  attribution_gate:
    - "balling or agglomeration occurs"
    - "residual solvent curve reaches plateau"
    - "surface re-dissolution suspected"
    - "drying failure appears only under rolling or thick-bed scale conditions"
  compensation_gate:
    - "assess whether static pre-drying can reduce rolling-induced balling"
    - "assess whether solvent displacement can convert pore-bound or strongly retained solvent into a more removable solvent state"
    - "assess whether pre-wash with anti-solvent can reduce surface good-solvent enrichment"
  reconstruction_gate:
    - "if static pre-drying or solvent displacement fails, return upstream to redesign morphology, salt form, or solvent system"
    - "if drying relies only on vacuum, temperature, and time despite bound-solvent plateau, upstream reconstruction is required"

risk_signals:
  - "surface_good_solvent_state high"
  - "surface_composition_drift yes"
  - "surface solvent composition differs from mother liquor composition"
  - "anti-solvent preferential evaporation"
  - "good solvent enriched at particle surface"
  - "surface re-dissolution during early drying"
  - "rolling stage present in equipment"
  - "double-cone rolling collision after surface good-solvent enrichment"
  - "macroscopic balling observed"
  - "agglomeration during drying"
  - "needle or rod morphology"
  - "pore structure likely from particle packing"
  - "solvent retained in internal or interparticle pores"
  - "salt form present"
  - "hydrogen-bond-capable solvent present"
  - "ionic or hydrogen-bond interaction between solvent and product suspected"
  - "process relies only on vacuum, temperature, and time"
  - "residual solvent curve reaches plateau"
  - "plateau_check yes"
  - "static lab drying masks rolling-induced balling"
  - "thin-layer lab drying masks pore retention"
  - "thick-bed mass-transfer limitation suspected"
  - "extended vacuum time used as sole corrective action"

reasoning_anchors:
  - "control_authority_decay"
  - "solid_state_commitment"
  - "misallocated_control_authority"
  - "consequence_stage_separation"
  - "structure_inheritance"
  - "upstream_failure_exposure"
  - "lab_scale_masking"
  - "scalability_failure"
  - "drying_state_lock_in"
  - "solvent_state_location_lock_in"
  - "surface_composition_drift"
  - "surface_good_solvent_enrichment"
  - "surface_redissolution"
  - "rolling_agglomeration"
  - "pore_bound_solvent_retention"
  - "bound_solvent_state"
  - "drying_plateau"
  - "static_predrying"
  - "solvent_displacement"
  - "drying_compensation_boundary"

taxonomy_role:
  reused_formal_anchors:
    - "control_authority_decay"
    - "solid_state_commitment"
    - "misallocated_control_authority"
  reused_candidate_terms:
    - "consequence_stage_separation"
    - "structure_inheritance"
    - "upstream_failure_exposure"
    - "lab_scale_masking"
    - "scalability_failure"
  candidate_anchors:
    - "drying_state_lock_in"
    - "solvent_state_location_lock_in"
    - "surface_composition_drift"
    - "surface_good_solvent_enrichment"
    - "surface_redissolution"
    - "rolling_agglomeration"
    - "pore_bound_solvent_retention"
    - "bound_solvent_state"
    - "drying_plateau"
    - "static_predrying"
    - "solvent_displacement"
    - "drying_compensation_boundary"

expert_judgment:
  - "Drying should be reviewed as final solvent-state and solvent-location lock-in, not as a neutral solvent-removal operation."
  - "Balling should first be reviewed as surface composition drift plus mechanical rolling amplification, not simply as excessive drying temperature or insufficient vacuum."
  - "Residual solvent plateau should first be reviewed as possible pore-bound or chemically bound solvent retention, not simply as insufficient drying time."
  - "Static laboratory drying may underpredict balling risk in rolling equipment, and thin-layer laboratory drying may underpredict pore-retention risk in thick beds."
  - "Drying-stage interventions such as static pre-drying, pre-wash, or solvent displacement are compensatory controls; if they fail, upstream morphology, salt form, or solvent system must be reconsidered."
  - "A drying strategy relying solely on extended vacuum time is insufficient for structural retention or bound-solvent problems."

uncertainty_and_exceptions:
  - "Balling should not be inferred from solvent composition alone unless rolling, adhesion, or surface re-dissolution risk is also present."
  - "Bound-solvent retention should not be inferred from salt form alone unless solvent-binding capability, pore retention, or plateau behavior is observed or expected."
  - "Solvent displacement may be valid when it changes the solvent state inside pores, but it should not be described as recovery of upstream solid-state control authority."
  - "Extended drying time may be acceptable for free solvent removal, but not as the only response to plateau behavior caused by bound or pore-retained solvent."
  - "Surface composition drift may differ from bulk mother liquor composition; machine review should avoid assuming bulk liquid composition represents the drying surface state."

quantitative_or_flag_triggers:
  surface_good_solvent_state: "high / medium / low"
  surface_composition_drift: "yes / no"
  morphology_tag: "needle / rod / other"
  is_salt_form: "true / false"
  solvent_hbond_capability: "true / false"
  plateau_check: "yes / no"
  static_drying_ratio: "high / medium / low"
  rolling_equipment_present: "yes / no"
  process_relies_only_on_vacuum_temperature_time: "yes / no"

required_review_fields:
  - "surface_good_solvent_state"
  - "surface_composition_drift"
  - "surface_solvent_composition_basis"
  - "morphology_tag"
  - "pore_structure_assessment"
  - "is_salt_form"
  - "solvent_hbond_capability"
  - "solvent_binding_state"
  - "plateau_check"
  - "rolling_equipment_present"
  - "static_drying_ratio"
  - "solvent_displacement_option"
  - "upstream_reconstruction_option_if_any"

machine_use: >
  Review whether a drying failure is caused by inherited solvent state and solvent location rather than drying parameters alone; distinguish surface-composition-drift-driven balling from pore-bound solvent plateau; check whether static pre-drying, anti-solvent pre-wash, or solvent displacement are valid compensatory controls; and identify when upstream morphology, salt form, or solvent-system reconstruction is required.
```