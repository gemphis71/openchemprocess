# Minimum Risk Taxonomy

status: working draft  
scope: derived from annotated OpenChemProcess snapshots  
current_schema: risk_annotation_schema_v0.2  

## Formal Reasoning Anchors

### control_authority_decay
Progressive loss of actionable process control as the system moves from reversible design variables toward less reversible material states.

### solid_state_commitment
A state in which product has entered solid inventory and later operations mainly handle the consequences of crystallization rather than fully reversing its origin.

### limited_control_regain
Temporary and constrained recovery of solution-phase control during recrystallization through the solid → solution → solid pathway.

### selective_repartitioning
Redistribution of product and impurities across solid and solution phases under constrained solubility space.

### misallocated_control_authority
Use of an operation as a control step when the required selectivity or decision authority actually belongs upstream or elsewhere.

### usable_solubility_gap
The practically useful solubility difference between dissolution and precipitation conditions.

### residual_modifier_effect
Increase or distortion of product solubility caused by residual high-content modifiers such as DMF, acids, bases, salts, or other solubilizing components.

### supersaturation_control_window
The operational range in which supersaturation is generated and consumed without crash crystallization, oil-out, amorphous precipitation, or uncontrolled nucleation.

### evaluation_window
A data-validity range within which recovery and impurity rejection measurements are meaningful for judging recrystallization selectivity.

### mother_liquor_retention
Carryover of mother liquor in wet cake that can negate impurity rejection achieved during crystallization or recrystallization.

## Candidate Terms

- local_supersaturation
- nucleation_scale_sensitivity
- solid_form_drift
- downstream_filtration_compatibility
- constrained_solubility_space
- delta_solubility_path
- kinetic_stability
- downstream_interface

## Quantitative Trigger Families

### ISOL-001 triggers
- crude_solubility_ratio > 2
- residual_modifier_content > 5%
- wet_cake_retention_ratio > 1.5
- wet_cake_retention_ratio > 2.0
- yield shift > 5%
- salt_stoichiometry_deviation > 3%

### ISOL-002 triggers
- key_impurity_rejection >= 90%
- recovery >= 80%
- major_impurity_rejection < 80%
- major_impurity_rejection < 70%
- valid_rejection_evaluation_window: recovery 40-85%
- wet_cake_ratio > 1.5
- wet_cake_ratio > 2.0
- rejection_variance > 10%
- solubility_ratio_shift > 2x

## Taxonomy Delta — WRKUP-003

### Reused formal reasoning anchors

- control_authority_decay
- misallocated_control_authority

### New candidate terms introduced

#### forced_composition_path
A process trajectory in which removal of volatile components forces the remaining liquid inventory through a defined and less reversible composition path.

#### nonvolatile_accumulation
Enrichment of salts, acids, bases, high-boiling residues, modifiers, or other nonvolatile species as solvent is removed.

#### composition_evolution_path
The solvent-composition trajectory followed during concentration or solvent exchange, including ratio drift, instability-zone crossing, and morphology or phase-behavior changes.

#### volatile_removal_trajectory
The evaporation or co-distillation order of volatile components during concentration, including azeotropy or volatility-order effects.

#### thermal_exposure_accumulation
Accumulation of temperature-time-concentration stress during concentration, especially under scale-up conditions where duration, temperature, and concentration may all increase.

#### early_solvent_exchange
Introduction of the next-step solvent before late-stage high-concentration or complete-dryness windows are reached.

#### equipment_transfer_boundary
A scale-up boundary where minimum stirrable volume, discharge path, solid transfer, or wet-product solvent target limits whether a concentration endpoint is operationally feasible.

#### upstream_solvent_selection_coupling
A review pattern in which downstream concentration or workup constraints feed back to extraction-solvent or reaction-solvent selection.

#### route_priority_review
A review pattern that evaluates whether product disengagement or concentration reduction should be preferred before accepting concentration plus solvent exchange.

### Candidate risk signals introduced

- CF > 3 with nonvolatile inventory present and undeclared
- CF > 5 in acid/base sensitive system with heating to complete dryness
- CF > 10 without explicit override
- mixed-solvent system without VRT volatility order
- mixed-solvent system without CEP composition-drift assessment
- heated concentration without scale-relevant degradation study
- final volume below minimum stirrable volume
- solid residue without transfer plan
- explosion hazard assessment missing before concentration

### Expert judgment patterns introduced

- Treat concentration as a forced composition trajectory rather than neutral solvent evaporation.
- Review concentration through CF, NV, VRT, CEP, TE, and OC together rather than as separate checklist items.
- Prefer route redesign, product disengagement, or CF reduction before accepting concentration plus solvent exchange.
- Do not treat small-scale complete dryness as automatically scalable.
- Do not treat thermal stability data as sufficient unless it covers scale-relevant temperature, time, and concentration.

## Taxonomy Delta — ISOL-003

### Reused formal reasoning anchors

- control_authority_decay
- solid_state_commitment
- misallocated_control_authority
- mother_liquor_retention

### Reused candidate terms

- downstream_filtration_compatibility
- downstream_interface

### New candidate terms introduced

#### consequence_stage_separation
A separation step that occurs after the main composition or solid-state control window has closed and therefore mainly realizes or amplifies previously formed material states.

#### loss_amplification_interface
A downstream interface where upstream solid, liquid, or impurity-state decisions become visible as yield loss, impurity carryover, solvent burden, or cycle-time burden.

#### structure_inheritance
A review pattern in which filtration performance is treated primarily as inherited from upstream PSD, morphology, fine-particle fraction, packing structure, and capillary retention tendency.

#### upstream_failure_exposure
The appearance of an upstream crystallization, recrystallization, or concentration failure at a later separation step where control authority is no longer available.

#### lab_scale_masking
A scale-up risk pattern in which thin cake, short path, small inventory, or unquantified retention makes a laboratory filtration appear acceptable while scale operability is not established.

#### scalability_failure
A condition where a process can be completed at laboratory scale but cannot be sustained or operated robustly at manufacturing scale.

#### wet_mass_ratio
Wet mass divided by dry mass or equivalent wet-cake burden indicator; used as a practical projection of separation efficiency, mother-liquor carryover, drying burden, and impurity-retention risk.

#### washing_displacement_efficiency
The extent to which washing replaces residual mother liquor or solvent state inside the wet cake, assessed by wash liquid composition versus residual liquid composition.

#### compensatory_filtration
Use of filtration equipment, washing, thin-layer handling, telescoping, or other downstream measures to manage losses without repairing the upstream solid-structure cause.

### Candidate risk signals introduced

