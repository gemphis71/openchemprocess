
---
snapshot_id: "ISOL-001-CRYSTALLIZATION"
status: "draft"
domain: "Process"
process: "Isolation"
topic: "Crystallization: Transition from Solution-Phase Control to Solid-State Commitment"
level: "001"
language: en  
canonical_id: ISOL-001-CRYSTALLIZATION
dependencies:
  - "WRKUP-003-SOLVENT-REMOVAL-DRIVEN-ACCUMULATION-AND-THERMAL-EXPOSURE-CONTROL"
  - "WRKUP-002-PARTITION-RATIO-DRIFT-INVENTORY-CONTROL"
  - "MIX-001-MIXING-TIME-SCALE-FAILURE"
  - "THR-001-THERMAL-CONTROL-AUTHORITY"
note:
  - "Machine-review oriented: Defines the control window and scale-up risks of primary crystallization through recovery rates, first-pass impurity rejection, supersaturation control, and solid-form management."
---

# **ISOL-001: Crystallization**

---

## **1. System Role**

Crystallization is the **first phase transition unit  in the OpenChemProcess sequence: from liquid phase to solid phase**.

The preceding chapters (WRKUP-001 to WRKUP-003) all operate within the **liquid-phase domain**, where operators can continuously and reversibly influence the future evolution of the system through variables such as solvent composition, phase ratio, temperature, concentration, acid–base state, phase transfer, and concentration. Once crystallization occurs, **a fundamental shift of control authority takes place**: the system transitions from a tunable state governed by solution distribution to a partially locked state dominated by solid form.

This core transition can be expressed as:

solution inventory → solid inventory  
solution-phase control → solid-state commitment

Therefore, the core definition of this chapter is:

> **Crystallization is the transition from solution-phase control to solid-state commitment.**

“Solid-state commitment” does not mean that all properties become completely immutable, but rather that once the product enters the solid phase, the available degrees of freedom are significantly reduced; polymorph, salt form, morphology, and mother liquor inclusion formed at this stage can only be managed downstream, and their origins are difficult to reverse.

Therefore, the focus of ISOL-001 is not to present crystallization as a crystallography theory overview, but to address a more process-oriented question:

> **How to deliver the product into the solid phase with the highest possible recovery and with the least amount of high-content impurities, within the final window where solution-phase control still exists.**

---

## **2. Design Objectives**

### **2.1 Primary Objective of Crystallization: Maximum Recovery**

The primary objective of crystallization (primary crystallization) is:

maximum product recovery

That is, to transfer the product from the post-workup solution system into a solid state that is separable, transferable, and further processable.

At this stage, the obtained solid **does not need to be the final optimal solid form**. The following are acceptable:

- imperfect crystals
    
- impurity-containing crystals
    
- amorphous solids
    
- poorly defined morphology
    
- non-final polymorph
    
- salt / hydrate / solvate forms
    

The criterion is that the solid enables effective product isolation and facilitates subsequent solid–liquid separation.

---

### **2.2 Secondary Task: First-Pass Impurity Rejection**

Primary objective: recovery; concurrent objective: impurity rejection.

The impurities referred to here are not ppm-level minor impurities, but bulk impurities, such as:

- reaction solvents or high-boiling residual solvents
    
- acids, bases, organic bases used in reaction
    
- unreacted starting materials
    
- high-content by-products
    
- degradation products of starting materials or product
    
- water, salts, organic acids, inorganic acids, organic bases, inorganic bases introduced or retained during extraction
    
- other residual modifiers that significantly alter product solubility behavior
    

Empirically:

- impurity content **≥10 wt%** requires attention
    
- impurity content **≥20 wt%** usually requires explicit removal design in the process
    

Therefore, the correct question for primary crystallization is not:  
“Can this product crystallize?”  
but rather:  
“Which high-content components in the system must remain in the mother liquor and must not enter the solid phase?”

---

### **2.3 Boundary with Recrystallization**

Primary crystallization and recrystallization have different optimization objectives.

