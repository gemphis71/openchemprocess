---
snapshot_id: "WRKUP-002-PARTITION-RATIO-DRIFT-INVENTORY-CONTROL"
status: "draft"
domain: "Process"
process: "Workup"
topic: "Partition-ratio drift: phase-environment drift / chemical speciation drift / industrial workflow risk tags (Soft Gate)"
level: "001"
language: en  
canonical_id: WRKUP-002-PARTITION-RATIO-DRIFT-INVENTORY-CONTROL
dependencies:
  - "WRKUP-001-WORKUP-CONTROL-AUTHORITY"
  - "MIX-001-MIXING-TIME-SCALE-FAILURE"
  - "THR-001-THERMAL-CONTROL-AUTHORITY"
note:
  - "Machine-review oriented: use Δkd between Wash/Extract #1 and #2 as an early discriminator. Trigger causality attribution and soft blocking to prevent loss amplification and downstream rework."
---

# wrkup-002｜phase redistribution & inventory control

## partition-ratio drift ($K_{d/w}$ drift) as a soft gate

## 1. positioning

This chapter treats extraction/washing as **inventory redistribution** and makes it auditable in three inventories:

- product inventory: where the product ends up (organic vs aqueous)
- waste inventory: whether water-soluble/reactive impurities are robustly removed
- carryover inventory: whether salts/metals/complexes/co-solvents/water are carried into the next reaction world

This is a **soft gate**: it does not reject a process immediately, but enforces structured **causality attribution** for high-attrition / high-rework paths.

Output levels:
- flag: additional evidence + causality attribution required before proceeding or replicating at scale
- soft block: do not extend/replicate the current workup plan until causality attribution is completed

## 2. foundational criteria

### 2.1 $K_{d/w}$ definition and consistency ($K_{d/w}$ consistency)

**definition (mass-balance basis)** $K_{d/w}$ = (total target amount in organic phase) / (total target amount in aqueous phase)

Compute “total amount” using **concentration × phase mass (by weighing)** (avoid volume-based shortcuts):
- $K_{d/w}$ = $(c_{org} \times m_{org}) / (c_{aq} \times m_{aq})$

Where:
- $m_{org}$, $m_{aq}$: phase masses (weighed)
- $c_{org}$, $c_{aq}$: analytical concentrations (any consistent units)

**consistency check (focus on #1→#2)** - $\Delta K_{d/w}(1 \rightarrow 2) = |K_{d/w,2} - K_{d/w,1}| / K_{d/w,1}$
- if $\Delta K_{d/w}(1 \rightarrow 2) > 15\%$: trigger soft block (**causality attribution** is mandatory before extending the same washing sequence)

The 15% threshold is an initial engineering criterion and may be **adjusted** based on product value and process risk, and **revised** as additional data become available.

### 2.2 phase-environment drift (phase-environment drift)

“Phase environment” means the **actual composition and physical state** of each phase during each wash: ionic strength, co-solvent content, water content in the organic, temperature window, and interfacial behavior. If the phase environment changes, $K_{d/w}$ is assumed non-equivalent.

**primary drift sources (auditable factors)**

1) wash#1 water becomes a brine-like environment (**in-situ loading drift**)
- Wash#1 may be nominally “water/acidic water/basic water”, yet it rapidly becomes **high ionic strength** upon contact:
  - loading-1: salts/metal salts/ionic byproducts partition into the aqueous phase
  - loading-2: neutralization during acid/base adjustment generates a salt-rich aqueous phase
- Wash#2 is often performed with a **low-ionic-strength aqueous wash** (no added salt) → a step change in ionic strength → elevated $K_{d/w}$ drift risk

2) mutual miscibility and co-solvent loading (mutual solubility & loading drift)
- THF/MeCN/IPA (and similar) are miscible or partially miscible with water
- recycled/looped solvent accumulates co-solvent and water → organic polarity increases → salt-carrying capacity and $K_{d/w}$ shift
- $K_{d/w}$ measured with fresh solvent is not interchangeable with $K_{d/w}$ under recycled-solvent conditions