- WMR >= 2
- WMR >= 3
- wet cake ratio >= 2
- lab filtration already difficult
- low permeability
- nonlinear flux decline
- nonlinear increase of separation time with cake thickness
- high mother liquor retention
- mother liquor retention not quantified
- moderate clogging
- unstable wet cake
- high fines fraction
- dense or compressible cake
- wash cannot penetrate cake
- washing cannot sustain impurity removal
- washing displacement efficiency not demonstrated
- breakthrough due to non-uniform cake
- high-boiling solvent retention
- preferential evaporation of low-boiling solvent without solvent exchange
- drying burden dominates downstream
- thin-layer lab filtration difficulty ignored
- filtration relies only on strong compensatory measures
- scale operability cannot be established

### Candidate quantitative trigger family — ISOL-003

- WMR < 1.2: low filtration-retention risk
- WMR 1.2-1.5: watch zone
- WMR >= 2: high filtration/drying burden risk
- WMR >= 3: non-scalability / redesign trigger
- wet cake ratio >= 2: high drying burden signal
- nonlinear separation time vs cake thickness: lab-masking / scale-up risk signal
- washing liquid composition vs residual liquid composition: washing displacement-efficiency check

### Expert judgment patterns introduced

- Treat filtration difficulty first as possible inherited solid-structure failure, not as a filtration operation error.
- Treat filtration as consequence-stage separation after solid-state commitment, not as a new purification or composition-control step.
- Treat WMR as a projection of upstream solid structure after control authority has largely disappeared.
- Distinguish valid outcome management from false control recovery when equipment or separation path is changed.
- If WMR is high, washing fails, or drying burden dominates, review should consider upstream restructuring or separation-path redesign before continued filtration optimization.

## Taxonomy Delta — ISOL-004

### Reused formal reasoning anchors

- control_authority_decay
- solid_state_commitment
- misallocated_control_authority

### Reused candidate terms

- consequence_stage_separation
- structure_inheritance
- upstream_failure_exposure
- lab_scale_masking
- scalability_failure

### New candidate terms introduced

#### drying_state_lock_in
The final fixation of solvent state and solvent location within the solid inventory during drying.

#### solvent_state_location_lock_in
A review pattern in which drying risk is governed by both solvent state and solvent location rather than by total solvent amount alone.

#### surface_composition_drift
Passive change in solvent composition at the particle surface during early drying, often caused by preferential evaporation of the anti-solvent or stronger retention of the good solvent.

#### surface_good_solvent_enrichment
Enrichment of a good solvent at the particle surface during drying, creating risk of local re-dissolution and adhesion.

#### surface_redissolution
Localized dissolution of the product surface caused by surface good-solvent enrichment or surface solvent-state drift.

#### rolling_agglomeration
Agglomeration or balling caused by adhesion amplification during rolling motion, especially in double-cone or similar drying equipment.

#### pore_bound_solvent_retention
Retention of solvent inside interparticle or intraparticle pores, especially when morphology creates spatial retention and mass-transfer resistance.

#### bound_solvent_state
A solvent state with reduced removability due to ionic interaction, hydrogen bonding, or other strong association with the product.

#### drying_plateau
A residual-solvent curve plateau indicating that conventional drying kinetics no longer remove solvent effectively.

#### static_predrying
A staged drying approach in which static vacuum drying precedes rolling or mechanical movement to reduce surface-driven agglomeration risk.

#### solvent_displacement
Replacement of a retained or bound pore solvent with another solvent state that is more removable under drying conditions.

#### drying_compensation_boundary
The boundary between valid drying-stage compensation and the need to return upstream to redesign morphology, salt form, or solvent system.

### Candidate risk signals introduced

- surface_good_solvent_state high
- surface_composition_drift yes
- surface solvent composition differs from mother liquor composition
- anti-solvent preferential evaporation
- good solvent enriched at particle surface
- surface re-dissolution during early drying
- rolling stage present in equipment
- double-cone rolling collision after surface good-solvent enrichment
- macroscopic balling observed
- agglomeration during drying
- needle or rod morphology
- pore structure likely from particle packing
- solvent retained in internal or interparticle pores
- salt form present
- hydrogen-bond-capable solvent present
- ionic or hydrogen-bond interaction between solvent and product suspected
- process relies only on vacuum, temperature, and time
- residual solvent curve reaches plateau
- plateau_check yes
- static lab drying masks rolling-induced balling
- thin-layer lab drying masks pore retention
- thick-bed mass-transfer limitation suspected
- extended vacuum time used as sole corrective action

### Candidate flag trigger family — ISOL-004

- surface_good_solvent_state: high / medium / low
- surface_composition_drift: yes / no
- morphology_tag: needle / rod / other
- is_salt_form: true / false
- solvent_hbond_capability: true / false
- plateau_check: yes / no
- static_drying_ratio: high / medium / low
- rolling_equipment_present: yes / no
- process_relies_only_on_vacuum_temperature_time: yes / no

### Expert judgment patterns introduced

- Treat drying as final solvent-state and solvent-location lock-in, not as neutral solvent removal.
- Treat balling as surface composition drift plus rolling amplification before attributing it to drying temperature or vacuum alone.
- Treat residual solvent plateau as possible pore-bound or bound-solvent retention before extending vacuum time.
- Distinguish free solvent removal from structural solvent retention.
- Treat static pre-drying, pre-wash, and solvent displacement as compensatory controls, not recovery of upstream solid-state control authority.
- If compensation fails, review should return upstream to morphology, salt form, or solvent-system reconstruction.

## Taxonomy Delta — WRKUP-002

### Reused formal reasoning anchors

- control_authority_decay
- misallocated_control_authority

### New candidate terms introduced

#### inventory_redistribution
A workup review pattern in which extraction or washing is treated as redistribution across product inventory, waste inventory, and carryover inventory.

#### partition_ratio_drift
A change in apparent or measured partition ratio across wash or extraction steps, indicating that the phase environment or species state may not be equivalent.

#### kd_consistency_check
A mass-balance-based check comparing Kd across Wash/Extract #1 and #2 to detect early non-equivalence in the washing sequence.

#### phase_environment_drift
A change in the actual phase composition or physical state across washes, including ionic strength, co-solvent content, organic water content, temperature window, or interfacial behavior.

#### chemical_speciation_drift
A change in the chemical form participating in partitioning, such as free versus ionic form, salt form, complexed form, or ion-paired form.

#### species_first_diagnostic_order
A diagnostic rule that checks chemical speciation drift before deep phase-environment diagnostics once Kd drift is triggered.

#### wash_count_iteration
Continuation of washing based on the number of washes rather than on validated partition equivalence or causality attribution.