- **Crystallization = isolation + first-pass impurity rejection**
    
- **Recrystallization = purification + impurity discrimination**
    

The former prioritizes recovery, while the latter prioritizes purity.  
The former mainly handles bulk impurities, while the latter focuses on structurally similar minor impurities or difficult-to-remove trace impurities.

Therefore, this chapter does not define primary crystallization as final purification, but as:

> **the first targeted impurity rejection under the premise of high recovery.**

---

## **3. Solubility Engineering**

### **3.1 Core Design Logic: From Workup Solution to Minimum Solubility Condition**

The starting point of crystallization design is not to discuss crystal quality, but to answer:

> **Under what conditions is the product solubility minimized?**

That is:

find minimum solubility state  
drive workup solution toward minimum solubility condition

The starting point should be clearly defined as:

workup solution

rather than the original reaction mixture. Crystallization typically operates on a solution inventory that has undergone workup, extraction, phase transfer, and concentration, rather than the untreated reaction mixture.

Factors determining the minimum solubility condition typically include:

- solvent type
    
- solvent mixture ratio
    
- temperature
    
- salt form
    
- polymorph
    
- hydrate / solvate formation
    
- ionic strength / phase environment
    

The core of crystallization design is to progressively drive the current workup solution toward this minimum solubility condition.

Available implementation approaches include:

- cooling
    
- solvent exchange
    
- anti-solvent addition
    
- solvent composition change
    
- salt formation
    
- hydrate / solvate induction
    
- preferential removal of components that significantly increase product solubility
    

---

### **3.2 Empirical Solubility Classification**

In process development, crystallization systems can be initially screened using empirical solubility windows.

For primary crystallization, it is generally required that the product has sufficiently low solubility in a “anti-solvent” and sufficiently high solubility in a “good solvent,” to establish a usable solubility difference.

Empirical reference:

- **anti-solvent**: product solubility **< 1 g / 15 g solvent**, preferably **< 1 g / 30 g solvent**
    
- **good solvent (usually with heating)**: product solubility **> 3 g / 10 g solvent**
    

These values are empirical ranges for process development, **not fixed standards**; actual thresholds should be adjusted based on product value, target recovery, operating temperature, filtration loss, and downstream purification requirements.

> For primary crystallization, the ideal system typically requires: **high solubility at elevated temperature, and significantly reduced solubility upon cooling or anti-solvent addition.** The key criterion is not the absolute solubility at a single point, but the **usable solubility gap**.

---

### **3.3 Solubility of pure and crude products must be determined independently**

> **Core Rule: Solubility measurement must distinguish between pure and crude product.**

**Operational principles:**

1. First measure the solubility baseline of **high-purity product (≈93–97% or higher)**
    
2. Then measure the solubility of the **crude system** in the same crystallization system
    

**Decision logic:**

- If `pure solubility ≈ crude solubility` → direct crystallization is feasible
    
- If `crude solubility >> pure solubility` (**difference ≥2–3×**) → the crude system contains components that significantly increase solubility
    

**Analysis approach:**  
Such influential impurities are typically present at relatively high levels (**5–20 wt%**) and can be traced through reaction balance and mass balance, and removed during upstream processing.

---

### **3.4 Effect of Impurities on Solubility**

In primary crystallization, the solubility of the pure product should be used as the basis for crystallization system selection; when crude solubility is elevated, it should be preferentially attributed to solubilizing components and resolved through upstream processing rather than adjusting the crystallization system itself.

**Case #1: Pentafluorophenol increases product solubility**  
After esterification, stoichiometric by-product pentafluorophenol, with certain acidity and lipophilicity, significantly increases the solubility of the product in the organic phase. By switching the workup solution to a DCM / MTBE crystallization system, the product exhibits very low solubility and crystallizes out, while pentafluorophenol remains in the mother liquor.

**Case #2: Residual DMF leads to crystallization failure**  
Due to its high boiling point, DMF remains at 10-30% after concentration and significantly increases product solubility in low-solubility systems. By enhancing extraction to reduce DMF below 5%, crystallization is restored.