3) hidden water in the organic phase (hidden water content)
- a few wt% water in the organic phase can materially change polarity and salt-carrying behavior → $K_{d/w}$ and carryover risk drift
- treat this as a phase-environment variable, not merely a “drying deficiency”

4) temperature window shift
- warm vs cold workup changes solubility contrast and the distribution window → $K_{d/w}(T)$ is not extrapolatable across temperature windows

5) rag layer / third phase
- longer settling/phase disengagement at scale + trace solids/metal salts/byproducts can accumulate at the interface and form a rag layer
- once a rag layer appears, the system is no longer a clean two-phase distribution problem; it becomes **three-phase inventory redistribution** with the interface as a loss channel
- early development should intentionally stress for rag-layer propensity (longer settling, repeated washes, ionic-strength and temperature-window switching) to assess visibility and repeatability

Emulsion and rag layer are interfacial phenomena governed by rule w2-3 (recording + inventory audit).

### 2.3 chemical speciation drift (species drift)

Species drift occurs when the target (or a critical component) partitions as **different chemical forms** across washes, making $K_{d/w}$ non-equivalent, typically:

- free form vs ionic/salt form (acid/base speciation equilibrium under pH changes)
- complexed / ion-paired form vs non-complexed form

Routine TLC/HPLC often cannot resolve complexes/organic salts/ion pairs as distinct “species”, so species drift is frequently misattributed to phase-environment drift.

## 3. failure modes

### I｜$K_{d/w}$ drift unchecked
- trigger: $\Delta K_{d/w}(1 \rightarrow 2) > 15\%$ without **causality attribution**; continued “wash-count” iteration
- outcome: target loss, emulsion/phase separation failure, rework amplification, downstream burden

### II｜chemical speciation drift missed
- misattribution: treating speciation/complexation as “ionic strength / solvent water / temperature” effects
- control: once drift triggers, run species-first check (rule w2-2) before deep phase-environment diagnostics

### III｜industrial-unfriendly workflow tag
- workflows/solvents structurally problematic at scale (VOCs, waste streams, transfer losses, condenser/line plugging due to water carryover, etc.)
- output as path-level risk tags; do not mix into $K_{d/w}$ mechanism explanations

## 4. representative cases

### case 1｜high-ionic-strength window → desalting wash: window switching drives $K_{d/w}(1 \rightarrow 2)$ drift (phase-environment drift)

**case header**
- system: target distribution is ionic-strength sensitive; mixture contains salts/metal salts/ionic byproducts; emulsification may occur
- plan: enter a high-ionic-strength “brine window” to lock-in or transfer, then switch to a low-ionic-strength desalting wash (no added salt)
- key drift: an ionic-strength step change plus Wash#1 aqueous loading → $K_{d/w}(1 \rightarrow 2)$ can shift materially

**subtype 1a｜lock-in**
- intent: keep target in organic while partitioning water-soluble byproducts into aqueous (cost: organic becomes salt-laden)
- risk: switching into desalting can reveal non-equivalent $K_{d/w}$ and drive target loss/emulsion/loss amplification

**subtype 1b｜transfer-out / salting-out**
- intent: reduce effective aqueous solubility and/or shift distribution to drive target transfer from aqueous to organic
- risk: switching into desalting can still trigger $K_{d/w}(1 \rightarrow 2)$ drift and loss

**key checks**
- Specify the origin of the high-ionic-strength condition in Wash#1 (loading-1, loading-2, or addition
- The failure mode is treating the two windows as kd-equivalent without measurement.

**control conclusion**
- if $\Delta K_{d/w}(1 \rightarrow 2) > 15\%$: explain the Wash#1 brine window formation and confirm the Wash#2 low-ionic-strength condition; otherwise soft block.

#audit: the mistake is not window switching; it is unvalidated $K_{d/w}$ equivalence across windows.