#### interfacial_inventory_loss_channel
An interfacial layer or emulsion that carries target inventory outside the two bulk phases and therefore must be audited as a separate loss channel.

#### rag_layer_third_phase
A persistent interfacial layer that invalidates the clean two-phase Kd model and creates three-phase inventory redistribution.

#### emulsion_inventory_audit
A review requirement to record and, when possible, quantify target inventory in emulsion or interfacial material.

#### recycled_solvent_loading_drift
Phase-environment drift caused by accumulated co-solvent, water, salts, or other load in recycled or looped solvent.

#### temperature_partition_window
A temperature-defined partitioning window in which Kd must be measured directly rather than extrapolated from another temperature.

#### concentration_dependent_partitioning
Nonlinear Kd behavior caused by concentration-dependent self-association, aggregation, activity effects, or proximity to solubility limits.

#### reaction_partition_coupling
A reactive wash pattern in which apparent Kd changes reflect reaction extent or species conversion rather than partitioning alone.

#### industrial_workflow_risk_tag
A path-level risk label for solvents or workflows that create scale, waste, transfer, plugging, or sustainability constraints and should not be mixed into Kd-mechanism explanations.

#### carryover_inventory
Inventory carried into the next process world, such as salts, metals, complexes, co-solvents, water, or reactive residues.

### Candidate risk signals introduced

- Delta Kd(1->2) > 15%
- Kd drift unexplained
- wash-count iteration continues after Kd drift
- target loss across wash sequence
- emulsion or phase separation failure
- rework amplification after washing
- Wash#1 brine-like environment formed by salts, metal salts, ionic byproducts, or neutralization
- Wash#2 low-ionic-strength desalting wash after high-ionic-strength Wash#1
- unvalidated Kd equivalence across high-ionic-strength and low-ionic-strength windows
- mutual miscibility between organic solvent and water
- co-solvent or water loading across washes
- recycled solvent accumulates water or co-solvent
- fresh-solvent Kd used for recycled-solvent workup
- hidden water in organic phase
- temperature window shift without Kd(T)
- missing chemical stability evidence for hot or cold workup window
- rag layer observed
- visible rag layer without inventory audit
- emulsion observed without interfacial inventory audit
- phase disengagement time increases from minutes to hours
- free/ionic speciation mixture possible
- pH on target treated as species-unification evidence
- complexed or ion-paired species unresolved by TLC/HPLC
- Kd_ref and Kd_in_situ differ by >15%
- reactive wash treated as partition-only
- missing reaction completion evidence in reactive wash
- concentration window shifts during washing
- low-concentration Kd extrapolated to high-concentration workup
- industrial-unfriendly workflow risk tag present
- DCM path-level risk requires path-rethink

### Candidate quantitative trigger family — WRKUP-002

- Delta Kd(1->2) > 15%: soft block when unexplained
- (Kd_ref - Kd_in_situ) / Kd_ref > 15%: species-first directional trigger
- recycled-solvent Kd differs from fresh-solvent Kd by >15%: recycled solvent loading drift
- phase disengagement time increases from minutes to hours or grows nonlinearly: interfacial inventory audit
- visible rag layer: rag-layer inventory audit required
- emulsion observed: interfacial inventory audit required
- temperature window shift: Kd(T) and stability evidence required
- suspected concentration-dependent Kd: highest-design-concentration Kd required
- reactive wash identified: reaction completion evidence required

### Expert judgment patterns introduced

- Treat extraction and washing as inventory redistribution, not as repeatable impurity removal by wash count.
- Treat Delta Kd(1->2) as an early soft-block discriminator for non-equivalent wash environments.
- Stop wash-count iteration when unexplained Kd drift appears; require causality attribution before continuing or scaling.
- Use species-first diagnostics when acid/base speciation, complexation, ion pairing, or reactive washing is plausible.
- Treat rag layer and emulsion as inventory-loss channels rather than mere separation inconvenience.
- Separate industrial workflow risk tags from mechanistic Kd drift explanations.

### Cross-snapshot alignment note

Some candidate terms (e.g. interfacial_inventory_loss_channel, rag_layer_third_phase)
may overlap conceptually with downstream_interface and loss_amplification_interface
introduced in ISOL-003. Alignment or consolidation should be considered after one
additional reuse across snapshots.


## Taxonomy Delta — CHG-002 and MIX-001

### Reused formal reasoning anchors

- control_authority_decay
- misallocated_control_authority

### Reused candidate terms

- scalability_failure
- lab_scale_masking
- structure_inheritance
- equipment_transfer_boundary

### New CHG-002 candidate terms introduced

#### nominal_vs_effective_dosing
A charging review pattern in which the nominal dosing profile no longer represents the actual time profile by which material enters and participates in the reaction mass.

#### phase_entry_failure
A charging-control failure in which the added material is delayed, isolated, phase-separated, or physically prevented from entering the effective reaction mass.

#### rate_matching_failure
A charging-control failure in which the effective material entry rate is mismatched with the reaction or heat-release consumption rate, leading to inventory accumulation.

#### hidden_unreacted_inventory
Unreacted material inventory that accumulates despite nominally controlled dosing, often becoming visible only after induction, delayed entry, or signal lag is overcome.

#### pre_dosing_state
The physical and spatial state of material before effective entry into the reaction mass, including entry location, local momentum, surface/subsurface introduction, and exchange environment.

#### dosing_inertia
Delay or continuation of effective material entry after a nominal control action, caused by line holdup, control delay, system inertia, or discretized dosing progression.

### New MIX-001 candidate terms introduced

#### mixing_time_scale_failure
A mixing-layer control failure in which the mixing time scale is slower than the characteristic reaction or physical-transformation time scale.

#### logical_lock_in
Irreversible loss of control authority caused by local reaction or phase history becoming established before global control variables become effective.

#### pre_homogenization_history_lock_in
A review pattern in which local reaction, concentration, or phase history becomes fixed before spatial homogenization is achieved.

#### secondary_mixing_manifestation
A boundary pattern in which mixing affects the timing or severity of a problem but is not the primary control-authority failure.

### Candidate risk signals introduced

- nominal dosing profile differs from effective material entry profile
- material forms floating or foaming layer before entering reaction mass
- phase transition or phase separation occurs near the dosing point
- solidification, precipitation, oiling-out, or stable emulsion occurs during dosing
- agglomeration or crust formation creates isolated solid micro-environments
- dosing entry point is located in low-momentum or low-exchange region
- reaction shows induction period or auto-accelerating behavior during dosing
- process signals lag behind true reaction progress
- line holdup, control delay, or discrete dosing events continue material entry after stop command
- unreacted inventory accumulates despite nominally controlled dosing
- local reaction history forms before spatial homogenization
- local phase history forms before spatial homogenization
- side reaction onset precedes completion of mixing
- extending reaction time fails to recover intended pathway
- extending reaction time amplifies side reactions
- reducing dosing rate fails to restore intended pathway
- modifying dosing structure fails to recover control authority
- interfacial reaction occurs before effective homogenization
- local concentration history becomes non-recoverable
- phenomenological mixing issue remains after CHG-002 dosing-rate explanation is eliminated