## **3.5 Solvate and Hydrate**

Certain products can form **solvate / hydrate**, which can significantly alter their solubility and crystallization behavior.

**Case #3-A: DCM solvate**  
A polymorph of sofosbuvir exists as a DCM solvate. When >1 eq DCM is introduced into the system to induce solvate formation, the solubility decreases significantly, leading to complete precipitation of the product and a substantial increase in recovery.

**Case #3-B: Hydrate**  
A certain product does not crystallize readily in DCM, but after the addition of >1 eq water, a hydrate is formed, resulting in significantly reduced solubility and precipitation as a solid. Although DCM and water are immiscible, the hydrate can still act as a key solid-state intermediate.

**Common types:**  
Carboxylic acids, amines, and amino acid-type compounds are more prone to forming hydrates (stabilized by hydrogen bonding).

Therefore, solvate / hydrate should not be treated as incidental phenomena, but as **design variables that can be actively utilized in primary crystallization**.

---

## **3.6 Salt Formation Crystallization**

When the target product is an amine or an acid, salt formation can be used to alter solubility and induce crystallization.

**Key study points:**

- measure and compare `free form solubility` and `salt form solubility`
    
- in multi-acid systems, consider different salt stoichiometries such as **1:1 salt, 1:2 salt**, etc.
    

**Complex case (amphoteric molecules):**  
Molecules containing both acidic and basic functional groups (e.g., those with phosphate and amine groups) may exist in equilibria among sodium salts, zwitterions, and acid salts.

**Case #6 (salt-form equilibrium)**  
When supersaturation is generated too rapidly, **multiple salt forms may crystallize simultaneously**. This is typically reflected as assay deviation of 1–2%, pH deviation, and deviation in ionic molar ratios.

**Case #7 (co-crystallization of free form and salt)**  
When `free form solubility > salt form solubility` but the difference is small, rapid acid/base addition or rapid cooling may result in co-crystallization of free form and salt. This is typically observed as slightly elevated assay (100–101%), lower-than-theoretical recovery, and the presence of 3–5% free form in the product.

## **4. Supersaturation Control**

### **4.1 Supersaturation Is Not “The Higher the Better,” but a Controlled Window**

Supersaturation is the sole driving force for crystallization and the most critical adjustable variable. However, higher supersaturation is not always better: if too low, crystallization may be slow or fail to initiate; if too high, non-ideal outcomes may occur (crash crystallization, oil-out, polymorph loss of control, etc.). Therefore, the core of process control is to establish supersaturation at an appropriate rate and to consume it in a controlled manner, so that the system remains within a **supersaturation control window**.

Approaches to achieve this include:

- control of cooling rate
    
- control of anti-solvent addition rate
    
- control of acid / base addition rate
    
- introduction of seed crystals
    
- holding (aging) at the crystallization temperature
    
- control of local concentration gradients (addition point, mixing)
    

Here, MSZW is not treated as a central concept; instead, emphasis is placed on the experimentally observable **operational window**, i.e., the range in which the system can crystallize stably without losing control.

---

### **4.2 Crash Crystallization**

If supersaturation is established too rapidly within a short time, the system may enter crash crystallization.

Typical consequences include:

- irregular crystal morphology
    
- significantly increased surface area
    
- increased fines
    
- intensified impurity inclusion
    
- poor filtrability
    
- increased dissolution loss
    
- simultaneous loss of recovery and purity
    

**Case #8: Crash crystallization during scale-up**  
In small-scale experiments, crystallization is often carried out in glass vessels by gradual cooling followed by overnight stirring, which appears as “slow crystallization”; however, at larger scale, crystallization is typically induced by active cooling. If rapid cooling or anti-solvent addition continues after reaching the crystallization temperature, higher supersaturation will accumulate, ultimately leading to crash crystallization. Therefore, at the lab scale, it is necessary to identify in advance:

- the temperature at which crystallization begins
    
