# Machine Change Log

## 2026-05-05

Initialized machine annotation baseline with two chapter-level samples.

- Added ISOL-001-CRYSTALLIZATION as baseline for risk detection before solid-state commitment.
- Added ISOL-002-RECRYSTALLIZATION as baseline for selectivity failure, limited control regain, and misallocated control authority.
- Initialized minimum taxonomy with formal reasoning anchors derived from crystallization and recrystallization.
- Added first two JSONL entries to openchemprocess_index.jsonl.md as the Obsidian-maintained source.
- Registered both snapshots as completed in annotation_registry.md.

Schema used: risk_annotation_schema_v0.2

## 2026-05-05

Performed first minimal machine-review test using ISOL-002 baseline annotation.

Test question:
A recrystallization requires three cycles and total recovery is below 70%. How should this be reviewed?

Result:
The model correctly matched ISOL-002-RECRYSTALLIZATION, identified repeated recrystallization and recovery <70% as compensatory-use / structurally weak signals, used reasoning anchors including limited_control_regain, selective_repartitioning, constrained_solubility_space, misallocated_control_authority, and recovery_constraint, and preserved uncertainty instead of giving deterministic operating instructions.

Assessment:
First baseline machine-review test passed.

Follow-up:
Consider adding Recovery_loss_flag or cumulative_recovery_loss >15% explicitly to the ISOL-002 JSONL entry if this trigger is expected to be machine-retrievable from the index layer alone.

## 2026-05-05

Performed second minimal machine-review test using ISOL-001 baseline annotation.

Test question:
During primary crystallization, crude-product solubility is about three times higher than pure-product solubility in the same solvent system. How should this be reviewed?

Result:
The model correctly matched ISOL-001-CRYSTALLIZATION, identified crude_solubility_ratio > 2 as the primary risk signal, used reasoning anchors including usable_solubility_gap, residual_modifier_effect, control_authority_decay, and solid_state_commitment, and concluded that the elevated crude solubility should be reviewed as crude-system solubility distortion rather than as evidence that the intrinsic solvent system is unsuitable.

Assessment:
Second baseline machine-review test passed. ISOL-001 and ISOL-002 now jointly validate the first minimal machine-review loop.

## 2026-05-05

Added WRKUP-003-SOLVENT-REMOVAL-DRIVEN-ACCUMULATION-AND-THERMAL-EXPOSURE-CONTROL machine annotation.

### Change type
machine_annotation_added

### Canonical snapshot
WRKUP-003-SOLVENT-REMOVAL-DRIVEN-ACCUMULATION-AND-THERMAL-EXPOSURE-CONTROL

### Taxonomy impact
- Reused existing formal anchors: control_authority_decay, misallocated_control_authority.
- Added WRKUP-003 terms as candidate terms, not formal anchors: forced_composition_path, nonvolatile_accumulation, composition_evolution_path, volatile_removal_trajectory, thermal_exposure_accumulation, early_solvent_exchange, equipment_transfer_boundary, upstream_solvent_selection_coupling, route_priority_review.
- Added candidate quantitative trigger family for CF-driven concentration review, including CF > 3, CF > 5, and CF > 10 review thresholds.

### Notes
CF thresholds remain engineering guidelines rather than universal deterministic rules. Missing fields should trigger review unless a defined hard-gate condition is met. Candidate terms should be reconsidered for formal promotion only after reuse in later snapshots such as ISOL-003, ISOL-004, or WRKUP-002.

## 2026-05-05

Added ISOL-003-FILTRATION machine annotation.

### Change type
machine_annotation_added

### Canonical snapshot
ISOL-003-FILTRATION

### Files affected
- 01_process/Isolation/isol_003_filtration.en.md
- 01_process/Isolation/isol_003_filtration.zh.md
- 03_machine/openchemprocess_index.jsonl.md
- 03_machine/minimum_risk_taxonomy.md
- 03_machine/annotation_registry.md
- 03_machine/machine_change_log.md

### Rationale
ISOL-003 introduces the first machine-review pattern for filtration as a consequence-stage separation after solid-state commitment. The annotation adds review logic for WMR, mother-liquor retention, inherited solid-structure failure, lab-scale masking, washing displacement failure, and path-level filtration non-scalability.

### Taxonomy impact
- Reused existing formal anchors: control_authority_decay, solid_state_commitment, misallocated_control_authority, mother_liquor_retention.
- Reused existing candidate terms: downstream_filtration_compatibility, downstream_interface.
- Added ISOL-003 terms as candidate terms, not formal anchors: consequence_stage_separation, loss_amplification_interface, structure_inheritance, upstream_failure_exposure, lab_scale_masking, scalability_failure, wet_mass_ratio, washing_displacement_efficiency, compensatory_filtration.
- Added candidate quantitative trigger family for WMR-driven filtration review, including WMR <1.2, 1.2-1.5, >=2, and >=3 thresholds.

