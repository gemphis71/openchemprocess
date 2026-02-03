---
snapshot_id: "MIX-001-MIXING-TIME-SCALE-FAILURE"
status: "draft"
domain: "Process"
process: "Mixing"
topic: "Mixing Time-Scale Failure and Logical Lock-in of Control Authority"
level: "001"
note: "An open-structure risk analysis snapshot. This file examines whether the mixing time scale can continue to support underlying control assumptions when charging sequence and dosing logic are formally satisfied. The irreversibility discussed herein refers to logical control loss (logical lock-in), rather than equipment limits or thermal constraints."
dependencies:
  - "CHG-001-CHARGING-SEQUENCE"
  - "CHG-002-ADDITION-MODE-AND-RATE"
  - "TMP-001-THERMAL-AND-GAS-RISK"
  - "PHS-001-PHASE-BEHAVIOR"
  - "CRY-001-CRYSTALLIZATION-BEHAVIOR"
---

# MIX-001 | Mixing Time-Scale Failure (Non-Gate)

## 1. Positioning

This snapshot identifies a class of control failures that are frequently misdiagnosed during scale-up:

When the charging sequence is correct (CHG-001) and the dosing mode together with the nominal dosing rate are logically satisfied (CHG-002),  
an insufficient mixing time scale may still allow local reaction or phase histories to form **prior to the effectiveness of global control variables**,  
resulting in an irreversible, logical transfer of control authority (**logical lock-in**).

---

## 2. Core Distinction: Core Mixing Failure vs Mixing as Manifestation

### A | Core Mixing Failure

Mixing constitutes a **necessary control precondition**.

When the mixing time scale exceeds the characteristic reaction or physical-transformation time scale,  
local reaction or phase histories are established prior to homogenization,  
and control authority cannot be recovered through subsequent operational adjustments.

**Diagnostic characteristics:**

- Extending reaction time does not recover control authority;
- Modifying dosing structure does not recover control authority;
- Only structural intervention at the mixing layer can prevent failure.

---

### B | Mixing as Manifestation

Mixing is **not the dominant driver** of failure.

Under scale-up conditions, changes in mixing capability alter the exposure and manifestation of latent issues,  
causing them to appear earlier or with greater severity.

**Diagnostic characteristics:**

- Control authority can be recovered by addressing the dominant non-mixing driver;
- Mixing functions as a secondary control lever rather than a control precondition.

---

## 3. Category A Cases | Core Mixing Failure (Control Loss Is Inevitable)

### Case A1 | Path Lock-in in a Biphasic Hydrolysis During Scale-Up

**System conditions**

The substrate is soluble in the organic phase and insoluble in water.  
The target hydrolysis proceeds exclusively at the organic–aqueous interface.  
At small scale, limited system volume and high energy input density ensure rapid interfacial renewal.  
Upon scale-up, reactor geometry and agitation characteristics reduce interfacial renewal frequency.

**Observed scale-up behavior**

- Prolonged residence of reactant within the organic phase;
- Extended residence of hydrolyzed product within the alkaline aqueous phase;
- Progressive accumulation of side reactions with time.

#### Decision Trace

**Hypothesis Space**

- H1: Dosing structure or dosing-rate limitation (CHG-002)  
- H2: Phase-distribution limitation recoverable by time extension (PHS)  
- H3: Mixing time-scale failure (MIX-001)

**Elimination Path**

- Reduction of dosing rate fails to restore the intended reaction pathway → eliminate H1;  
- Extension of reaction time amplifies side reactions → eliminate H2.

**Decision Pivot**

Interfacial reactions occur prior to spatial homogenization.  
Once local reaction history is established, it irreversibly governs the overall reaction outcome.

**Explicit Labels**

- MIX-001: true  
- Recoverable_by_time: false  
- Recoverable_by_dosing: false  

---

### Case A2 | Failure of a System Requiring Instantaneous Dispersion Upon Dosing

**System conditions**

The system is highly sensitive to local concentration and requires rapid spatial homogenization following dosing.  
This assumption holds implicitly at small scale.

**Observed scale-up behavior**

- Side reactions initiate at an early dosing stage even at low nominal dosing rates;
- Side-reaction onset precedes completion of mixing.

#### Decision Trace

**Hypothesis Space**

- H1: Dosing rate remains excessive (CHG-002)  
- H2: Mixing time-scale insufficiency (MIX-001)

**Elimination Path**

- Further reduction of dosing rate fails to suppress side reactions;  
- Extension of reaction time increases the side-reaction fraction.

**Decision Pivot**

Side reactions initiate prior to completion of mixing.  
Local concentration history is non-recoverable.

**Explicit Labels**

- MIX-001: true  
- Recoverable_by_time: false  

---

## 4. Category B Cases | Mixing as Manifestation (Dominant Driver Elsewhere)

### Case B1 | Local High-Activity Exposure in a BF₃-Catalyzed System

**System conditions**

A BF₃ complex is employed as a catalytic reagent and introduced at high effective concentration.  
At small scale, rapid spatial homogenization prevents abnormal local catalytic activity.  
At scale, transient regions of excessively high catalytic activity emerge during catalyst addition.

#### Decision Trace

**Hypothesis Space**

- H1: Mixing time-scale failure (MIX-001)  
- H2: Catalyst addition structure leading to excessive local activity density (CHG-002)

**Elimination Path**

- Slowing catalyst addition or pre-diluting the catalyst restores the intended reaction pathway → eliminate H1.

**Decision Pivot**

Control authority is recoverable through adjustment of catalyst addition structure and effective concentration.

**Explicit Labels**

- MIX-001: false  
- CHG-002: true  

---

### Case B2 | Acidification-Induced Oil-Out During Organic Acid Precipitation

**System conditions**

Hydrochloric acid is added to convert an organic salt into its free organic acid, which is intended to precipitate as a solid.  
At scale, the local acidification rate exceeds the nucleation and solidification kinetics of the organic acid.

#### Decision Trace

**Hypothesis Space**

- H1: Mixing time-scale failure (MIX-001)  
- H2: Phase-transition and precipitation-pathway selection (PHS / CRY)

**Elimination Path**

- Reduction of acid addition rate and improvement of spatial distribution restore solid precipitation → eliminate H1.

**Decision Pivot**

Mixing modifies pathway exposure rather than the dominant kinetic drivers governing nucleation and precipitation.

**Explicit Labels**

- MIX-001: false  
- Primary_driver: Phase / Crystallization  

---

## 5. Usage Guidance

- Category A cases require intervention at the mixing layer as a primary control measure;
- Category B cases require addressing the dominant non-mixing driver, with mixing considered as a secondary control lever;
- Phenomenological similarity to mixing-related issues should not justify automatic classification as MIX-001.

---

#Audit: This snapshot describes a logical lock-in mode of control loss at the mixing layer. Identification relies on evaluating whether control authority can be recovered through time extension or dosing-structure adjustment, rather than on phenomenological similarity alone.
If mixing time-scale failure has already caused irreversible expansion of reaction pathways or local reaction domains, subsequent temperature adjustment can only delay consequences and cannot restore control authority; such cases should not be classified as thermal control authority (see THR-001).