- the rate of solid formation
    
- how long the system must be held at that temperature to consume supersaturation
    

---

### **4.3 Local Supersaturation and Addition Sequence**

A moderate bulk concentration does not imply absence of local issues. During anti-solvent addition or acid/base addition, extremely high local supersaturation may be generated near the addition point, leading to local crash crystallization, undesired solid forms, fines, oil-out, or co-precipitation of multiple salt forms.

Industrial mitigation strategies include slow addition, appropriate addition points, and use of transfer pumps to reduce local gradients. In addition, the sequence of anti-solvent addition affects the supersaturation trajectory:

- commonly: `antisolvent → product solution`
    
- in some systems: if the product is nearly insoluble in the anti-solvent, `product solution → antisolvent` may be used, which alters nucleation and growth pathways
    

---

## **5. Nucleation and Seeding**

Many systems can crystallize without seeding, which often leads to underestimation of its importance. The role of seeding is not only to “initiate crystallization,” but also to:

- provide dominant nucleation sites
    
- shorten induction time
    
- direct the desired solid form
    
- preferentially consume supersaturation at defined surfaces
    
- improve reproducibility and scale-up robustness
    

Therefore, although seeding is not always strictly required, it should generally be regarded as an important **control safeguard**.

**Case #4: Failure of nucleation during scale-up**  
In small-scale experiments, crystallization proceeds within 15–30 minutes after seeding; however, at larger scale, no crystallization occurs after prolonged stirring, even with additional seeding. Eventually, crystallization is established only after extended agitation, repeated seeding, or generating a stable slurry in a smaller system and reintroducing it. This case demonstrates that successful crystallization at small scale does not guarantee stable crystallization at scale.

Empirically, during initial scale-up, particular attention should be given to:

- whether induction time is significantly extended
    
- whether seed loading is insufficient (recommended **1–5%**)
    
- whether seeds truly act as dominant nucleation centers
    

---

## **6. Solid Form Control**

Although primary crystallization focuses on recovery, this does not imply that solid form can be ignored. In ISOL-001, the purpose of considering solid form is to **select the lowest-solubility form favorable for high recovery**, rather than defining the final target polymorph for the product.

At minimum, the following should be considered:

- polymorph
    
- hydrate
    
- solvate
    
- salt form
    
- mixed solid forms
    

---

### **6.1 Batch-to-Batch Solid Form Consistency Monitoring**

During long-term production, polymorph or solid-form drift may lead to variations in crystallization behavior, solubility, recovery, and product quality. When a change in recovery exceeding approximately **5%** (either increase or decrease) is observed, solid-form variation should be investigated first.

It is recommended to establish `IR_form_consistency_flag` as a sampling-based indicator for batch-to-batch solid-form consistency.

**Case #5: Solid-form drift during long-term production**  
After dozens of production batches, product recovery suddenly decreased by 6%. IR comparison revealed that the polymorph had shifted from a stable form to a metastable form, leading to increased solubility and incomplete crystallization. Recovery was restored after adjusting crystallization conditions (introducing seeding and controlling cooling rate).

---

### **6.2 Solid Form Strategy for Unstable Products**

For products with limited stability (e.g., aldehydes, easily racemized compounds, or intermediates that continue reacting in crude form), the priority of primary crystallization is shifted forward: the objective becomes **rapid removal of the product from the reaction environment**, minimizing exposure to impurities.

In such cases, a system with extremely low solubility should be selected, and if necessary, a more stable intermediate solid form (e.g., salt, bisulfite adduct) may be used to achieve rapid isolation.

**Supplement to Case #8:** For unstable products, primary crystallization serves as a rapid isolation strategy, while true purification is deferred to recrystallization.

---

## **7. Scale Sensitivity**

Crystallization is a highly scale-sensitive operation unit. Thermodynamic correctness does not guarantee successful scale-up, because crystallization is **kinetically controlled** and highly sensitive to equipment conditions.

Key differences during scale-up include:

- heating / cooling rates
    
- reactor thermal inertia and insulation
    