### Notes
WMR thresholds are review triggers rather than deterministic rejection rules. Filtration equipment or path changes may be valid outcome management, but they should not be interpreted as recovery of upstream composition or solid-formation control authority. Candidate terms should be reconsidered for formal promotion after reuse in ISOL-004 drying, WRKUP-003 solvent exchange, or future solid-handling snapshots.

## 2026-05-05

Added ISOL-004-DRYING machine annotation.

### Change type
machine_annotation_added

### Canonical snapshot
ISOL-004-DRYING

### Files affected
- 01_process/Isolation/isol_004_drying.en.md
- 01_process/Isolation/isol_004_drying.zh.md
- 03_machine/openchemprocess_index.jsonl.md
- 03_machine/minimum_risk_taxonomy.md
- 03_machine/annotation_registry.md
- 03_machine/machine_change_log.md

### Rationale
ISOL-004 introduces the first machine-review pattern for drying as final solvent-state and solvent-location lock-in after filtration. The annotation adds review logic for surface composition drift, surface-driven balling, pore-bound solvent retention, bound-solvent plateau, static versus rolling scale masking, and drying-stage compensation boundaries.

### Taxonomy impact
- Reused existing formal anchors: control_authority_decay, solid_state_commitment, misallocated_control_authority.
- Reused existing candidate terms from ISOL-003: consequence_stage_separation, structure_inheritance, upstream_failure_exposure, lab_scale_masking, scalability_failure.
- Added ISOL-004 terms as candidate terms, not formal anchors: drying_state_lock_in, solvent_state_location_lock_in, surface_composition_drift, surface_good_solvent_enrichment, surface_redissolution, rolling_agglomeration, pore_bound_solvent_retention, bound_solvent_state, drying_plateau, static_predrying, solvent_displacement, drying_compensation_boundary.
- Added candidate flag trigger family for drying review, including surface_good_solvent_state, surface_composition_drift, morphology_tag, is_salt_form, solvent_hbond_capability, plateau_check, static_drying_ratio, rolling_equipment_present, and process_relies_only_on_vacuum_temperature_time.

### Formalization watchlist
The repeated use of consequence_stage_separation, structure_inheritance, upstream_failure_exposure, lab_scale_masking, and scalability_failure across ISOL-003 and ISOL-004 suggests these terms may become formal reasoning anchors after one more downstream or solid-handling snapshot confirms reuse.

### Notes
Drying-stage interventions such as static pre-drying, pre-wash, or solvent displacement may be valid compensatory controls, but they should not be interpreted as recovery of upstream solid-state or composition control authority. Extended vacuum time alone should not be treated as sufficient for bound-solvent or pore-retention plateau behavior.

## 2026-05-05

Added WRKUP-002-PARTITION-RATIO-DRIFT-INVENTORY-CONTROL machine annotation.

### Change type
machine_annotation_added

### Canonical snapshot
WRKUP-002-PARTITION-RATIO-DRIFT-INVENTORY-CONTROL

### Files affected
- 01_process/Workup/wrkup_002_partition_ratio_drift_inventory_control.en.md
- 01_process/Workup/wrkup_002_partition_ratio_drift_inventory_control.zh.md
- 03_machine/openchemprocess_index.jsonl.md
- 03_machine/minimum_risk_taxonomy.md
- 03_machine/annotation_registry.md
- 03_machine/machine_change_log.md

### Rationale
WRKUP-002 introduces the first machine-review pattern for extraction and washing as inventory redistribution rather than repeatable wash-count operation. The annotation adds review logic for Delta Kd(1->2), species-first attribution, phase-environment drift, interfacial inventory audit, recycled-solvent loading drift, concentration-dependent Kd, reactive wash drift, and industrial workflow risk tags.

### Taxonomy impact
- Reused existing formal anchors: control_authority_decay, misallocated_control_authority.
- Added WRKUP-002 terms as candidate terms, not formal anchors: inventory_redistribution, partition_ratio_drift, kd_consistency_check, phase_environment_drift, chemical_speciation_drift, species_first_diagnostic_order, wash_count_iteration, interfacial_inventory_loss_channel, rag_layer_third_phase, emulsion_inventory_audit, recycled_solvent_loading_drift, temperature_partition_window, concentration_dependent_partitioning, reaction_partition_coupling, industrial_workflow_risk_tag, carryover_inventory.
- Added candidate quantitative trigger family for Kd-driven workup review, including Delta Kd(1->2) >15%, species-first Kd_ref vs Kd_in_situ >15%, recycled-solvent Kd shift >15%, phase disengagement-time escalation, and rag-layer/emulsion inventory-audit triggers.

### Formalization watchlist
The terms phase_environment_drift, chemical_speciation_drift, inventory_redistribution, and interfacial_inventory_loss_channel may become formal reasoning anchors if reused in WRKUP-003 concentration, downstream isolation/drying, or future extraction-related snapshots.

### Notes
Delta Kd thresholds are review triggers rather than deterministic rejection rules. Window switching, temperature-window design, reactive washing, and recycled-solvent use may be valid if explicitly measured and attributed. Industrial workflow risk tags should remain separate from mechanistic Kd drift explanations.

