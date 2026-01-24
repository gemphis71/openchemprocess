snapshot_id: "CHG-002-ADDITION-MODE-AND-RATE"  
status: "draft"  
domain: "Process"  
process: "Charging"  
topic: "Risk envelope of addition mode and dosing profile (open, non-gate)"  
level: "001"  
note: "Open risk-structure document; focuses on whether addition mode and rate still constitute an effective control lever. Thresholds and patterns are experience-based and subject to revision."  
dependencies:

- "CHG-001-CHARGING-SEQUENCE"
    
- "MIX-001-MIXING-ESTABLISHMENT"
    
- "TMP-001-THERMAL-AND-GAS-RISK"
    
- "MAT-001-FEED-EQUIVALENCE"
    

---

# CHG-002 Addition Mode and Dosing Profile — Risk Envelope (Non-Gate)

## 1. Positioning

This document identifies situations in which, **after the charging sequence has been fixed**,  
the **choice of addition mode or dosing profile** places the process at a structural disadvantage during scale-up.

It is not a yes/no gate. Instead, it serves as a **risk-indication layer** for whether control authority over charging still exists.

- Certain addition modes may _survive_ under specific conditions
    
- But should not be treated as default options
    
- Their use must be justified by clearly stated **conditions of validity and failure boundaries**
    

**Core judgment**:

> **Nominal dosing ≠ Effective dosing**  
> The discrepancy arises from phase-related barriers and time-scale delays encountered as material enters the reaction mass.

---

## 2. Classification of Risk Mechanisms

### Type I｜Phase-entry risk

During charging, material undergoes **phase separation or phase transition**,  
causing it to temporarily or persistently detach from the reaction mass (main circulation / bulk liquid),  
thereby weakening or eliminating charging as a control lever.

---

### Type II｜Rate-matching risk

Material has entered the reaction mass,  
but the **dosing profile (i.e., the rate at which material enters the reaction mass)** is mismatched with the reaction rate or heat-release rate,  
leading to the time-accumulation of **unreacted inventory** and approach to irreversible boundaries.

> Note: Type II presupposes that the reaction system is already reactive.  
> Scenarios involving non-initiated reactions, absence of activity, or intrinsic system failure are outside the scope of this type.

---

## 3. Pre-dosing State for Type I (General)

Before evaluating any Type I risk,  
the **physical context of the dosing entry point** must be explicitly defined;  
otherwise, subsequent judgments will be systematically distorted.

### 3.1 Spatial Mapping of the Entry Point

- Surface dosing vs. sub-surface introduction
    
- Proximity to high-shear regions (near impeller) vs. low-energy regions (away from main circulation / potential dead zones)
    

### 3.2 Local Momentum Context at Entry

- Free-fall entry
    
- Pressure-driven or jet introduction
    
- Diffusive entry after pre-dilution
    

**Structural conclusion**:

Under scale-up conditions,  
**the entry-point location and local momentum jointly determine the effective temporal weighting of dosing**.  
If the pre-dosing state resides in a low-momentum, low-exchange region,  
the probability of RP-I1 is systematically amplified.

---

## 4. Phase-entry Risk Patterns (Type I)

### RP-I1｜"Fails to enter": Floating or foaming layers delaying effective dosing

**Description**  
Due to poor wettability, density differences, or gas entrainment,  
material forms a floating or foaming layer at the liquid surface,  
remaining spatially isolated from the reaction mass.

**Scale-up mechanism (S-axis)**  
Interface renewal frequency decreases markedly with scale,  
transforming what is a transient phenomenon at small scale into a stable structure in production.

**Survive conditions**  
The material remains chemically inert while outside the bulk phase;  
and even if entrained collectively, does not trigger runaway heat release or side-reaction amplification.

**Failure boundary**  
The nominal dosing profile becomes fully decoupled from the effective dosing profile,  
forming **hidden inventory** that may be released in a concentrated manner at a later stage.

---

### RP-I2｜"Enters and exits": Phase transition or separation induced by dosing

**Description**  
After entering the vessel, the material rapidly undergoes phase changes, including:

- Low-temperature solidification (liquid → solid)
    
- Solubility-driven crystallization / salt precipitation
    
- Oiling-out or formation of stable emulsions
    

**Scale-up mechanism (S-axis)**  
Local temperature and composition gradients are harder to dissipate at scale,  
allowing phase transitions to occur near the dosing point and persist.

**Survive conditions**  
Phase changes are highly reversible,  
and the reversal time scale is significantly shorter than the system’s sensitivity window to heat release or impurity formation.

**Failure boundary**  
Formation of a stable isolated phase,  
causing “charging control” to degenerate into “phase-diffusion control.”

---

### RP-I3｜"Enters but is trapped": Agglomeration or crust formation creating solid micro-environments

**Description**  
Particles agglomerate after entry;  
insoluble products form surface layers,  
trapping byproducts or solvent within the solid interior.

**Scale-up mechanism (S-axis)**  
Low-shear environments during scale-up  
enable long-term structural stability of agglomerates.

**Survive conditions**  
Agglomeration and crusting do not retain critical materials;  
or the pathway is structurally eliminated early via **pre-wetting or slurry formation**.

**Failure boundary**  
External controls lose influence over internal solid-state conditions,  
leading to poor reproducibility, downstream processing difficulty, or quality risk.

---

## 5. Rate-matching Risk Patterns (Type II)

### RP-II1｜Accumulation of unreacted inventory due to induction period, detection lag, and dosing speed

**Description**  
The reaction exhibits an induction period or auto-accelerating behavior;  
process signals lag behind true reaction progress;  
and the dosing system has inherent inertia, including **control delay, line holdup, and discretized dosing progression**.

Under these conditions,  
**the rate at which material enters the reaction mass** becomes mismatched with the true consumption rate,  
causing nominally “controlled” dosing to generate sustained accumulation of **unreacted inventory**.

> Note: This class of risk is often not explicitly recognized at small scale.  
> With small quantities and fast system response, mismatches between entry rate and reaction rate rarely lead to significant inventory;  
> upon scale-up, this time-scale mismatch becomes a dominant risk driver.

**Scale-up mechanism (S-axis)**  
Scale-up increases mixing and heat-transfer response lag,  
and coarsens the achievable time granularity of dosing,  
compressing the operational window between “detecting change” and “adjusting dosing.”

**Survive conditions**  
Unreacted inventory remains within the remaining tolerance envelope of the system,  
and can be safely absorbed even after dosing cessation.

**Failure boundary**  
Near the trigger point,  
“stopping dosing” no longer equates to “stopping material entry”:  
**line holdup, discrete dosing events, and system inertia** continue to introduce material after the control command,  
driving the system across irreversible thresholds.

---

## 6. Usage Notes

- This is an **open structural document**
    
- Risk patterns and boundaries are experience-based and subject to revision
    
- The goal is to **identify scale sensitivity of charging control authority in advance**, not to issue safety conclusions
    

#Audit: This is a loss-of-charging-control risk class. Once the failure boundary is crossed, neither addition mode nor dosing rate remains an effective adjustment lever; such risks must be challenged during process design and scale-up review, not mitigated post hoc.