- mixing intensity and local flow patterns
    
- anti-solvent addition rate and location
    
- seed dispersion efficiency
    
- extension of induction time
    

These factors collectively determine how supersaturation is generated, whether nucleation can initiate successfully, whether growth dominates, and whether downstream filtration is feasible.

---

### **7.1 Thermodynamic Feasibility ≠ Scale-Up Feasibility**

**Kinetic parameters that must be evaluated at lab scale:**

- crystallization onset temperature
    
- crystallization rate
    
- rate of supersaturation generation and consumption
    
- effectiveness of seeding
    

**Case #4** and **Case #8** demonstrate that conditions effective at small scale may fail at larger scale due to differences in thermal history and mixing.

---

### **7.2 Interface to Filtration**

Primary crystallization must not only consider whether solids form, but also evaluate downstream filtration feasibility:

- whether crystal morphology is suitable for filtration (needle, plate, block)
    
- whether particle size distribution leads to long filtration time or poor washing
    
- whether mother liquor retention affects impurity removal
    

Empirically, mother liquor retention can be assessed via the wet-to-dry mass ratio:

- **wet mass < dry mass × 1.2** (mother liquor < 20% of dry solid): generally acceptable
    
- **wet mass ≥ dry mass × 1.5** (≥50%): requires attention
    
- **wet mass ≥ dry mass × 2.0** (≥100%): high risk
    

If the crystallization system is highly concentrated and retains large amounts of mother liquor, bulk impurities intended to remain in solution may be reintroduced into the filter cake, reducing purification effectiveness. Therefore, crystallization design must consider compatibility with downstream filtration from the outset.

---

## **8. Non-Ideal Outcomes**

Success criteria are not limited to solid formation but must meet quality and filtrability thresholds. Common non-ideal outcomes include:

- amorphous precipitation
    
- oil-out
    
- mixed salt / mixed polymorph
    
- excessive fines
    
- impurity trapping
    
- mother liquor retention-driven purity loss
    

---

### **8.1 Oil-Out**

Oil-out should be treated as an independent risk module and is defined as:

> **The system does not enter a stable solid–liquid crystallization pathway, but instead forms a product-rich liquid-like phase (oil phase).**

Once an oil phase forms, the product remains dissolved in that phase and cannot be converted into stable crystals, leading to loss of process control.

Common contributing factors include:

- excessively high local supersaturation
    
- difficulty in nucleation initiation
    
- overly rapid cooling
    
- inappropriate anti-solvent trajectory
    
- presence of trace components prone to emulsification or aggregation
    
- aggregation of amorphous precursors into an oil-like phase
    

Therefore, oil-out is not a simple variation of poor crystallization, but a **disaster signal** requiring independent root-cause analysis and risk management.

---

### **8.2 Amorphous Precipitation**

Amorphous precipitation typically indicates that supersaturation is generated too rapidly relative to crystal growth. It is associated with high surface area, strong adsorption of mother liquor and impurities, and increased burden on subsequent recrystallization. However, amorphous solids are not always unacceptable; if they exhibit very low solubility, can be filtered reliably, and can be safely handled, they may serve as a temporary intermediate state.

---

### **8.3 Co-Precipitation of Multiple Solid Forms**

When different salt forms or solid forms have similar solubility and supersaturation develops too rapidly, mixed-form co-precipitation may occur. The signals are often subtle (slightly elevated assay, slight pH deviation, slight deviation in stoichiometry), but fundamentally indicate the presence of mixed solid forms.

---

## **9. #Audit: Core Shadow Indicators**

|Indicator|Meaning|Trigger|
|---|---|---|
|`Crude_solubility_ratio`|crude / pure solubility|>2 → investigation|
|`Residual_modifier_content`|residual solubility modifiers (e.g., DMF)|>5% → Soft Block|
|`IR_form_consistency_flag`|batch solid-form consistency check|mandatory if recovery change >5%|
|`Salt_stoichiometry_deviation`|salt stoichiometry deviation|>3% → mixed salt warning|
|`Wet_cake_retention_ratio`|wet / dry mass ratio|>1.5 attention; >2.0 high risk|
|`Crash_risk_flag`|crash crystallization risk|review before scale-up|
|`Oil_out_flag`|presence of oil phase|requires root-cause analysis|