### case 2｜mutual miscibility exchange: $K_{d/w}$ drift driven by co-solvent/water exchange across washes (phase-environment drift)

**case header**
- system: organic solvent and water are miscible or partially miscible, leading to reciprocal phase loading (water-in-organic and solvent-in-aqueous)
- plan: Wash#1 alters both phases; Wash#2 proceeds on these “re-formulated” phases
- key drift: composition (water content/co-solvent fraction/polarity) changes across washes → $K_{d/w}(1 \rightarrow 2)$ cannot be assumed equivalent

**key checks**
- Wash#1 typically includes:
  - water → organic: raises organic water content and polarity
  - organic → aqueous: loads aqueous with organic/co-solvent, changing aqueous properties
- Wash#2 occurs on altered phases; $K_{d/w}$ drift is expected unless demonstrated otherwise.

**control conclusion**
- in mutually miscible systems, $K_{d/w}(1 \rightarrow 2)$ must be checked; $\Delta K_{d/w}(1 \rightarrow 2) > 15\%$ triggers rule w2-1.

#audit: in miscible/partially miscible systems, “repeat wash” ≠ “repeat environment”.

### case 3｜rag layer (third phase) as an unaudited inventory-loss channel (phase-environment drift: physical manifestation)

**case header**
- system: prolonged settling/phase disengagement at scale; trace solids/metal salts/byproducts accumulate and form a rag layer
- plan: a persistent interfacial layer appears, complicating separation and potentially carrying product into waste
- key drift: two-phase model breaks → three-phase redistribution; the rag layer becomes a separate inventory channel

**key checks**
- treat the rag layer as a third phase; $K_{d/w}$ only describes the two bulk phases and does not capture interfacial inventory.
- mitigation is highly case-specific; this chapter requires explicit inventory audit.

**control conclusion**
- when a rag layer appears:
  - record wash index, disengagement time, temperature, salt/acid/base conditions (diagnostic inputs)
  - estimate target content in the rag layer (coarse quantification acceptable); otherwise it is an unaudited loss channel
- visible rag layer without inventory audit → soft block (do not replicate as a stable two-phase workflow).

#audit: the key question is not “how to eliminate quickly”, but whether interfacial inventory is unaccounted.

### case 4｜temperature window as a $K_{d/w}$ modality: heating/cooling changes solubility contrast (temperature window shift)

**case header**
- system: room-temperature $K_{d/w}$ is poor (often limited by organic solubility or insufficient solubility contrast)
- plan: screen temperature windows early (both heating and cooling) to reshape relative solubilities and distribution
- key drift: temperature changes solubility contrast → $K_{d/w}$ changes materially; window switching is a model change

**key checks**
- do not extrapolate $K_{d/w}$ across temperature windows.
- evidence required:
  1) $K_{d/w}$ in the selected temperature window (at least spanning Wash#1→#2)
  2) chemical stability over the hot/cold hold-time window

**control conclusion**
- missing $K_{d/w}(T)$ data or stability evidence → flag or soft block (risk-tiered).
- If temperature materially improves $K_{d/w}$​, formalize temperature as an explicit operating-window parameter in the workup design, not as a procedural workaround.

#audit: treat temperature as a partition-window variable, not a procedural speed knob.

### case 5｜speciation equilibrium: partial ionization drives $K_{d/w}$ jumps (chemical speciation drift)

**case header**
- system: target is an organic acid/base; free and ionic forms coexist at a given pH; TLC/HPLC often cannot resolve forms
- plan: pH/salt conditions differ between washes, or residual speciation persists under the same nominal pH
- key drift: measured $K_{d/w}$ reflects an effective distribution of a speciation mixture, not a single species

**key checks**
- pH control is speciation equilibrium control, not completion; residual ionic fraction follows pH–pKa (≈10× ratio per 1 pH unit).
- when $K_{d/w,free}$ and $K_{d/w,ion}$ differ substantially, a small ionic fraction can shift $K_{d/w,in-situ}$ away from $K_{d/w,ref}$.
- “pH on target” is not evidence of unified species; apply rule w2-2 (species-first).

