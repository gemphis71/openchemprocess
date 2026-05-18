snapshot_id: "THR-001-THERMAL-CONTROL-AUTHORITY"
status: "draft"
domain: "Process"
process: "Thermal"
topic: "Thermal control as a risk structure governing reaction pathway and stage accessibility"
level: "001"
language: en  
canonical_id: THR-001-THERMAL-CONTROL-AUTHORITY
note:  This document aims to identify, under scale-up conditions, whether temperature
  escalates from a rate-modulating parameter to a primary source of control authority.
  It does not address heat-transfer engineering or temperature-control hardware.
  The focus is exclusively on how temperature determines reaction logic,
  including pathway dominance and stage accessibility.
dependencies:
  - "CHG-001-CHARGING-SEQUENCE"
  - "CHG-002-ADDITION-MODE-AND-RATE"
  - "MIX-001-MIXING-TIME-SCALE-FAILURE"
---
## 1. Positioning

Under the prerequisite that charging sequence (CHG-001),  addition mode and nominal rate (CHG-002),  and mixing logic (MIX-001) are structurally sound,

**temperature becomes the primary source of control authority in a limited class of reaction systems.**

In such systems:

- temperature is no longer merely a parameter controlling reaction “speed”;
    
- temperature selection directly determines:
    
    - which reaction pathway becomes dominant; or
        
    - whether the reaction can cross a stage or intermediate boundary;
        
- once the temperature strategy is incorrect,  
    upstream CHG / MIX control measures cannot provide equivalent recovery.
    

---

## 2. Core Distinction

### A | Parallel Reaction Pathway Allocation

**Thermal as Competing Pathway Authority**

The reaction system contains two or more accessible reaction pathways.  
Temperature allocates pathway dominance by altering their relative intrinsic rates.

**Diagnostic characteristics:**

- changing temperature alters product composition or selectivity;
    
- extending time or adjusting addition rate is ineffective;
    
- control authority cannot be transferred to the CHG / MIX layers.
    

---

### B | Reaction Stage Accessibility

**Thermal as Stage-Gating Authority**

The reaction proceeds via intermediates or multiple stages.  
Temperature determines whether—and when—the system can enter the next stage.

**Diagnostic characteristics:**

- reaction stagnation or intermediate accumulation within a specific temperature window;
    
- reaction recovery or stage transition upon heating;
    
- temperature defines stage boundaries, rather than merely modulating rate.
    

---

## 3. Type A Cases | Parallel Pathway Allocation

---

### Case A1 | Pathway Ratio Shift in Selective Acylation of Diols (DLL)

#### System Conditions

- Substrate: diol containing both primary and secondary alcohols
    
- Reaction: acylation with pivaloyl chloride
    
- Intrinsic rate ratio: ~1:20 (secondary : primary)
    

#### Logic Conflict

Low temperature is commonly employed to “improve selectivity”;  
however, in this system, selectivity does not improve monotonically with decreasing temperature.

#### Observed Behavior

- At low temperature (~0 °C):
    
    - the primary-alcohol pathway dominates;
        
    - the secondary-alcohol pathway is suppressed;
        
    - selectivity remains stable within the target conversion window.
        
- Upon heating:
    
    - the contribution of the secondary-alcohol pathway continuously increases;
        
    - selectivity collapses as the reaction proceeds.
        

#### Decision Trace

**Hypothesis Space**

- H1: selectivity change is solely caused by overall rate variation
    
- H2: temperature alters the relative rates of two competing pathways
    
- H3: selectivity collapse originates from late-stage substrate ratio changes
    

**Elimination Path**

- product ratio differences appear at low conversion under different temperatures → exclude H1
    
- substrate ratio changes cannot explain early-stage divergence → constrain H3
    

**Decision Pivot**  
Temperature reallocates pathway dominance by modifying the relative rates of competing alcohol sites.  
Pathway authority is determined exclusively by temperature;  
CHG / MIX adjustments cannot provide equivalent substitution.