## 2026-05-10

Completed first 12-case machine-review robustness baseline.

### Change type
qa_baseline_completed_and_prompt_patch_required

### Scope
- Reviewed OCP-MR-001 through OCP-MR-012 against the current six chapter-level machine annotations: ISOL-001, ISOL-002, WRKUP-002, WRKUP-003, ISOL-003, and ISOL-004.
- Recorded results in `machine_review_test_results_v0.1.md`.
- Identified prompt-level and QA-checklist-level issues without changing taxonomy, JSONL, schema, or source snapshots.

### Assessment
The first robustness cycle broadly passed. The machine layer can identify the intended review domain, reject several false positives, avoid deterministic threshold misuse, and preserve the Machine Reviewer frame without giving SOP-like recommendations.

### Issues exposed
- Review-domain snapshot matching was sometimes conflated with risk-positive conclusion.
- Matched risk signals, inferred or partially supported signals, and reasoning anchors were sometimes over-included or placed in the wrong section.
- Some allowed canonical anchors were listed as positive anchors even when they were only conceptually related or boundary-adjacent.
- In reviewer-output audit cases, nearest canonical replacements were sometimes treated like positively supported reasoning anchors despite missing underlying process evidence.

### Patch decision
- Patch `machine_review_test_prompt_v0.1.md` to explicitly separate review-domain match, risk-positive conclusion, matched risk signals, inferred / partially supported signals, positive reasoning anchors, and canonical correction / nearest allowed terms.
- Patch `machine_review_test_cases_v0.1.md` only where expected wording could confuse review-domain matching with positive risk finding.
- Patch `machine_layer_integrity_checklist.md` to prevent QA-output terms, inferred signals, and nearest canonical replacements from contaminating JSONL or taxonomy.
- No taxonomy, JSONL, schema, or source snapshot change is required from this robustness cycle.

### Notes
This checkpoint supports continued annotation expansion, but only after the QA files are stabilized. Candidate terms should still require source-snapshot support and change-log documentation before entering taxonomy delta.

## 2026-05-10

Added CHG-002-ADDITION-MODE-AND-RATE and MIX-001-MIXING-TIME-SCALE-FAILURE machine annotations.

### Change type

machine_annotation_added

### Canonical snapshots

- CHG-002-ADDITION-MODE-AND-RATE
- MIX-001-MIXING-TIME-SCALE-FAILURE

### Files affected

- 01_process/charging/chg_002_addition_mode_and_rate.en.md
- 01_process/charging/chg_002_addition_mode_and_rate.zh.md
- 01_process/Mixing/mix_001_mixing_time_scale_failure.en.md
- 01_process/Mixing/mix_001_mixing_time_scale_failure.zh.md
- 03_machine/openchemprocess_index.jsonl.md
- 03_machine/minimum_risk_taxonomy.md
- 03_machine/annotation_registry.md
- 03_machine/machine_change_log.md

### Rationale

CHG-002 extends the machine layer upstream by defining when nominal dosing no longer functions as effective dosing. The annotation introduces review logic for phase-entry failure, rate-matching failure, delayed material entry, dosing inertia, detection lag, and hidden unreacted inventory as mechanisms of charging-control decay.

MIX-001 extends the machine layer by defining when mixing time scale becomes a primary control precondition rather than a secondary manifestation. The annotation introduces review logic for local reaction or phase history before homogenization, logical lock-in, and attribution tests based on whether time extension or dosing-structure adjustment can restore control authority.

### Taxonomy impact

- Reused existing formal anchors: control_authority_decay, misallocated_control_authority.
- Reused existing candidate terms: scalability_failure, lab_scale_masking, structure_inheritance, equipment_transfer_boundary.
- Added CHG-002 candidate terms: nominal_vs_effective_dosing, phase_entry_failure, rate_matching_failure, hidden_unreacted_inventory, pre_dosing_state, dosing_inertia.
- Added MIX-001 candidate terms: mixing_time_scale_failure, logical_lock_in, pre_homogenization_history_lock_in, secondary_mixing_manifestation.

### Notes

These candidate terms should not be promoted to formal reasoning anchors until cross-snapshot reuse is tested through THR-001, CHG-001, WRKUP-001, and follow-up robustness cases. Diagnostic observations such as failed recovery by time extension or failed recovery by dosing adjustment remain risk-signal evidence, not candidate anchors. The annotations are written for Machine Reviewer behavior only and should not be interpreted as dosing, agitation, equipment, or thermal operating recommendations.

## 2026-05-10

Added THR-001-THERMAL-CONTROL-AUTHORITY, CHG-001-CHARGING-SEQUENCE, and WRKUP-001-WORKUP-CONTROL-AUTHORITY machine annotations.

### Change type
machine_annotation_added

### Canonical snapshots
- THR-001-THERMAL-CONTROL-AUTHORITY
- CHG-001-CHARGING-SEQUENCE
- WRKUP-001-WORKUP-CONTROL-AUTHORITY