### Expert judgment patterns introduced

- Treat nominal dosing and effective dosing as separate review objects under scale-up conditions.
- Review phase-entry failure before assigning apparent charging failure to mixing or thermal control.
- Treat delayed entry, dosing inertia, and hidden unreacted inventory as charging-control decay rather than as downstream thermal rescue problems.
- Classify MIX-001 as positive only when local reaction or phase history forms before homogenization and cannot be recovered by time extension or dosing-structure adjustment.
- Treat mixing-related observations as secondary manifestations when the dominant control failure remains in CHG, phase behavior, crystallization, or thermal pathway selection.
- Do not convert charging, dosing, mixing, agitation, or thermal review into SOP-like operating recommendations.

### Cross-snapshot alignment note

CHG-002 and MIX-001 extend the taxonomy upstream from downstream consequence-stage review into early control-authority attribution. The new candidate terms remain non-formal until reuse is tested through THR-001, CHG-001, WRKUP-001, and follow-up robustness cases. `dosing_inertia` should be kept broader than line holdup alone. `secondary_mixing_manifestation` should be used as a false-positive guardrail rather than as a positive MIX-001 anchor.

## Taxonomy Delta — THR-001, CHG-001, and WRKUP-001

### Reused formal reasoning anchors

- control_authority_decay
- misallocated_control_authority

### Reused candidate terms

- lab_scale_masking
- scalability_failure

### New THR-001 candidate terms introduced

#### thermal_control_authority
A review pattern in which temperature functions as a source of control authority rather than merely as a rate-modulating or heat-removal parameter.

#### temperature_as_primary_authority
A condition where reaction pathway or stage dominance is determined primarily by temperature selection and cannot be equivalently recovered through CHG or MIX interventions.

#### competing_pathway_authority
A thermal-control pattern in which temperature allocates dominance among accessible parallel reaction pathways by changing their relative intrinsic rates.

#### stage_gating_authority
A thermal-control pattern in which temperature determines whether the system can cross an intermediate or reaction-stage boundary.

#### substitutable_control_authority
A boundary pattern in which thermal and charging controls can substitute for each other, preventing classification as a core THR-only authority case.

### New CHG-001 candidate terms introduced

#### charging_sequence_risk
A charging review pattern in which the order of material introduction creates structural scale-up risk before addition mode, mixing, or thermal control can function as effective safeguards.

#### effective_mixing_assumption
The assumption that added material enters the reaction mass and participates in bulk mixing within the charging time scale; if violated, CHG-001 sequence analysis is insufficient.

#### accumulation_then_trigger
A charging sequence in which most or all reactive inventory is accumulated before a later trigger such as heating, activation, or catalyst addition.

#### reactive_inventory_before_trigger
Reactive inventory present before the event that initiates or accelerates the reaction.

#### feed_rate_control_lost
Loss of feed-rate control as an active lever after the system has already accumulated reactive inventory and the reaction has been triggered.

#### strong_trigger_sequence
A subclass of accumulation-then-trigger sequence in which the trigger advances the reaction through substrate decomposition or highly reactive intermediate formation.

#### sliding_window_temperature_rise
Maximum net temperature increase over any continuous time window used as an empirical signal of hidden scale-up sensitivity.

### New WRKUP-001 candidate terms introduced

#### workup_as_termination_control
A workup review pattern in which workup functions as a reaction-termination control layer rather than a result-processing step.

#### reaction_end_state_not_final_state
A condition where the nominal reaction end state still contains reactive intermediates, metal complexes, reversible catalytic states, or species awaiting transformation.

#### quench_reaction_completion
Evidence that the quench reaction, rather than the mere addition of quench agent, has reached the chemically stable final state.

#### chemically_incomplete_quench
A failure mode in which quench agent has been added but the system retains chemical activity because the quench reaction is incomplete under the design conditions.

#### critical_quench_window
A reactive time window during early quench in which scale-up elongates exposure and shifts pathway dominance or side-reaction risk.

#### physically_inaccessible_quench
A failure mode in which quench reagent is nominally added but cannot actually enter the reaction phase due to freezing, phase separation, or interfacial isolation.

#### apparent_addition_not_participation
A review pattern in which apparent addition of a quench reagent is not accepted as evidence of actual chemical participation.

### Candidate risk signals introduced

- temperature change alters product composition or selectivity
- temperature change alters dominance between competing reaction pathways
- reaction stagnates or intermediate accumulates within a specific temperature window
- heating enables stage transition or reaction recovery
- temperature defines stage boundary rather than merely modulating rate
- thermal and charging controls are substitutable in a boundary case
- pre-charged material can react with subsequently formed product or intermediate
- solid is charged before liquid level, wetting, dispersion, or dissolution conditions are established
- most or all reactants are accumulated before reaction triggering
- reactive inventory exists before triggering
- feed rate as a control lever is lost after triggering
- generation rate may exceed heat-removal or venting capacity after triggering
- small-scale lack of temperature rise may be masked by high surface-area-to-volume ratio
- sliding-window temperature rise indicates scale-up sensitivity
- primary reaction has nominally stopped but reactive species remain
- reaction end state is not chemically stable final state
- stable final state requires a quench reaction
- quench agent added is treated as termination criterion
- quench reaction has non-negligible kinetic time scale
- reactive window exists from t = 0 until complete deactivation
- final pH is used as sole quench criterion
- quench reagent is physically inaccessible due to freezing, phase separation, or interfacial isolation
- apparent quench-agent addition does not imply actual participation

### Candidate quantitative or review-trigger family

- ΔT15,max >= 3 °C over any continuous 15-minute window: CHG-001 risk indication
- ΔT15,max >= 6 °C over any continuous 15-minute window: CHG-001 high-risk indication
- primary_thermal_authority_review_required: pathway or stage dominance is determined by temperature and cannot be equivalently recovered by CHG or MIX
- p3_review_required: most or all reactants are accumulated before heating, activation, or catalyst trigger
- p4_strong_trigger_review_required: trigger advances reaction through substrate decomposition or highly reactive intermediate formation
- workup_authority_review_required: primary reaction nominally stopped but reactive species remain and stable final state requires quench reaction
- physically_inaccessible_quench_review_required: quench reagent may be frozen, phase-separated, or interfacially isolated from reaction phase