#### Explicit Labels

- Case_Type: Core
    
- Authority_Level: Primary
    
- Control_Mode: Competing_Pathway
    
- Substitutable_By: None
    

---

### Case A2 | Loss of Catalytic Pathway Authority in CBS Asymmetric Reduction

#### System Conditions

- Parallel pathways:
    
    - CBS catalytic cycle (high ee)
        
    - direct borane reduction (racemic)
        

#### Logic Conflict

The conventional strategy of “lower temperature for higher selectivity” is reversed in this system.

#### Observed Behavior

- Upon cooling:
    
    - overall reaction rate decreases;
        
    - ee continuously declines;
        
    - extending time or increasing catalyst loading is ineffective.
        
- Upon heating:
    
    - the catalytic pathway regains dominance;
        
    - ee recovers and stabilizes.
        

#### Decision Trace

**Hypothesis Space**

- H1: ee loss is due to incomplete reaction
    
- H2: ee loss is due to pathway contribution shift
    
- H3: ee variation originates from post-reaction handling or time effects
    

**Elimination Path**

- time extension / catalyst loading increase ineffective → exclude H1
    
- ee divergence appears at early stages → exclude H3
    

**Decision Pivot**  
Cooling preferentially suppresses the CBS catalytic cycle,  
allowing the non-selective pathway to dominate.  
Control authority resides at the thermal layer  
and cannot be transferred to CHG / MIX.

#### Explicit Labels

- Case_Type: Core
    
- Authority_Level: Primary
    
- Control_Mode: Competing_Pathway
    
- Substitutable_By: None
    

---

## 4. Type B Cases | Stage Accessibility (Intermediate-Involving)

---

### Case B1 | Stage Deadlock Caused by a Stable Intermediate

#### System Conditions

- Pathway: S → I → P
    
- I is stable; I → P requires higher temperature
    

#### Logic Conflict

The reaction can initiate at low temperature but cannot complete.

#### Observed Behavior

- At low temperature:
    
    - state: I-Accumulated;
        
    - S consumption stops;
        
    - reaction stagnates.
        
- Upon heating:
    
    - I → P conversion is enabled;
        
    - reaction progression resumes.
        

#### Decision Pivot

Temperature determines stage accessibility.  
If I → P is disabled, the reaction is structurally blocked at the stage boundary.

#### Explicit Labels

- Case_Type: Core
    
- Authority_Level: Primary
    
- Control_Mode: Stage_Gate
    
- Substitutable_By: None
    

---

### Case B2 | Stable Intermediate with Thermally Unstable Product

#### System Conditions

- I is stable
    
- P degrades at elevated temperature
    

#### Logic Conflict

Constant high temperature simultaneously promotes formation and degradation.

#### Observed Behavior

- Constant high temperature: rapid degradation of P
    
- Staged temperature profile:
    
    - low temperature completes S → I;
        
    - short-term heating completes I → P;
        
    - high-temperature residence time of P is minimized.
        

#### Decision Pivot

Temperature is used to decouple stages and manage residence time,  
rather than to simply accelerate the reaction.

#### Explicit Labels

- Case_Type: Core
    
- Authority_Level: Primary
    
- Control_Mode: Stage_Gate
    
- Substitutable_By: None
    

---

### Case B3 | Mismatch Between Formation and Consumption of an Unstable Intermediate (Boundary Case)

#### System Conditions

- heating accelerates S → I;
    
- I → P is relatively slow;
    
- I is unstable.
    

#### Logic Conflict

Heating simultaneously amplifies risk and provides a potential corrective lever.

#### Observed Behavior

- heating alone: accumulation of I and amplification of side reactions;
    
- two viable corrective routes:
    
    - limiting formation flux (CHG);
        
    - further heating to accelerate I → P.
        

#### Decision Pivot

Thermal and charging constitute **substitutable control authority layers**.  
Temperature is no longer the sole source of control authority.