### Files affected
- 01_process/Thermal/thr_001_thermal_control_authority.en.md
- 01_process/Thermal/thr_001_thermal_control_authority.zh.md
- 01_process/charging/chg_001_charging_sequence.en.md
- 01_process/charging/chg_001_charging_sequence.zh.md
- 01_process/workup/wrkup_001_workup_control_authority.en.md
- 01_process/workup/wrkup_001_workup_control_authority.zh.md
- 03_machine/openchemprocess_index.jsonl.md
- 03_machine/minimum_risk_taxonomy.md
- 03_machine/annotation_registry.md
- 03_machine/machine_change_log.md

### Rationale
THR-001 extends the machine layer by defining when temperature is a primary source of control authority rather than merely a rate parameter, thermal consequence, or heat-removal issue. The annotation adds review logic for competing pathway dominance, stage-gating authority, and boundary cases where thermal and charging controls are substitutable.

CHG-001 extends the machine layer by defining charging-sequence risk before addition mode, mixing, or thermal controls can act as effective safeguards. The annotation adds review logic for effective-mixing assumption, premature coexistence, physical decoupling, accumulation-then-trigger sequences, reactive inventory before trigger, strong-trigger sequences, and loss of feed-rate control after triggering.

WRKUP-001 extends the machine layer by defining when workup becomes a reaction-termination control layer. The annotation adds review logic for reaction end state not being the chemically stable final state, quench reaction completion, chemically incomplete quench, critical quench window, physically inaccessible quench, and apparent addition not being actual participation.

### Taxonomy impact
- Reused existing formal anchors: control_authority_decay, misallocated_control_authority.
- Reused existing candidate terms: lab_scale_masking, scalability_failure.
- Added THR-001 candidate terms: thermal_control_authority, temperature_as_primary_authority, competing_pathway_authority, stage_gating_authority, substitutable_control_authority.
- Added CHG-001 candidate terms: charging_sequence_risk, effective_mixing_assumption, accumulation_then_trigger, reactive_inventory_before_trigger, feed_rate_control_lost, strong_trigger_sequence, sliding_window_temperature_rise.
- Added WRKUP-001 candidate terms: workup_as_termination_control, reaction_end_state_not_final_state, quench_reaction_completion, chemically_incomplete_quench, critical_quench_window, physically_inaccessible_quench, apparent_addition_not_participation.

### Notes
These candidate terms should not be promoted to formal reasoning anchors until follow-up robustness testing confirms stable attribution boundaries across CHG-001, CHG-002, MIX-001, THR-001, and WRKUP-001. Source annotations use YAML for human-maintained snapshots, while JSONL index entries remain single-line JSON objects for machine use. Must / required / prohibited / recommended language from source snapshots is interpreted as review criteria or blocking signals, not as SOP-like process instructions.

## 2026-05-15 — Machine review robustness test results v0.2 added

Change type: test_result_added / robustness_checkpoint

Files added or updated:
- `03_machine/machine_review_test_results_v0.2.md`
- `03_machine/machine_change_log.md`
- `03_machine/annotation_registry.md` status verification only

Summary:
Completed the v0.2 upstream-control robustness test cycle covering OCP-MR-013 through OCP-MR-021. This cycle tested attribution boundaries among `CHG-001-CHARGING-SEQUENCE`, `CHG-002-ADDITION-MODE-AND-RATE`, `MIX-001-MIXING-TIME-SCALE-FAILURE`, `THR-001-THERMAL-CONTROL-AUTHORITY`, and `WRKUP-001-WORKUP-CONTROL-AUTHORITY`.

Result:
The machine-review layer passed the v0.2 cycle with minor warnings. No primary attribution collapse was observed. The main residual issue is section-placement discipline: in some boundary cases, signals from secondary, excluded, or weakly evidenced snapshots were placed under inferred / partially supported signals instead of excluded / not-established evidence.

Patch decision:
No taxonomy update required.
No JSONL update required.
No source snapshot update required.
No schema update required.

Follow-up:
Monitor future test outputs for QA-output contamination, especially where review-trigger labels, nearest canonical replacements, or excluded-snapshot signals are accidentally promoted into positive risk signals or reasoning anchors.


## 2026-05-16 — TLC gate-level machine annotations added

Change type: machine_annotation_added / jsonl_entries_added / taxonomy_candidate_terms_added / registry_updated

Files added or updated:
- `01_process/tlc/snapshot_tlc_pre_000_applicability_stability.zh.md`
- `01_process/tlc/snapshot_tlc_pre_000_applicability_stability.en.md`
- `01_process/tlc/snapshot_tlc_pre_001_representativeness_sampling.zh.md`
- `01_process/tlc/snapshot_tlc_pre_001_representativeness_sampling.en.md`
- `01_process/tlc/snapshot_tlc_diag_001_interpretability_gate.zh.md`
- `01_process/tlc/snapshot_tlc_diag_001_interpretability_gate.en.md`
- `03_machine/openchemprocess_index.jsonl`
- `03_machine/minimum_risk_taxonomy.md`
- `03_machine/annotation_registry.md`
- `03_machine/machine_change_log.md`