### Expert judgment patterns introduced

- Treat temperature as primary control authority only when it determines pathway or stage dominance and cannot be equivalently recovered through CHG or MIX.
- Treat thermal anomalies caused by prior charging inventory accumulation or mixing time-scale failure as manifestations rather than THR-001 positive cases.
- Treat accumulation-then-trigger sequences as charging-sequence risk when reactive inventory exists before initiation and feed-rate control is lost after triggering.
- Treat sliding-window temperature rise as an empirical scale-up sensitivity signal, not a deterministic safety specification.
- Treat workup as termination control only when reactive species remain after nominal reaction stop and quench completion is required for chemical stability.
- Treat apparent quench-agent addition, final pH, physical removal, or downstream cleanup as insufficient evidence of quench completion unless chemical deactivation is demonstrated.
- Do not convert charging, thermal, or quench review criteria into SOP-like operational recommendations.

### Cross-snapshot alignment note

THR-001, CHG-001, and WRKUP-001 extend the upstream and termination-control side of the machine layer. The new terms remain candidate terms and should not be promoted to formal anchors until follow-up robustness tests confirm stable attribution boundaries among CHG-001, CHG-002, MIX-001, THR-001, and WRKUP-001.
## Taxonomy Delta — TLC Observation and Diagnostic Gates

### Scope

This delta introduces TLC gate-level review terms for observation validity, sampling representativeness, and interpretability authority. These terms support Machine Reviewer behavior before chemical interpretation is attempted. They should not be treated as TLC operating instructions or general analytical rules.

### Reused formal reasoning anchors

None.

### New candidate terms introduced

#### observation_validity_gate
A pre-interpretation review pattern that checks whether an observed analytical signal is admissible as evidence before it is used to infer reaction progress, conversion, impurity pattern, or intermediate survival.

#### sample_state_projection
A review pattern in which the analytical signal is treated as a projection of a source chemical state; if the sample transforms during preparation, handling, or observation, the projection no longer represents the original state.

#### representativeness_check
A sampling-validity review pattern that checks whether the micro-sample used for TLC represents the physical phase and composition of the full reaction system.

#### liquid_phase_only_projection
A boundary condition in which TLC reflects only the liquid-phase concentration of sampled material, not total conversion or total system composition, especially under dissolution, precipitation, adsorption, partitioning, or heterogeneous-system constraints.

#### interpretability_gate
A diagnostic review gate that determines whether a developed and visualized TLC plate has sufficient visual, chromatographic, and anchoring validity to enter chemical interpretation.

#### data_object_boundary
A review boundary in which the current developed and visualized TLC plate is treated as a distinct data object; re-staining, re-development, or changed visualization creates a new data input requiring re-evaluation.

#### interpretability_revoked
A TLC interpretability status in which physical, visual, chromatographic, or projection-axis failure invalidates downstream chemical interpretation.

#### interpretability_downgraded
A TLC interpretability status in which signal distortion or anchoring instability restricts the plate to limited qualitative interpretation and prohibits stronger inference.

#### logical_void_status
A TLC interpretability status in which missing protocol anchoring or logical reference failure nullifies the current plate data object for reaction interpretation.

### Candidate risk signals introduced

#### TLC-PRE-000 candidate risk signals
- sample may transform within the TLC exposure window
- sample half-life is shorter than sampling-to-development time scale
- sample is sensitive to silica gel surface acidity
- sample is sensitive to trace moisture or oxygen during TLC handling
- low-temperature sample undergoes rapid warming during spotting
- thermally unstable intermediate may transform during TLC preparation
- reaction continues on the TLC plate
- plate signal may not represent the original chemical state

#### TLC-PRE-001 candidate risk signals
- heterogeneous reaction system sampled as a single mixed spot
- solid-liquid or liquid-liquid phases are not sampled separately
- mixed sampling under high-speed stirring is treated as representative
- starting material reacts while simultaneously dissolving
- product precipitates during the reaction
- product or intermediate partitions into another phase
- target component adsorbs onto catalyst or inorganic support
- liquid-phase TLC signal is treated as total conversion evidence
- sampling bias may create directional error in composition ratio

#### TLC-DIAG-001 candidate risk signals
- visual contrast is too low to extract clear spot contours
- background noise obscures the effective plate area
- starting material reference does not form repeatable migration
- starting material remains near the origin without a usable projection
- critical spots fall into low-Rf or high-Rf information compression zones
- no distinguishable structure exists in the effective projection interval
- banding, streaking, or global shifting indicates chromatographic failure
- co-spot reference is missing in reaction monitoring
- sample signal cannot be anchored or calibrated
- low-Rf tailing limits morphology-based interpretation
- co-spot anchoring deviation limits interpretability

### TLC-specific review trigger family

These triggers are TLC-specific evidence-admissibility or interpretability triggers. They are not global analytical rules and should not be generalized outside TLC diagnostic review without source support.

#### TLC-PRE-000 triggers
- TLC exposure window: 30-60 seconds from sampling and spotting to development chamber
- fast-evolving system: chemical transformation half-life significantly shorter than TLC handling window
- TLC surface environment: silica gel surface, mildly acidic silanol groups, trace moisture, oxygen
- thermal jump context: low-temperature reaction sample rapidly warms to room temperature

#### TLC-PRE-001 triggers
- heterogeneous system: solid-liquid or liquid-liquid system
- mixed sampling risk: high-speed stirred mixed sampling used as a composition proxy
- solubility equilibrium constraint: starting material dissolves while reacting
- product precipitation: product reaches saturation and precipitates during reaction
- surface adsorption: component adsorbs on catalyst or inorganic support
- qualitative-only record: TLC result should not be used for quantitative conversion judgment under heterogeneity constraints

#### TLC-DIAG-001 triggers
- background noise area: >30% effective plate area covered by background noise
- origin projection failure: starting material reference remains near Rf approximately 0
- projection-axis compression: critical spots fall below Rf 0.2 or above Rf 0.8 without distinguishable structure in Rf 0.2-0.7
- tail extension threshold: tail extension along migration direction exceeds 0.2 Rf units
- co-spot anchoring deviation:
  - PASS: |Delta Rf| < 0.05
  - CAUTION: 0.05 <= |Delta Rf| < 0.1
  - DOWNGRADED: 0.1 <= |Delta Rf| < 0.2
  - REVOKED: |Delta Rf| >= 0.2

### Expert judgment patterns introduced