#### Explicit Labels

- Case_Type: Boundary
    
- Authority_Level: Shared
    
- Control_Mode: Stage_Gate
    
- Substitutable_By: CHG
    

---

## 5. Usage Notes

- If thermal anomalies manifest only after charging is complete,  
    and control authority has already been lost due to inventory accumulation,  
    the risk should be attributed to the CHG layer rather than THR.
    
- Thermal runaway triggered by mixing time-scale failure represents a thermal manifestation,  
    not thermal control authority (see MIX-001).
    
- Case B3 is a cross-layer boundary case and should not be treated as a core THR archetype.
    

---

## #Audit

This document characterizes risk structures in which temperature serves as the **primary source of control authority**.  
The diagnostic criterion is:

> Whether pathway or stage dominance can be determined **only** by temperature selection  
> and cannot be equivalently recovered by CHG or MIX interventions.


---

## Machine Annotation

```yaml
schema_version: "risk_annotation_schema_v0.2"
annotation_scope: "chapter_level"
canonical_id: "THR-001-THERMAL-CONTROL-AUTHORITY"
process_stage: "thermal_control_authority"
transition_model: "temperature_as_rate_parameter_to_primary_control_authority"

control_window: >
  THR-001 applies only after charging sequence, addition logic, and mixing logic are structurally sound. Within this limited class of systems, temperature becomes the primary source of control authority because it determines competing pathway dominance or stage accessibility.

core_judgment: >
  Temperature should be treated as primary control authority only when reaction pathway or stage dominance is determined by temperature selection and cannot be equivalently recovered by CHG or MIX interventions. Thermal anomalies caused by prior charging inventory accumulation or mixing time-scale failure should be reviewed as CHG or MIX manifestations, not as THR-001 positive cases.

risk_signals:
  - "temperature change alters product composition or selectivity"
  - "temperature change alters dominance between competing reaction pathways"
  - "extending time does not recover selectivity or pathway dominance"
  - "adjusting addition rate does not recover selectivity or pathway dominance"
  - "reaction stagnates or intermediate accumulates within a specific temperature window"
  - "heating enables stage transition or reaction recovery"
  - "temperature defines stage boundary rather than merely modulating rate"
  - "cooling suppresses the desired catalytic or selective pathway"
  - "constant high temperature promotes both desired formation and product degradation"
  - "thermal and charging controls are substitutable in a boundary case"

expert_judgment:
  - "If CHG and MIX controls are structurally valid and temperature alone determines pathway or stage accessibility, THR-001 is the primary review-domain snapshot."
  - "If a thermal anomaly only appears after charging inventory has accumulated, the primary attribution should remain CHG rather than THR."
  - "If thermal runaway is triggered by mixing time-scale failure, the thermal signal is a manifestation rather than thermal control authority."
  - "If charging and thermal controls can substitute for each other, the case should be treated as a boundary case rather than a core THR-001 archetype."

reasoning_anchors:
  - "control_authority_decay"
  - "misallocated_control_authority"
  - "thermal_control_authority"
  - "temperature_as_primary_authority"
  - "competing_pathway_authority"
  - "stage_gating_authority"
  - "substitutable_control_authority"

uncertainty: "medium"

exceptions:
  - "Temperature-dependent rate change alone is not sufficient to establish THR-001."
  - "Thermal instability caused by prior inventory accumulation should remain attributed to the charging layer unless pathway or stage authority is temperature-primary."
  - "Thermal consequences of MIX-001 logical lock-in should not be reclassified as THR-001."
  - "Boundary cases with substitutable CHG and THR controls should remain explicitly marked as shared-authority cases."

machine_use: >
  Use this annotation to review whether temperature is the primary source of reaction-pathway or stage-accessibility control. Keep the output in attribution and evidence-sufficiency language. Do not provide temperature programs, heating/cooling instructions, operating windows, or thermal troubleshooting recommendations.