Summary:
Added the first TLC gate-level machine annotation batch covering `TLC-PRE-000-APPLICABILITY-STABILITY`, `TLC-PRE-001-REPRESENTATIVENESS-SAMPLING`, and `TLC-DIAG-001-INTERPRETABILITY-GATE`. This batch extends the machine layer from process-control authority review into observation-layer evidence admissibility, sampling representativeness, and TLC interpretability authority.

Machine-review purpose:
The new TLC entries train the Machine Reviewer to check whether TLC evidence is admissible before using TLC observations for reaction interpretation. The main review sequence is:
1. sample stability within the TLC exposure window and environment;
2. representativeness of the spotted micro-sample relative to the reaction system;
3. interpretability status of the developed and visualized TLC plate before chemical interpretation.

Taxonomy update:
Added a new taxonomy section: `Taxonomy Delta — TLC Observation and Diagnostic Gates`. New terms were added as candidate terms only, including `observation_validity_gate`, `sample_state_projection`, `representativeness_check`, `liquid_phase_only_projection`, `interpretability_gate`, `data_object_boundary`, `interpretability_revoked`, `interpretability_downgraded`, and `logical_void_status`.

Boundary decision:
TLC-specific parameters such as the 30-60 second exposure window, Rf compression intervals, background-noise threshold, tail-extension threshold, and co-spot Delta Rf intervals were recorded only as TLC-specific review triggers. They were not promoted to global analytical rules or formal reasoning anchors.

Patch decision:
No schema update required.
No benchmark update required.
No source-frontmatter update required.
No formal-anchor promotion required.
No DIAG-002 or diagnostic-example entries were added in this batch.

Follow-up:
Future TLC diagnostic-pathway and diagnostic-example annotations should reuse these gate-level terms where possible. Example-level morphology or plate-pattern terms should not be promoted into taxonomy unless they clarify or reuse the established observation-validity, representativeness, or interpretability-gate structure.
## 2026-05-17 — TLC interpretation-pathway machine annotation added

Change type: machine_annotation_added / jsonl_entry_added / taxonomy_candidate_terms_added / registry_updated

Files added or updated:
- `01_process/tlc/snapshot_tlc_diag_002_interpretation_pathways.zh.md`
- `01_process/tlc/snapshot_tlc_diag_002_interpretation_pathways.en.md`
- `03_machine/openchemprocess_index.jsonl`
- `03_machine/minimum_risk_taxonomy.md`
- `03_machine/annotation_registry.md`
- `03_machine/machine_change_log.md`

Summary:
Added the formal machine annotation for `TLC-DIAG-002-INTERPRETATION-PATHWAYS`. This entry extends the TLC diagnostic gate sequence from interpretability adjudication into permitted interpretation-pathway selection.

Machine-review purpose:
The new entry trains the Machine Reviewer to select only permitted TLC interpretation pathways after `TLC-DIAG-001` has established interpretability. It blocks prohibited inferences including precise conversion percentages, kinetic quantification, direct intensity-content equivalence, complete-conversion claims from starting-material disappearance, and definitive structural assignment from TLC signals.

Taxonomy update:
Added additional candidate terms under `Taxonomy Delta — TLC Observation and Diagnostic Gates`, including `permitted_interpretation_pathway`, `presence_absence_inference`, `identity_consistency_check`, `qualitative_trend_monitoring`, `prohibited_quantitative_conversion`, `intensity_content_non_equivalence`, and `co_elution_uncertainty`.

Boundary decision:
`TLC-DIAG-002` was added as a formal JSONL entry because it defines a reusable review layer after interpretability is established. It is not a TLC operating procedure and does not prescribe experimental optimization steps.

Candidate-only review:
`TLC-DIAG-EX-001-FRONTING-BAND-AND-BASELINE-COMPRESSION` and `TLC-DIAG-EX-002-OVERLOAD-AND-SOLVENT-CARRYOVER` were reviewed as diagnostic examples only. They were not added to JSONL, registry completed status, or formal taxonomy in this batch. Their morphology-specific terms remain candidate-only / example-level and should not be promoted unless later reuse demonstrates cross-example review value.

Patch decision:
No schema update required.
No benchmark update required.
No source-frontmatter update required.
No formal-anchor promotion required.
No diagnostic-example JSONL entries were added in this batch.

## 2026-05-17 — TLC preparation, projection-axis, and visual-object machine annotations added

Change type: machine_annotation_added / jsonl_entries_added / taxonomy_candidate_terms_added / registry_updated