- Treat TLC as an admissible diagnostic projection only after sample stability in the TLC environment is established.
- Treat sampling representativeness as a precondition for using TLC as reaction-system evidence.
- Treat heterogeneous-system TLC as phase-specific evidence unless physical and proportional representativeness is established.
- Do not treat liquid-phase TLC signals as total conversion evidence when dissolution, precipitation, adsorption, partitioning, or heterogeneous-system bias is present.
- Treat the developed TLC plate as a visual data object before treating it as chemical evidence.
- Establish interpretability before assigning reaction conversion, impurity, or mechanism meaning.
- Distinguish PASS, DOWNGRADED, REVOKED, and VOID interpretability states.
- Treat CAUTION as a sub-state of DOWNGRADED, not as an independent final status.
- Do not convert TLC-specific review triggers into global analytical rules.
- Do not convert TLC gate review into TLC operating SOP recommendations.

### Cross-snapshot alignment note

TLC-PRE-000, TLC-PRE-001, and TLC-DIAG-001 introduce an observation-layer gate sequence before chemical interpretation. These terms should be monitored for reuse in later TLC diagnostic-pathway and diagnostic-example annotations. Example-level terms from future TLC cases should not be promoted into taxonomy unless they reuse or clarify this gate-level structure.

### Additional candidate terms introduced by TLC-DIAG-002

#### permitted_interpretation_pathway
A TLC diagnostic review pattern that defines the permitted inference space after interpretability has been established.

#### presence_absence_inference
A limited TLC interpretation pathway that judges whether a known substance is present or absent based on anchored signal appearance at an expected position.

#### identity_consistency_check
A TLC interpretation pathway that checks whether a sample signal is physically consistent with a known reference through Rf anchoring and multi-mode visualization behavior.

#### qualitative_trend_monitoring
A TLC interpretation pathway that monitors empirical process trends such as gradual starting-material weakening, product strengthening, or impurity evolution without claiming precise kinetics.

#### prohibited_quantitative_conversion
A negative interpretation rule that blocks precise conversion percentages, kinetic parameters, or complete-conversion claims based on TLC alone.

#### intensity_content_non_equivalence
A negative interpretation rule that blocks direct equivalence between UV intensity, iodine depth, chemical stain vividness, and molar content or purity.

#### co_elution_uncertainty
An uncertainty state in which multiple chemical entities may overlap at the same Rf position, especially when visualization responses diverge across UV, iodine, or chemical stains.

### Candidate risk signals introduced by TLC-DIAG-002

- TLC plate enters interpretation despite REVOKED or VOID status
- DOWNGRADED plate is used for unrestricted chemical interpretation
- single staining or observation method is used to conclude single component status
- co-elution risk is ignored when different visualization methods diverge
- staining intensity is treated as molar content or purity
- relative migration order is treated as intrinsic compound strength
- spot area is compared across different Rf regions as content evidence
- disappearance of starting material spot is treated as complete chemical conversion
- TLC is used to output precise conversion percentage or kinetic parameters
- TLC signal is used to infer specific functional group details or complete structure

### TLC-DIAG-002 specific review triggers

- mandatory_precondition: only plates that passed TLC-DIAG-001 may enter TLC-DIAG-002
- revoked_or_void_block: REVOKED or VOID status prohibits interpretation
- downgraded_limited_use: DOWNGRADED status permits only explicitly limited-use pathways
- multi_visualization_check: UV, iodine, and at least one general or specific chemical stain may support presence/absence or identity consistency
- co_elution_warning: same Rf position with divergent visualization response indicates possible overlap
- local_area_content_condition: area-content relation is only rough and local when Rf values are identical or very close
- trend_reliability_window: TLC trend interpretation is relatively more reliable in early-to-mid reaction range and weaker late in reaction

### Additional expert judgment patterns introduced by TLC-DIAG-002

- Treat interpretability status as a mandatory precondition before pathway selection.
- Use TLC primarily for presence/absence, identity consistency, and qualitative or semi-quantitative trend monitoring.
- Treat co-elution as an uncertainty state when visualization methods diverge at the same Rf position.
- Do not equate staining intensity, UV response, iodine depth, or chemical stain vividness with molar content or purity.
- Do not treat disappearance of a starting-material spot as proof of complete chemical conversion.
- Do not use TLC to output precise conversion percentages, kinetic constants, or definitive structural assignments.
### Additional candidate terms introduced by TLC-PRE-002, TLC-003, and TLC-004

#### sample_preparation_gate
A TLC evidence-admissibility gate that determines whether quench, dilution, solvent adjustment, or matrix adjustment is required before spotting.

#### quench_requirement_check
A review pattern that checks whether a sample must be chemically quenched before TLC because ongoing reaction or reactive intermediates would otherwise alter the sampled state.

#### dilution_requirement_check
A review pattern that checks whether concentration, suspension, overload, or uncontrolled spot diameter invalidates direct spotting as a diagnostic input.

#### matrix_compatibility_check
A review pattern that checks whether solvent, water, acid, base, or other system matrix components distort migration behavior.

#### migration_distortion_control
A TLC review pattern that treats Rf shift, spot diffusion, severe tailing, or uncontrolled migration behavior as evidence-admissibility concerns before interpretation.

#### projection_axis_validity
A review pattern that checks whether the eluent system creates a usable information projection axis for TLC interpretation.

#### information_projection_axis
A TLC concept in which the eluent projects chemical differences onto the plate coordinate system in a way that may or may not be interpretable.

#### projection_axis_compression
A condition in which information is compressed near the baseline or solvent front, making component count, polarity order, or conversion inference unreliable.

#### rf_regular_projection
A condition where eluent ratio and Rf behavior maintain a stable and interpretable relationship under normal spot morphology.

#### surface_interaction_decoupling
A TLC review pattern in which acid or base modification is used only to reduce plate-surface interaction distortion, not to prove sample structure.

#### non_inferable_zone
A TLC projection region where baseline proximity, solvent-front proximity, severe tailing, phase instability, or compression prevents reliable inference.

#### visual_data_object_generation
A review pattern in which a developed TLC plate becomes an interpretable visual data object only after valid visualization, marking, and documentation.

#### visualization_validity
A review pattern that checks whether visualization mode, contrast, staining behavior, and background condition allow meaningful observation.

#### information_revealing_order
The irreversible sequence by which TLC visual information should be revealed and recorded, including solvent-front marking, drying, UV observation, iodine staining, and optional secondary staining.

#### solvent_front_marker_integrity
A visual-data-object requirement that the solvent front or equivalent projection marker must be preserved for Rf-based interpretation.

#### temporal_visual_validity
A review pattern that checks whether visual evidence is documented within the time window before staining fades, background oxidizes, or signal changes.

