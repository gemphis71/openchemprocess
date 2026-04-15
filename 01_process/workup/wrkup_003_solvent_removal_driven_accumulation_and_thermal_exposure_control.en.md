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