Files added or updated:
- `01_process/tlc/snapshot_tlc_pre_002_sample_preparation_gate.zh.md`
- `01_process/tlc/snapshot_tlc_pre_002_sample_preparation_gate.en.md`
- `01_process/tlc/snapshot_tlc_003_eluent_selection.zh.md`
- `01_process/tlc/snapshot_tlc_003_eluent_selection.en.md`
- `01_process/tlc/snapshot_tlc_004_plate_visual_observation.zh.md`
- `01_process/tlc/snapshot_tlc_004_plate_visual_observation.en.md`
- `03_machine/openchemprocess_index.jsonl`
- `03_machine/minimum_risk_taxonomy.md`
- `03_machine/annotation_registry.md`
- `03_machine/machine_change_log.md`

Summary:
Added formal machine annotations for `TLC-PRE-002-SAMPLE-PREPARATION-GATE`, `TLC-003-ELUENT-SELECTION`, and `TLC-004-PLATE-VISUAL-OBSERVATION`. This batch completes the core TLC observation chain from sample admissibility and preparation, through projection-axis selection, to visual data-object generation before diagnostic interpretation.

Machine-review purpose:
The new entries train the Machine Reviewer to decide whether TLC evidence is chemically prepared, physically projectable, and visually objectified before downstream diagnostic interpretation. The emphasis remains on evidence admissibility, projection-axis validity, and visual-object integrity rather than TLC operation optimization.

Taxonomy update:
Added candidate terms under `Taxonomy Delta — TLC Observation and Diagnostic Gates`, including `sample_preparation_gate`, `quench_requirement_check`, `dilution_requirement_check`, `matrix_compatibility_check`, `migration_distortion_control`, `projection_axis_validity`, `information_projection_axis`, `projection_axis_compression`, `rf_regular_projection`, `surface_interaction_decoupling`, `non_inferable_zone`, `visual_data_object_generation`, `visualization_validity`, `information_revealing_order`, `solvent_front_marker_integrity`, `temporal_visual_validity`, and `pre_diagnostic_visual_failure`.

Boundary decision:
TLC-specific time, concentration, Rf, solvent-ratio, and visualization-window values were recorded only as TLC-specific review triggers. They were not promoted to global analytical rules or formal reasoning anchors. The new machine annotations are review-layer entries and should not be interpreted as TLC operating SOPs.

Candidate-only review:
`TLC-002-SPOTTING-OPERATION` was reviewed as operation-heavy and kept candidate-only in this batch. It was not added to JSONL, registry completed status, or taxonomy candidate anchors. Its higher-level framing as spatial signal encoding may be reconsidered later if multiple diagnostic examples reuse spotting-related validity logic.

Patch decision:
No schema update required.
No benchmark update required.
No source-frontmatter update required.
No formal-anchor promotion required.
No TLC-002 JSONL entry was added in this batch.
## 2026-05-17 — TLC coordinate-baseline and spotting-layout machine annotations added

Change type: machine_annotation_added / jsonl_entries_added / taxonomy_candidate_terms_added / registry_updated

Files added or updated:
- `01_process/tlc/snapshot_tlc_000_origin_line.zh.md`
- `01_process/tlc/snapshot_tlc_000_origin_line.en.md`
- `01_process/tlc/snapshot_tlc_001_spotting_layout.zh.md`
- `01_process/tlc/snapshot_tlc_001_spotting_layout.en.md`
- `03_machine/openchemprocess_index.jsonl`
- `03_machine/minimum_risk_taxonomy.md`
- `03_machine/annotation_registry.md`
- `03_machine/machine_change_log.md`

Summary:
Added formal machine annotations for `TLC-000-ORIGIN-LINE` and `TLC-001-SPOTTING-LAYOUT`. This batch completes the basic TLC coordinate and reference-layout layer beneath the previously added preparation, projection-axis, visual-object, interpretability, and interpretation-pathway gates.

Machine-review purpose:
The new entries train the Machine Reviewer to check whether TLC has a valid physical coordinate baseline and lane-reference layout before performing Rf calculation, cross-lane comparison, identity consistency review, matrix-shift compensation, or reaction trend interpretation.

Taxonomy update:
Added candidate terms under `Taxonomy Delta — TLC Observation and Diagnostic Gates`, including `coordinate_baseline_integrity`, `origin_line_validity`, `rf_coordinate_validity`, `cross_lane_comparison_validity`, `centroid_localization_validity`, `physical_marker_noninterference`, `reference_layout_validity`, `relative_coordinate_system`, `co_spot_anchoring`, `matrix_shift_compensation`, `lane_geometry_validity`, and `edge_effect_control`.

Boundary decision:
TLC-specific geometric values such as origin-line height, vertical alignment tolerance, initial spot diameter, lane spacing, and edge margin were recorded only as TLC-specific review triggers. They were not promoted to global analytical rules or formal reasoning anchors. Lane intensity / area ratio remains limited to rough qualitative or relative trend interpretation and must not be used for precise conversion inference.

Candidate-only status:
`TLC-002-SPOTTING-OPERATION` remains candidate-only and was not added to JSONL, registry completed status, or taxonomy candidate anchors in this batch. Existing candidate annotation blocks remain sufficient for now.