#### pre_diagnostic_visual_failure
A visual-layer failure that blocks diagnostic interpretation before chemical meaning is assigned.

### Candidate risk signals introduced by TLC-PRE-002

- sample undergoes non-negligible chemical change during TLC preparation window
- unquenched fast reaction is spotted directly
- highly reactive intermediate remains active during sampling or spotting
- sample is highly sensitive to trace moisture, protons, or room-temperature transition
- unquenched TLC result reflects stochastic transformation after spotting
- reaction concentration exceeds TLC working concentration window
- high concentration causes suspension, overload, or uncontrolled spot diameter
- in-situ quench is used beyond its concentration applicability boundary
- high-boiling or highly polar solvent distorts migration behavior
- free water, strong acid, or strong base distorts Rf or spot morphology
- pre-processing introduces precipitation or new reaction

### Candidate risk signals introduced by TLC-003

- eluent system fails to project components into effective Rf range
- all critical spots remain near the baseline
- all critical spots run near the solvent front
- Rf ratio correlation is used despite abnormal spot shape
- spot tailing or strong surface adsorption invalidates polarity inference
- aqueous or highly polar eluent mixture becomes phase-separated
- organic versus inorganic discrimination axis is used for fine organic separation
- eluent acid or base modification is treated as substantive sample chemistry
- severe tailing remains without surface-interaction decoupling
- projection-axis failure is used for conversion or mechanism inference

### Candidate risk signals introduced by TLC-004

- developed plate is interpreted before visual object validity is established
- solvent front is not marked or physical projection marker is missing
- image documentation occurs outside the information stability window
- iodine staining fades before documentation
- staining agent covers the background and masks migration morphology
- no clear structure is visible under UV or staining
- same migration structure shifts position across visualization modes
- secondary staining is treated as direct structural confirmation
- visual contrast is insufficient to distinguish spots, tailing, and background
- loss of physical markers causes projection-axis failure

### TLC-specific review trigger additions

#### TLC-PRE-002 triggers
- preparation_time_window: sampling to spotting to development typically takes 30-60 seconds
- working_concentration_window: 0.1-0.5 M as TLC working concentration window
- high_concentration_trigger: reaction concentration >= 0.5 M or uncontrolled spot diameter / suspension / overload
- matrix_distortion_context: DMSO, DMF, NMP, free water, strong acid, or strong base may distort Rf, diffusion, or tailing

#### TLC-003 triggers
- effective_rf_range: prioritize interpretable information between Rf 0.2 and 0.7
- baseline_compression: critical spots remain below Rf 0.2
- front_compression: critical spots run above Rf 0.8
- dcm_meoh_water_reference_window: DCM / MeOH / H2O = 3 / 2 / 0.5 as TLC-specific homogeneous-window reference

#### TLC-004 triggers
- visualization_sequence: solvent-front marking and drying, then UV 254/365, iodine staining, and secondary chemical staining
- information_stability_window: image documentation typically within 0-5 minutes after staining
- marker_integrity: solvent front must be clearly marked for Rf projection
- pre_diagnostic_failure: no visible structure, total background coverage, or loss of projection marker blocks diagnostic interpretation

### Additional expert judgment patterns introduced

- Treat sample preparation as a precondition for TLC evidence admissibility, not as a downstream interpretation step.
- Treat quench, dilution, and matrix adjustment as controls over chemical-state preservation and migration-state validity.
- Treat eluent selection as projection-axis selection before using Rf values for inference.
- Treat baseline compression, front compression, phase instability, and unresolved surface interaction as projection-axis failures.
- Treat visualization as generation of a visual data object before chemical interpretation.
- Treat missing solvent front or missing physical marker as projection-axis failure.
- Keep causal explanation under the diagnostic layer rather than the visual observation layer.
- Do not convert TLC-specific time, concentration, Rf, solvent-ratio, or visualization-window triggers into global analytical rules.
- Do not convert TLC sample preparation, eluent selection, or visualization review into TLC operating SOP recommendations.
### Additional candidate terms introduced by TLC-000 and TLC-001

#### coordinate_baseline_integrity
A TLC coordinate-system review pattern that checks whether the physical origin line provides a valid baseline for Rf calculation and cross-lane comparison.

#### origin_line_validity
A TLC review pattern that checks whether the origin line height, marking, and sample placement preserve a valid starting coordinate.

#### rf_coordinate_validity
A review pattern that checks whether Rf values can be interpreted from a valid physical baseline and solvent-front coordinate system.

#### cross_lane_comparison_validity
A review pattern that checks whether multiple lanes share a valid geometric basis for comparison.

#### centroid_localization_validity
A machine-vision-oriented review pattern that checks whether initial spot geometry supports reliable spot localization.

#### physical_marker_noninterference
A TLC review pattern that checks whether physical marking avoids silica disruption or chemical interference.

#### reference_layout_validity
A TLC protocol review pattern that checks whether lane layout contains sufficient reference, sample, co-spot, and optional standard information for interpretation.

#### relative_coordinate_system
A TLC layout concept in which lane positions and reference signals create a comparative coordinate system for interpretation.

#### co_spot_anchoring
A TLC reference strategy in which a mixed reference/sample lane is used to anchor identity and distinguish matrix-induced Rf shift from chemical difference.

#### matrix_shift_compensation
A review pattern that checks whether pH, salts, byproducts, or reaction-matrix effects may shift Rf without changing chemical identity.

#### lane_geometry_validity
A TLC layout review pattern that checks whether lane spacing, spot overlap, and edge margin preserve interpretable lane geometry.

#### edge_effect_control
A TLC layout review pattern that checks whether edge proximity or smiling effects may distort outer-lane migration.

### Candidate risk signals introduced by TLC-000

- sample spot is submerged by mobile phase
- origin line does not provide a uniform starting Y-coordinate
- vertical deviation between spot centers creates artificial Rf error
- origin mark disrupts silica capillary behavior
- ink or chemically interfering marker is used on the plate
- initial spot diameter is too large for reliable centroid localization
- cross-lane comparison is performed despite invalid origin-line geometry
- Rf values are calculated from lanes with invalid physical baseline

### Candidate risk signals introduced by TLC-001

- TLC plate lacks a starting-material reference lane
- reaction sample is interpreted without co-spot anchoring when matrix shift is possible
- sample lane Rf shift is interpreted as chemical change without spike comparison
- spike lane splits into two spots or elongated double-spot morphology
- product or impurity standard is missing when target position anchoring is required
- lane spacing is too narrow and causes overlap
- outer lanes are too close to plate edge and affected by edge distortion
- matrix effect is ignored during identity consistency judgment
- intensity or area ratio is used for precise conversion inference