---

#Audit:  
The true value of primary crystallization is not merely to “isolate the product,” but to use the final window of liquid-phase control to retain bulk impurities in the mother liquor and deliver the product into a solid inventory that remains processable.

## 10. Machine Annotation

```yaml
schema_version: "risk_annotation_schema_v0.2"
annotation_scope: "chapter_level"
canonical_id: "ISOL-001-CRYSTALLIZATION"
process_stage: "isolation_crystallization"

transition_model: "solution_phase_control_to_solid_state_commitment"

control_window: >
  Primary crystallization is the last major window in which solution-phase variables can still be used to recover product, reject bulk impurities, and define the first solid inventory before later operations mainly handle consequences.

core_judgment: >
  The main machine-review task is to detect whether the crystallization design has addressed solubility gap, residual solubilizing modifiers, supersaturation generation, nucleation robustness, solid-form risk, and filtration compatibility before the system crosses into solid-state commitment.

risk_signals:
  - "crude_solubility_ratio > 2"
  - "residual_modifier_content > 5%"
  - "rapid supersaturation buildup"
  - "local supersaturation near antisolvent, acid, or base addition point"
  - "delayed or failed nucleation after seeding"
  - "yield shift > 5% across batches"
  - "wet_cake_retention_ratio > 1.5"
  - "wet_cake_retention_ratio > 2.0"
  - "oil_out_flag observed"
  - "salt_stoichiometry_deviation > 3%"
  - "mixed solid form or mixed salt form suspected"

expert_judgment:
  - "If crude solubility is significantly higher than pure-product solubility, crystallization failure is likely driven by residual solubilizing modifiers rather than by the intrinsic solvent system."
  - "If supersaturation is generated faster than it can be consumed through controlled nucleation and growth, the process is at risk of crash crystallization, amorphous precipitation, oil-out, or mixed solid-form precipitation."
  - "If nucleation depends on small-scale behavior and seeding is not robust, crystallization may fail to scale even when small-scale recovery appears acceptable."
  - "If wet cake retention is high, first-pass impurity rejection may be negated by mother liquor carryover."
  - "If solid-form consistency drifts across batches, yield and purity variation should be treated as a solid-state control issue rather than only as a solvent or recovery issue."

reasoning_anchors:
  - "control_authority_decay"
  - "solid_state_commitment"
  - "usable_solubility_gap"
  - "residual_modifier_effect"
  - "supersaturation_control_window"
  - "local_supersaturation"
  - "nucleation_scale_sensitivity"
  - "solid_form_drift"
  - "mother_liquor_retention"
  - "downstream_filtration_compatibility"

quantitative_triggers:
  crude_solubility_ratio: ">2"
  residual_modifier_content: ">5%"
  wet_cake_retention_ratio_warning: ">1.5"
  wet_cake_retention_ratio_high_risk: ">2.0"
  yield_shift_solid_form_check: ">5%"
  salt_stoichiometry_deviation: ">3%"

uncertainty: "medium"

exceptions:
  - "Amorphous or imperfect solids may be acceptable if they are stable, filterable, transferable, and intended only as an intermediate isolation form."
  - "High impurity content does not automatically invalidate crystallization if impurities are designed to remain in the mother liquor and wet cake retention is low."
  - "Oil-out and mixed solid forms require case-specific investigation and should not be treated as ordinary crystallization variation."
  - "Thresholds are empirical screening triggers, not universal pass/fail specifications."

machine_use: >
  Use this annotation to review whether a proposed primary crystallization design has addressed solubility gap, residual modifiers, supersaturation generation rate, nucleation robustness, solid-form risk, and filtration interface before the system crosses from solution-phase control into solid-state commitment.