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