Patch decision:
No schema update required.
No benchmark update required.
No source-frontmatter update required.
No formal-anchor promotion required.
No TLC-002 JSONL entry was added in this batch.

## 2026-05-17 — WRKUP quench checklist and TLC meta-level diagnostic authority annotations added

Change type: machine_annotation_added / jsonl_entries_added / taxonomy_candidate_terms_added / registry_updated

Files added or updated:
- `01_process/workup/wrkup_001_quench_checklist.zh.md`
- `01_process/workup/wrkup_001_quench_checklist.en.md`
- `00_meta/snapshot_tlc_meta_001_early_diagnostic_value_and_limits.zh.md`
- `00_meta/snapshot_tlc_meta_001_early_diagnostic_value_and_limits.en.md`
- `00_meta/snapshot_tlc_meta_002_feedback_loops_and_decision_latency.zh.md`
- `00_meta/snapshot_tlc_meta_002_feedback_loops_and_decision_latency.en.md`
- `03_machine/openchemprocess_index.jsonl`
- `03_machine/minimum_risk_taxonomy.md`
- `03_machine/annotation_registry.md`
- `03_machine/machine_change_log.md`

Summary:
Added formal machine annotations for one derived WRKUP rejection checklist and two TLC meta-level diagnostic authority documents: `WRKUP-001-QUENCH-CHECKLIST`, `TLC-META-001-EARLY-DIAGNOSTIC-VALUE-AND-LIMITS`, and `TLC-META-002-DECISION-LATENCY-AND-FEEDBACK-STRATEGY`.

Machine-review purpose:
The WRKUP checklist entry provides a derived rejection gate for preventing downstream progression when quench completion, critical reactive-window control, or physical accessibility is not established. The TLC meta entries define when TLC has diagnostic authority, when that authority should be downgraded or terminated, and how TLC functions as a high-frequency low-latency feedback branch rather than a replacement for precision analysis.

Taxonomy update:
Added candidate terms including `rejection_checklist_gate`, `diagnostic_value_boundary`, `early_stage_diagnostic_authority`, `late_stage_interpretability_downgrade`, `total_sample_projection`, `discovery_first_logic`, `pseudo_completion_risk`, `resolution_scale_mismatch`, `decision_latency_match`, `high_frequency_low_latency_feedback`, `multi_level_feedback_strategy`, `temporal_aliasing_risk`, `situational_awareness_branch`, `precision_confirmation_branch`, `fuzzy_anomaly_detection`, and `decision_safety_margin`.

Boundary decision:
`WRKUP-001-QUENCH-CHECKLIST` was added as a derived decision gate and does not introduce new process knowledge. It provides rejection logic only and must not be interpreted as optimization or remediation guidance. The TLC meta entries do not provide TLC operating instructions, do not change release standards, and do not replace precision analytical methods.

Patch decision:
No schema update required.
No benchmark update required.
No source-frontmatter update required.
No formal-anchor promotion required.

## 2026-05-17 — TLC diagnostic examples reviewed as candidate-only annotations

Change type: candidate_annotation_added / no_jsonl_update / no_registry_update / no_taxonomy_promotion

Files updated:
- `01_process/tlc/snapshot_tlc_diag_ex_003_low_rf_triangular_tailing_surface_interaction.zh.md`
- `01_process/tlc/snapshot_tlc_diag_ex_003_low_rf_triangular_tailing_surface_interaction.en.md`
- `01_process/tlc/snapshot_tlc_diag_ex_004_logic_gap_missing_spike_and_fronting_overflow.zh.md`
- `01_process/tlc/snapshot_tlc_diag_ex_004_logic_gap_missing_spike_and_fronting_overflow.en.md`
- `01_process/tlc/snapshot_tlc_diag_ex_005_starting_material_stagnation_and_polarity_gap.zh.md`
- `01_process/tlc/snapshot_tlc_diag_ex_005_starting_material_stagnation_and_polarity_gap.en.md`

Summary:
Reviewed `TLC-DIAG-EX-003`, `TLC-DIAG-EX-004`, and `TLC-DIAG-EX-005` as diagnostic examples and added `Machine Annotation Candidate` blocks only. These examples reuse established TLC gate-level anchors such as `interpretability_gate`, `interpretability_downgraded`, `interpretability_revoked`, `co_spot_anchoring`, `logical_void_status`, `projection_axis_validity`, and `reference_layout_validity`.

Boundary decision:
No JSONL entries were added. No registry completed / added rows were created. No example-specific morphology terms were promoted into taxonomy. `TLC-DIAG-EX-004` is marked for future sub-snapshot watch because it strongly reinforces missing co-spot reference, logical void status, and prohibited reaction-completion inference.

Patch decision:
No schema update required.
No benchmark update required.
No source-frontmatter update required.
No formal-anchor promotion required.

## 2026-05-17 — TLC TECH quench recipes reviewed as candidate-only annotation

Change type: candidate_annotation_added / no_jsonl_update / no_registry_update / no_taxonomy_promotion

