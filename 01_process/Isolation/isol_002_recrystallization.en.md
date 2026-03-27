---  
snapshot_id: "ISOL-002-RECRYSTALLIZATION"  
status: "draft"  
domain: "Process"  
process: "Isolation"  
topic: "Recrystallization: Selective Re-partitioning and Solid-State Reconstruction (Selective Re-partitioning under Constrained Solubility Space)"  
level: "002"  
dependencies:  
- "ISOL-001-CRYSTALLIZATION"  
- "WRKUP-003-SOLVENT-REMOVAL-DRIVEN-ACCUMULATION-AND-THERMAL-EXPOSURE-CONTROL"  
- "WRKUP-002-PARTITION-RATIO-DRIFT-INVENTORY-CONTROL"  
- "THR-001-THERMAL-CONTROL-AUTHORITY"  
note:  
- "For machine review: define the control boundary and failure signals of recrystallization using Selectivity, Recovery, and the solubility path (ΔSolubility)."  
- "This chapter corresponds to a brief window of control regain: solid → solution → solid, but control authority is limited and cannot be fully restored."  
---
# ISOL-002: Recrystallization


## 1. System Role

> control regain

Recrystallization is not a repetition of crystallization, but a **selective reconstruction process occurring at the solid–liquid partition boundary**.

solid → solution → solid

The system temporarily returns to the solution state, regains limited partition control capability, and redefines component allocation upon re-entering the solid phase.

Recrystallization = selective re-partitioning under constrained solubility space

---

### Control Essence

Recrystallization is a control problem, not a precipitation problem.

---

### Operational Objective Clarification (Pre-design Requirement)

Recrystallization may serve different purposes. The objective must be clearly defined before design:

- **Impurity removal–focused**: improve purity via selective impurity partitioning
- **Polymorph transformation–focused**: change crystal form/salt form without significantly altering purity
- **Hybrid objective**: impurity removal + polymorph transformation

> This chapter focuses on impurity-removal-driven recrystallization, but the selectivity framework applies equally to polymorph transformation or hybrid objectives.

---

## 2. Design Objective

> control definition

This chapter defines the control objectives and evaluation system of recrystallization.  
All subsequent modules (Selectivity Landscape, Solubility Envelope, Kinetic Stability, Downstream Interface) are built around these objectives.

---

### 2.1 Objective Function

maximize impurity rejection  
subject to recovery constraint

---

### 2.2 Recovery

**Definition:**  
Recovery = 1 − (S_final / S_initial)

- S_initial = mass of target compound in solution before crystallization
- S_final = mass of target compound remaining in mother liquor after crystallization

|Range|Status|Action|
|---|---|---|
|≥85%|Ideal|Design target|
|80–85%|Acceptable|Acceptable|
|<80%|Hard Warning|Must justify (unless compensated)|
|<70%|Unacceptable|Redesign required unless strongly justified|

#### Common Engineering Factors Affecting Recovery

- High-boiling solvent residue (DMF, DMSO >5%)
- Co-solvent retention
- Incomplete salt form conversion
- Excessively small crystal size leading to dissolution loss

---

### 2.3 Impurity Rejection

**Definition:**  
Rejection = 1 − (C_solid / C_feed)

- C_solid = impurity concentration in solid after crystallization (mass fraction)
- C_feed = impurity concentration in solution before crystallization (mass fraction)

|Rejection|Evaluation|
|---|---|
|≥90%|Can serve as primary impurity control step|
|80%-90%|Feasible but suboptimal; requires upstream support or multiple crystallizations|
|<80%|Should not be used as main control step|

---

### 2.4 Evaluation Window (Data Validity)

**Key Principle:** Rejection must be measured within  
**Recovery ∈ [40%, 85%]** to be considered reliable.

|Recovery Range|Bias|
|---|---|
|<40%|Rejection may be overestimated|
|>85%|Rejection may be underestimated|

---

## 3. Selectivity Landscape

> control allocation
>Gate Type: Hard Gate

Entry condition: before detailed design, determine the role of this step in the process.

---

### 3.1 Feasibility Assessment

Does there exist a system where:  
**key impurity rejection ≥90%** AND **recovery ≥80%**?

|Result|Condition|Process Role|Strategy|
|---|---|---|---|
|**Optimal Use**|Satisfied|Primary impurity control step|Single or few crystallizations; high recovery maintained|
|**Compensatory Use**|Not satisfied|Auxiliary step|Multiple crystallizations + mother liquor recycle; recovery decreases|

#### Failure Signal (Compensatory Use Warning)

- ≥2 crystallizations required to reach purity target
- Repeated mother liquor recycle with unstable purity
- Recovery consistently <70%

---

### 3.2 Strategy for Low Rejection (<70%)

If major impurity rejection <70%,  
**priority should be given to controlling the impurity in other process steps**, rather than inefficient recrystallization.

Possible approaches:

- Adjust reaction conditions (change impurity profile)
- Optimize extraction/washing (exploit partition differences)
- Delay impurity removal to downstream steps with higher rejection

Avoid recrystallization at low rejection (<70%) unless unavoidable.

---

### 3.3 Impurity Load Matching Principle

Rejection requirement ≠ fixed threshold, but **f(impurity loading)**

|Impurity Type|Rejection Requirement|Strategy|
|---|---|---|
|**Major impurity** (high loading)|≥85%|Must be primarily removed at this step|
|**Minor impurity** (low loading)|70–85% or lower acceptable | May deprioritize|