**control conclusion**
- if $(K_{d/w,ref} - K_{d/w,in-situ}) / K_{d/w,ref} > 15\%$: speciation drift likely; do not enter phase-environment diagnostics until excluded.
- Where speciation mixing is confirmed and $K_{d/w}$​ is speciation-dependent, specify a target free/ion fraction as a workup design requirement, subject to stability limits.

#audit: pH is an equilibrium variable; small ionic fractions can produce large $K_{d/w}$ drift when $K_{d/w}$ is speciation-sensitive.

### case 6｜dichloromethane (DCM) and other industrial-unfriendly solvents (workflow risk tag)

**case header**
- system: some solvents are structurally problematic at scale (VOCs, waste, transfer loss, water-related condenser/line plugging)
- plan: transfer/back-transfer/concentration steps expose scale constraints
- key drift: do not explain as a $K_{d/w}$ mechanism; output industrial compatibility risk tags

**key checks**
- DCM can be advantageous for certain extractions, but scale constraints are often systemic.

**control conclusion**
- output risk tag + workflow redesign prompt (replaceable / not replaceable / constraint justification), not as a $K_{d/w}$ drift mechanism.

#audit: this is a scale-sustainability constraint, not a partition mechanism.

### case 6b｜recycled/looped solvent loading drift (phase-environment drift + industrial tag)

**case header**
- system: recycled solvent accumulates co-solvent/water, changing organic polarity and salt-carrying capacity
- plan: assumptions built on fresh-solvent windows fail under recycled-solvent batches
- key drift: recycled batch ≠ fresh batch → $K_{d/w}$ drift

**key checks**
- “same solvent name” does not imply “same phase environment”.