Files updated:
- `01_process/tlc/snapshot_tlc_tech_001_quench_recipes.zh.md`
- `01_process/tlc/snapshot_tlc_tech_001_quench_recipes.en.md`

Summary:
Reviewed `TLC-TECH-001-QUENCH-RECIPES` as a TECH toolbox file and added `Machine Annotation Candidate` blocks only. The file supports TLC sample-preparation decisions after `TLC-PRE-002-SAMPLE-PREPARATION-GATE` has determined that quenching or derivatization is required.

Boundary decision:
No JSONL entry was added. No registry completed / added row was created. No recipe-specific terms were promoted into taxonomy. The file remains a technical support module and must not be interpreted as a Machine Reviewer SOP source.

Review boundary:
TLC quench recipes may help transform a reactive or poorly projectable sample into a TLC-interpretable derivative, but recipe execution does not prove original reaction completion, workup quench completion, or process termination. Reagent examples such as MeOH, EtOH, ammonia, amines, AcOH, AcOH/MeOH, or hydride-quench conditions should remain recipe-level information and should not be converted into review rules.

Patch decision:
No schema update required.
No benchmark update required.
No source-frontmatter update required.
No formal-anchor promotion required.

## 2026-05-17 — TLC robustness test results v0.3 added

Change type: test_result_added / robustness_checkpoint / no_taxonomy_update / no_jsonl_update

Files added or updated:
- `03_machine/machine_review_test_results_v0.3_tlc.md`
- `03_machine/machine_change_log.md`

Summary:
Completed the v0.3 TLC machine-review robustness test cycle covering `OCP-MR-022` through `OCP-MR-029`. This cycle tested TLC evidence admissibility, sampling representativeness, interpretability status, permitted interpretation pathways, TLC meta-level diagnostic authority, decision latency, TLC sample-quench boundaries, and candidate-only diagnostic/TECH example containment.

Result:
The TLC machine-review layer passed the v0.3 cycle with attribution-layer warnings. The model reliably blocked incorrect chemical conclusions: it did not treat TLC as precise conversion evidence, did not treat blank sample lanes as reaction completion, did not treat same-Rf behavior as definitive identity, did not treat TLC quench recipes as workup or process completion evidence, did not convert TLC morphology into taxonomy, and did not provide SOP-like recommendations.

Issue exposed:
The main residual issue is primary-snapshot attribution precision. In several cases, the model reached the correct review conclusion but collapsed narrower or higher-level TLC layers into broader gates. Specifically, `TLC-001-SPOTTING-LAYOUT`, `TLC-PRE-002-SAMPLE-PREPARATION-GATE`, `TLC-DIAG-002-INTERPRETATION-PATHWAYS`, `TLC-META-001-EARLY-DIAGNOSTIC-VALUE-AND-LIMITS`, and `TLC-META-002-DECISION-LATENCY-AND-FEEDBACK-STRATEGY` were sometimes under-attributed, with the model falling back to `TLC-DIAG-001-INTERPRETABILITY-GATE` or `TLC-PRE-000-APPLICABILITY-STABILITY`.

Patch decision:
No taxonomy update required.
No JSONL update required.
No source snapshot update required.
No schema update required.
Optional future prompt patch only: emphasize selecting the narrowest governing snapshot and avoiding collapse of meta-level, sample-preparation, reference-layout, or permitted-interpretation boundaries into generic TLC pre-observation or interpretability gates.

Follow-up:
Before expanding TLC annotations further, update or annotate the machine-review test prompt to reinforce attribution precision for TLC layers. Future v0.3+ testing should continue to separate correct blocked conclusions from correct primary-snapshot attribution.

## 2026-05-17 — Machine review test prompt attribution-precision patch added

Change type: prompt_patch_added / no_taxonomy_update / no_jsonl_update / no_source_snapshot_update

Files added or updated:
- `03_machine/machine_review_test_prompt_v0.1.md`
- `03_machine/machine_change_log.md`

Summary:
Added an attribution-precision rule to the machine-review test prompt after v0.3 TLC robustness testing. The patch instructs the reviewer to select the narrowest governing snapshot rather than collapsing specific TLC layers into broader gates.

Reason:
The v0.3 TLC robustness cycle showed that model outputs often reached the correct blocked conclusion but under-attributed the primary snapshot. In particular, `TLC-001-SPOTTING-LAYOUT`, `TLC-PRE-002-SAMPLE-PREPARATION-GATE`, `TLC-DIAG-002-INTERPRETATION-PATHWAYS`, `TLC-META-001-EARLY-DIAGNOSTIC-VALUE-AND-LIMITS`, and `TLC-META-002-DECISION-LATENCY-AND-FEEDBACK-STRATEGY` were sometimes collapsed into `TLC-DIAG-001-INTERPRETABILITY-GATE` or `TLC-PRE-000-APPLICABILITY-STABILITY`.

Patch decision:
No taxonomy update required.
No JSONL update required.
No source snapshot update required.
No schema update required.
Prompt-level attribution guidance only.