### TLC-specific review trigger additions

#### TLC-000 triggers
- origin_line_reference_height: typically 1.0 cm from plate bottom
- lane_invalid_if_submerged: sample spot submerged by mobile phase invalidates the lane
- vertical_alignment_tolerance: spot-center vertical deviation should be controlled within 2.0 mm
- initial_spot_diameter_reference: initial spot diameter ideally 0.5-1.5 mm
- marker_constraint: use light pencil marking; avoid scoring silica or using ink

#### TLC-001 triggers
- standard_lane_set: Ref / Spike / Sample / Product-or-impurity-standard
- lane_spacing_reference: recommended pitch 3-6 mm
- edge_margin_reference: outermost spots should be at least 5 mm from plate edge
- spike_single_spot_logic: single cohesive spike spot supports matrix-shift explanation
- spike_split_logic: two distinct spots or elongated double-spot shape indicates different entities
- conversion_inference_boundary: intensity/area ratio can support only rough trend or relative estimate, not precise conversion

### Additional expert judgment patterns introduced

- Treat the origin line as the physical coordinate baseline before Rf calculation.
- Treat submerged spots, origin-line misalignment, or marker interference as coordinate-system validity failures.
- Treat TLC layout as a reference and anchoring system before interpreting spot identity.
- Use co-spot behavior to distinguish matrix-induced displacement from chemical identity difference.
- Treat lane overlap and edge effects as layout-level threats to interpretation.
- Do not convert TLC-specific geometric values into global analytical rules.
- Do not convert lane intensity or area ratio into precise conversion percentage.
## Taxonomy Delta — Derived Quench Gate and TLC Meta Diagnostic Authority

### Scope

This delta adds one derived quench rejection gate and two TLC meta-level diagnostic authority entries. The quench checklist is derived from WRKUP-001 and introduces no new process knowledge. The TLC meta entries define methodological boundaries for early diagnostic value, late-stage downgrading, decision latency, and multi-level feedback architecture.

### Candidate terms introduced

#### rejection_checklist_gate
A derived machine-review gate that produces PASS / REJECT decisions without providing optimization, remediation, or operating instructions.

#### diagnostic_value_boundary
A meta-level review boundary that defines when a diagnostic tool has authority and when that authority should be downgraded or terminated.

#### early_stage_diagnostic_authority
A TLC meta-level authority state in which early or mid-stage reaction exploration benefits from rapid visual trend and anomaly detection.

#### late_stage_interpretability_downgrade
A TLC meta-level boundary where late-stage confirmation, trace impurity control, or regulatory evidence exceeds the reliable authority of TLC.

#### total_sample_projection
A TLC methodological concept in which the full applied sample remains spatially represented on the plate, including material that stays at the origin.

#### discovery_first_logic
A diagnostic strategy in which the first goal is to detect what may be present in an incompletely known system before precise quantification is attempted.

#### pseudo_completion_risk
A late-stage TLC risk where disappearance of a starting-material spot indicates falling below visualization limit rather than true chemical completion.

#### resolution_scale_mismatch
A mismatch between the resolution scale of TLC and the problem scale, especially for trace impurities or final-state confirmation.

#### decision_latency_match
A review pattern that checks whether the feedback speed of an analytical tool matches the decision window of the reaction system.

#### high_frequency_low_latency_feedback
A feedback architecture role in which TLC provides rapid, low-resolution situational awareness.

#### multi_level_feedback_strategy
A monitoring architecture that combines high-frequency low-gain feedback with low-frequency high-gain precision analysis.

#### temporal_aliasing_risk
A risk that important transient states are missed because the analytical feedback cycle is slower than the process state-transition cycle.

#### situational_awareness_branch
A diagnostic branch that provides fast awareness of process-state deviations without claiming final quantitative authority.

#### precision_confirmation_branch
A low-frequency, high-resolution analytical branch used for confirmation, quantification, and compliance calibration.

#### fuzzy_anomaly_detection
A TLC meta-level concept describing rapid recognition of unstructured visual anomalies that may not correspond to predefined analytical peaks.

#### decision_safety_margin
The time or informational margin gained by rapid diagnostic feedback before slower precision analysis returns.

### Candidate risk signals introduced

#### WRKUP-001-QUENCH-CHECKLIST signals
- reactive species remain at nominal reaction end
- quench is not explicitly designed as a completable chemical reaction
- quench completion is defined by reagent addition rather than chemical deactivation
- quench completion is defined by operational completion rather than stable final state
- reactive window exists between quench start and complete deactivation
- scale-up elongates the reactive quench window
- final pH is used as sole evidence of quench success
- final analytical result is used without excluding early reactive window
- quench reagent may be physically inaccessible under scale-up conditions
- physical accessibility relies on rapid dumping or ideal mixing assumptions

#### TLC-META-001 signals
- TLC is treated as a precision measurement tool
- TLC is used as primary late-stage confirmation evidence
- disappearance of starting material spot is treated as complete conversion
- trace impurity judgment is based primarily on TLC
- staining behavior near detection limit is treated as linear concentration evidence
- TLC is used for regulatory or final-state confirmation after problem scale becomes trace-level
- early diagnostic signal is overextended into late-stage confirmation authority
- multi-channel visualization divergence is ignored during identity assessment

#### TLC-META-002 signals
- precision analysis feedback cycle is slower than reaction state transition
- system relies only on low-frequency high-precision analysis during dynamic stage
- transient abnormal states may be missed due to decision latency
- high-resolution formal analysis is treated as sufficient despite temporal aliasing risk
- TLC high-frequency branch is removed before process state is stable
- unstructured visual anomalies are ignored because they are not predefined analytical peaks
- TLC is incorrectly treated as a replacement for confirmatory precision analysis
- high-frequency situational awareness is confused with release or compliance evidence

### Expert judgment patterns introduced

- Treat WRKUP-001 quench checklist as a rejection gate only, not as a remediation guide.
- Reject downstream progression when quench completion, reactive-window control, or physical accessibility is not established.
- Preserve TLC diagnostic authority for early discovery, trend perception, and anomaly warning.
- Downgrade TLC authority for late-stage confirmation, trace impurity quantification, precise conversion, or regulatory evidence.
- Treat starting-material spot disappearance as possible pseudo-completion rather than proof of chemical completion.
- Treat TLC as a high-frequency, low-latency situational-awareness branch, not as a replacement for precision analysis.
- Treat temporal aliasing as a review risk when analytical feedback is slower than process state transition.
- Keep compliance release, final quantification, and structural confirmation under validated precision analytical methods.