**control conclusion**
- before using recycled solvent for extraction, measure $K_{d/w}$ using the same-source recycled batch (covering Wash#1→#2); otherwise flag.

#audit: recycled solvent introduces silent phase-environment drift; unmeasured $K_{d/w}$ implies operation in an unvalidated window.

### case 7｜concentration-dependent $K_{d/w}$: non-linear distribution isotherms across concentration windows

**case header**
- system: self-association/aggregation or proximity to solubility/activity limits at high concentration; $K_{d/w}$ is non-linear vs concentration
- plan: low-concentration $K_{d/w}$ is used to infer high-concentration behavior (or wash dilution shifts the concentration window during the sequence)
- key drift: $K_{d/w}$ decreases (or curves) at higher concentrations; dilute data are not linearly extrapolatable

**key checks**
- with aggregation/saturation/strong activity-coefficient effects, $K_{d/w}$ is not constant.
- low-concentration $K_{d/w}$ cannot be extrapolated to high-concentration windows; wash dilution can introduce within-sequence $K_{d/w}$ drift.

**control conclusion**
- validate $K_{d/w}$ at the highest design concentration (worst-case); do not linearly extrapolate from dilute data.
- if $\Delta K_{d/w}(1 \rightarrow 2) > 15\%$ with a concurrent concentration-window shift, include concentration dependence in the top-priority diagnostic set.

#audit: $K_{d/w}$ non-linearity can masquerade as phase-environment drift; confirm the concentration window first.

### case 8｜reaction–partition coupling in reactive extraction (scavenging wash drift)

**case header**
- system: the wash includes a chemical transformation (e.g., sodium bisulfite scavenging of aldehydes; acid wash for basic impurities)
- plan: treat washing as partition-only while extent of reaction differs across washes (equivalents/hold time/window)
- key drift: $K_{d/w}$ swings reflect reaction progress changing species/inventory, not only phase environment

**key checks**
- reactive wash is not partition-only; reaction extent governs apparent $K_{d/w}$.
- incomplete reaction or non-equivalent reaction windows across washes produces large $K_{d/w}$ variability.

**control conclusion**
- once a wash is identified as reactive, diagnostic priority is fixed: species-first (rule w2-2) before phase-environment diagnostics.
- missing completion evidence (equivalents/time/window) → flag, even if emulsion is not obvious.

#audit: $K_{d/w}$ drift in reactive washes is often a reaction-extent problem, not a pure partition problem.

## 5. blocking rules

### rule w2-1｜$K_{d/w}$ drift soft block (15%)
- if $\Delta K_{d/w}(1 \rightarrow 2) > 15 \%$ with no explained cause: soft block (do not extend the same washing plan).

### rule w2-2｜species-first consistency check (15%)

**preconditions**
- acids/bases are assumed to exhibit mixed speciation (free ↔ ionic) by default; TLC/HPLC often cannot resolve forms.
- once w2-1 triggers, the diagnostic order is fixed: species first, then phase environment.

**check (reference-based, directional)**
- $K_{d/w,ref}$: reference free/non-complexed form (or forced-unified speciation)
- $K_{d/w,in-situ}$: measured in the real mixture

if:
- $(K_{d/w,ref} - K_{d/w,in-situ}) / K_{d/w,ref} > 15\%$

then:
- species drift likely; do not enter phase-environment diagnostics until species drift is excluded.

supplement:
- if $K_{d/w,in-situ} \geq K_{d/w,ref}$, this directional trigger does not apply; proceed to phase-environment diagnostics.

### rule w2-3｜interfacial phenomenon audit (emulsion / rag layer)
- emulsion and rag layer must be recorded (wash index, phase disengagement time, temperature, salt/acid/base conditions).
- diagnose as phase-environment symptoms (ionic strength/density/interfacial conditions/co-solvent/water/temperature).
- estimate target content in the interfacial layer (coarse quantification acceptable); otherwise it is an unaudited loss channel.
- addendum (self-emulsification): amphiphilic targets/intermediates may increase self-emulsification with conversion. use **phase disengagement time** as a $K_{d/w}$ shadow indicator; systematic amplification across washes (minutes → hours or clear non-linear growth) triggers interfacial inventory audit and allows escalation to soft block.

### rule w2-4｜industrial-unfriendly workflow tag
- for path-level risks (e.g., DCM), output risk tag + workflow redesign prompt; do not mix into $K_{d/w}$ mechanism explanations.

### rule w2-5｜recycled solvent loading drift
- when using recycled/looped solvent: measure $K_{d/w}$ using the same-source recycled batch (at least covering Wash#1→#2).
- if $K_{d/w}$ differs from fresh-solvent $K_{d/w}$ by > 15%: treat as phase-environment drift and diagnose.
- missing this test → flag.

## 6. method summary (machine-oriented)

- control variable: $K_{d/w}$; early monitor: $\Delta K_{d/w}(1 \rightarrow 2)$
- diagnostic order: rule w2-2 (species-first) → phase-environment drift
- interfacial phenomena: rule w2-3 (record + target inventory audit)
- recycled solvent and industrial-unfriendly solvents: path-level tags (rule w2-4 / w2-5)

## #audit

Use 1→2 $\Delta K_{d/w}$ as an early soft-block discriminator; prioritize chemical speciation drift via $K_{d/w,ref}$ vs $K_{d/w,in-situ}$; audit emulsion/rag layer as interfacial inventory-loss channels; tag recycled-solvent loading drift and DCM workflow constraints as path-level risks and trigger workflow redesign.

## 7. Machine Annotation

```yaml
schema_version: "risk_annotation_schema_v0.2"
annotation_scope: "chapter_level"
canonical_id: "WRKUP-002-PARTITION-RATIO-DRIFT-INVENTORY-CONTROL"
process_stage: "workup_phase_redistribution_inventory_control"

transition_model: "two_phase_inventory_redistribution_to_partition_ratio_drift_soft_gate"

control_window: >
  Extraction and washing are treated as inventory redistribution rather than simple impurity removal. The relevant inventories are product inventory, waste inventory, and carryover inventory. Control authority is exercised by detecting whether the partition environment remains equivalent across washes and by blocking wash-count iteration when Kd drift indicates non-equivalent phase environment or species state.

core_judgment: >
  The central machine-review task is to detect whether a workup sequence assumes repeated washes are equivalent when Kd has drifted across Wash/Extract #1 and #2. When Delta Kd(1->2) exceeds the review threshold, the process should enter structured causality attribution rather than continuing wash-count optimization.

review_gates:
  kd_drift_soft_gate:
    - "Delta Kd(1->2) > 15% without explained cause"
    - "continued wash-count iteration despite unexplained Kd drift"
  species_first_gate:
    - "acid/base target with possible free/ionic speciation"
    - "complexed or ion-paired form possible"
    - "Kd_ref vs Kd_in_situ differs by >15% in the directional species-first check"
    - "reactive wash identified"
  phase_environment_gate:
    - "ionic strength changes between Wash#1 and Wash#2"
    - "Wash#1 becomes brine-like through in-situ loading"
    - "mutual miscibility or co-solvent loading changes phase composition"
    - "hidden water in organic phase changes polarity or salt-carrying behavior"
    - "temperature window changes between washes"
  interfacial_inventory_gate:
    - "emulsion observed"
    - "rag layer observed"
    - "phase disengagement time increases nonlinearly across washes"
    - "interfacial target inventory not quantified"
  path_level_risk_gate:
    - "industrial-unfriendly solvent or workflow risk tag present"
    - "recycled or looped solvent used without same-source Kd verification"
    - "DCM or similar path-level solvent risk used without replacement or constraint justification"

risk_signals:
  - "Delta Kd(1->2) > 15%"
  - "Kd drift unexplained"
  - "wash-count iteration continues after Kd drift"
  - "target loss across wash sequence"
  - "emulsion or phase separation failure"
  - "rework amplification after washing"
  - "Wash#1 brine-like environment formed by salts, metal salts, ionic byproducts, or neutralization"
  - "Wash#2 low-ionic-strength desalting wash after high-ionic-strength Wash#1"
  - "unvalidated Kd equivalence across high-ionic-strength and low-ionic-strength windows"
  - "mutual miscibility between organic solvent and water"
  - "co-solvent or water loading across washes"
  - "recycled solvent accumulates water or co-solvent"
  - "fresh-solvent Kd used for recycled-solvent workup"
  - "hidden water in organic phase"
  - "temperature window shift without Kd(T)"
  - "missing chemical stability evidence for hot or cold workup window"
  - "rag layer observed"
  - "visible rag layer without inventory audit"
  - "emulsion observed without interfacial inventory audit"
  - "phase disengagement time increases from minutes to hours"
  - "free/ionic speciation mixture possible"
  - "pH on target treated as species-unification evidence"
  - "complexed or ion-paired species unresolved by TLC/HPLC"
  - "Kd_ref and Kd_in_situ differ by >15%"
  - "reactive wash treated as partition-only"
  - "missing reaction completion evidence in reactive wash"
  - "concentration window shifts during washing"
  - "low-concentration Kd extrapolated to high-concentration workup"
  - "industrial-unfriendly workflow risk tag present"
  - "DCM path-level risk requires path-rethink"

reasoning_anchors:
  - "control_authority_decay"
  - "misallocated_control_authority"
  - "inventory_redistribution"
  - "partition_ratio_drift"
  - "kd_consistency_check"
  - "phase_environment_drift"
  - "chemical_speciation_drift"
  - "species_first_diagnostic_order"
  - "wash_count_iteration"
  - "interfacial_inventory_loss_channel"
  - "rag_layer_third_phase"
  - "emulsion_inventory_audit"
  - "recycled_solvent_loading_drift"
  - "temperature_partition_window"
  - "concentration_dependent_partitioning"
  - "reaction_partition_coupling"
  - "industrial_workflow_risk_tag"
  - "carryover_inventory"

taxonomy_role:
  reused_formal_anchors:
    - "control_authority_decay"
    - "misallocated_control_authority"
  candidate_anchors:
    - "inventory_redistribution"
    - "partition_ratio_drift"
    - "kd_consistency_check"
    - "phase_environment_drift"
    - "chemical_speciation_drift"
    - "species_first_diagnostic_order"
    - "wash_count_iteration"
    - "interfacial_inventory_loss_channel"
    - "rag_layer_third_phase"
    - "emulsion_inventory_audit"
    - "recycled_solvent_loading_drift"
    - "temperature_partition_window"
    - "concentration_dependent_partitioning"
    - "reaction_partition_coupling"
    - "industrial_workflow_risk_tag"
    - "carryover_inventory"

expert_judgment:
  - "Repeated washing should not be assumed to repeat the same partition environment."
  - "Delta Kd(1->2) is an early discriminator for non-equivalent phase environment or species state, not a deterministic rejection rule."
  - "Once unexplained Kd drift appears, review should stop wash-count iteration and require causality attribution."
  - "Species drift should be checked before deep phase-environment diagnostics when acid/base speciation, complexation, ion pairing, or reactive washing is plausible."
  - "Rag layer and emulsion should be reviewed as inventory channels, not merely as operational inconvenience."
  - "Recycled solvent and industrial-unfriendly solvent choices should be tagged as path-level risks when they affect phase environment, carryover inventory, waste, transfer, or scale sustainability."

uncertainty_and_exceptions:
  - "The 15% Delta Kd threshold is an initial engineering criterion and may be adjusted based on product value, process risk, analytical variability, and company standards."
  - "Kd drift does not by itself identify cause; it only triggers species-first and phase-environment attribution."
  - "High-ionic-strength window switching may be intentional and valid; the risk is unvalidated Kd equivalence across windows."
  - "Temperature can be a valid partition-window variable if Kd(T) and stability evidence are available."
  - "DCM or other industrial-unfriendly solvents may be justified in specific cases, but require explicit replacement assessment or constraint justification."
  - "Interfacial layer mitigation is case-specific; the minimum requirement is inventory audit before replication or scale-up."

quantitative_or_flag_triggers:
  kd_drift_soft_block: "Delta Kd(1->2) > 15% without explained cause"
  species_first_directional_check: "(Kd_ref - Kd_in_situ) / Kd_ref > 15%"
  recycled_solvent_kd_shift: "recycled-solvent Kd differs from fresh-solvent Kd by >15%"
  phase_disengagement_shadow_signal: "systematic amplification across washes, e.g. minutes to hours or nonlinear growth"
  rag_layer_audit_required: "visible rag layer"
  emulsion_audit_required: "emulsion observed"
  kd_temperature_window_required: "temperature window shift"
  highest_concentration_kd_required: "concentration-dependent Kd suspected"
  reactive_wash_completion_required: "reactive wash identified"

required_review_fields:
  - "Kd_1"
  - "Kd_2"
  - "Delta_Kd_1_to_2"
  - "phase_mass_basis"
  - "organic_phase_concentration"
  - "aqueous_phase_concentration"
  - "wash_index"
  - "ionic_strength_or_salt_loading_source"
  - "co_solvent_content"
  - "organic_water_content"
  - "temperature_window"
  - "phase_disengagement_time"
  - "rag_layer_or_emulsion_flag"
  - "interfacial_target_inventory_if_present"
  - "Kd_ref"
  - "Kd_in_situ"
  - "species_drift_assessment"
  - "reactive_wash_completion_evidence_if_any"
  - "recycled_solvent_source_if_any"
  - "industrial_workflow_risk_tag_if_any"

machine_use: >
  Review whether an extraction or washing sequence treats repeated washes as Kd-equivalent despite Delta Kd(1->2) drift; trigger species-first attribution before phase-environment diagnostics; audit emulsion or rag layer as interfacial inventory-loss channels; and separate industrial workflow risk tags from mechanistic Kd drift explanations.
```