#### Failure Signal

- Minor impurities removed well but overall purity still fails  
    → major impurity not controlled
- Major impurity rejection <85% without upstream compensation  
    → process design flaw

---

### 3.4 Process Implication (Hard Rule)

Insufficient selectivity → trace back upstream, not optimize crystallization.

**Trigger:** major impurity rejection <80%  
→ must evaluate reaction pathway or crude quality

---

### Hard Principle

> Insufficient selectivity = misallocated control authority

---

## 4. Solubility Envelope

> control space

Defines how to construct the solubility space required for selectivity.

---

### 4.1 Single-Solvent Anchor

At least one solvent must be identified such that:  
**key impurity rejection ≥90%** (or satisfies matching principle)

- Solvent type (good/poor) is not important
- Removal capability is critical
- This solvent defines the primary selectivity direction

---

### 4.2 Multi-Impurity → Solvent Combination

Different impurities may require different solvents; combined to achieve overall control.

Design sequence:

1. Identify high-rejection solvent (anchor)
2. Construct good solvent / anti-solvent system
3. Calculate recovery based on solubility relationships

---

### 4.3 Anti-solvent Role Boundary

|Target|Effect of Anti-solvent|
|---|---|
|Rejection|Usually preserved, but may alter partition pathway in abnormal cases|
|Recovery|Strong impact (via solubility reduction)|

**Failure Signal:** after anti-solvent addition

- abnormal impurity distribution
- significant drop in rejection

→ indicates selectivity mechanism has changed; reassessment required

---

### 4.4 ΔSolubility Driving Paths

All crystallization driving forces are expressed as ΔSolubility.

|Path|Mechanism|Typical Operation|Failure Signal|
|---|---|---|---|
|**Temperature**|dissolve at high T → crystallize upon cooling|cooling crystallization|too fast cooling → crash crystallization|
|**Salt form**|free ↔ salt|pH adjustment, counterion addition|pH drift, assay >100% → mixed salt forms|
|**Solvent**|good → + anti-solvent|anti-solvent addition|local precipitation, fine crystals|
|**Polymorph**|amorphous ↔ polymorph|seeding, aging|solubility variation under same conditions, rejection fluctuation|

---

## 5. Kinetic Stability

> control stability
> Gate Type: Soft Gate

Ensures the crystallization process is stable and reproducible.

---

## 5.1 Supersaturation Control

**Core requirement:** avoid excessive instantaneous supersaturation (burst nucleation). Supersaturation must remain within a controlled envelope where
nucleation and growth are balanced; outside this envelope,
burst nucleation dominates.

|State | Observation | Action|
|---|---|---|
|Normal | balance between nucleation and growth| — |
|Crash | excessive fine crystals, difficult filtration | increase temperature → aging → particle size growth|

**Trigger:** rapid buildup of supersaturation → high risk

---

## 5.2 Seeding Control

**Operational rule:** nucleation must be controlled via seeding (seed loading ≥1%, recommended 1–5%), 

**Failure Signal:**

- delayed nucleation
- batch-to-batch recovery variation >5%

→ indicates polymorph instability or seed failure

---

## 5.3 Particle Size Effect

|Direction|Impact on Recovery|Impact on Rejection|
|---|---|---|
|Particle size ↑|slight increase|essentially unchanged|
|Particle size ↓|slight decrease|essentially unchanged|

**Diagnostic Rule:**

- Recovery changes + Rejection stable → particle size effect
- Recovery changes + Rejection changes → polymorph change

---

# 6. Downstream Interface

> control loss
> Gate Type: Soft Gate

This section ensures that crystallized solids can be handled in downstream operations (solid–liquid separation, drying) without introducing additional risks.

---

## 6.1 Solid–Liquid Separation and Mother Liquor Retention

**Metric:**  
Wet/Dry = wet cake mass / dry mass

|Range|Evaluation|
|---|---|
|<1.2|good, easy filtration|
|1.2–1.5|acceptable, monitor particle size|
|1.5–2.0|high risk, requires filtration/centrifugation optimization|
|>2.0|unacceptable, severe mother liquor retention|

**Failure Signal:**  
abnormal purity despite correct crystallization  
→ mother liquor entrainment

---

## 6.2 Linkage with Crystallization Parameters

- excessively small particle size → difficult filtration, increased wet/dry ratio
- polymorph instability → may affect cake structure
- crash crystallization → fine crystals blocking filter bed

---

# 7. #Audit (Shadow Metrics)

|Metric|Meaning|Trigger / Recording Point|
|---|---|---|
|`Selectivity_major`|rejection of major impurity|<80% triggers reassessment|
|`Recovery_loss_flag`|cumulative loss from multiple crystallizations|>15% record|
|`Rejection_variance`|batch-to-batch rejection variability|>10% requires investigation|
|`Solubility_ratio_shift`|change in solubility ratio|>2× record|
|`Wet_cake_ratio`|wet/dry ratio|>1.5 warning, >2.0 hard trigger|
|`Crash_flag`|occurrence of crash crystallization|record immediately|
|`Polymorph_drift`|polymorph drift|recovery variation >5% record|

---

## #Audit Summary

The real risk of recrystallization is not  
“crystallization failure”,

but

**“continuing crystallization under incorrect selectivity assumptions.”**