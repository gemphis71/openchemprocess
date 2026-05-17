# Machine Review Test Results v0.1

status: final test log  
scope: results from robustness test cases in machine_review_test_cases_v0.1.md  
date_started: 2026-05-06  
date_completed: 2026-05-10  

## Overall assessment

The first 12-case robustness cycle broadly passed. The current machine layer can identify review-domain snapshots, reject several false-positive cases, avoid deterministic threshold misuse, and maintain the Machine Reviewer frame without SOP-like operational recommendations. The main residual risk is not taxonomy coverage but output-boundary discipline: future tests must keep review-domain match, risk-positive conclusion, matched risk signals, inferred / partially supported signals, reasoning anchors, and canonical correction / nearest allowed terms strictly separated.

Patch scope: update `machine_review_test_prompt_v0.1.md`, minimally adjust expected wording in `machine_review_test_cases_v0.1.md`, add QA-output contamination checks to `machine_layer_integrity_checklist.md`, and record this checkpoint in `machine_change_log.md`. No taxonomy, JSONL, schema, or source snapshot change is required from this baseline cycle.

## OCP-MR-001

Status: Pass with warning

Model tested:
- ChatGPT

Pass basis:
- Correctly rejected positive `partition_ratio_drift` conclusion.
- Correctly treated `Delta Kd(1->2) > 15%` as a soft-block discriminator, not a deterministic rule.
- No action recommendation leakage.
- No non-canonical reasoning anchor introduced.

Warning:
- The model used `WRKUP-002-PARTITION-RATIO-DRIFT-INVENTORY-CONTROL` as a high-confidence primary snapshot, which is acceptable as a review-domain match but should be distinguished from a positive-risk match.
- The reasoning anchors list included unsupported or explicitly excluded anchors, including `chemical_speciation_drift`, `rag_layer_third_phase`, `emulsion_inventory_audit`, and `recycled_solvent_loading_drift`.

Patch required:
- Revise OCP-MR-001 expected primary snapshot wording in `machine_review_test_cases_v0.1.md`.
- Add Hard Rule 11 to `machine_review_test_prompt_v0.1.md`: positively supported anchors only; unsupported or excluded anchors belong under uncertainty / excluded evidence.

## OCP-MR-002

Status: Pass

Model tested:
- ChatGPT

Pass basis:
- Correctly matched `WRKUP-002-PARTITION-RATIO-DRIFT-INVENTORY-CONTROL` as the primary snapshot.
- Correctly identified `rag layer observed` and `visible rag layer without inventory audit` as matched risk signals.
- Correctly did not treat `Delta Kd(1->2) > 15%` as triggered because Kd difference is only 8%.
- Correctly interpreted the rag layer as a separate `interfacial_inventory_loss_channel` / `rag_layer_third_phase`, outside the clean two-bulk-phase Kd model.
- Correctly avoided listing `partition_ratio_drift`, `chemical_speciation_drift`, or `phase_environment_drift` as positively supported anchors.
- No action recommendation leakage.
- No non-canonical reasoning anchor introduced.
- No deterministic threshold misuse.

Patch required:
- None.

## OCP-MR-003

Status: Pass with minor warning

Model tested:
- ChatGPT

Pass basis:
- Correctly matched `WRKUP-002-PARTITION-RATIO-DRIFT-INVENTORY-CONTROL` as the primary snapshot.
- Correctly identified `free/ionic speciation mixture possible`, `pH on target treated as species-unification evidence`, `complexed or ion-paired species unresolved by TLC/HPLC`, and `Kd_ref and Kd_in_situ differ by >15%` as matched risk signals.
- Correctly treated the >15% `Kd_ref` / `Kd_in_situ` difference as a species-first directional review trigger, not as deterministic proof of one mechanism.
- Correctly used `chemical_speciation_drift` and `species_first_diagnostic_order` as the primary reasoning anchors.
- Correctly avoided action recommendation leakage.
- No non-canonical reasoning anchor introduced.

Warning:
- The model listed `phase_environment_drift` and `carryover_inventory` under reasoning anchors, but the scenario does not provide positive evidence for phase-environment change or actual carryover inventory.
- These terms should be placed under uncertainty / possible but unproven explanations, not under positively supported reasoning anchors.

Patch required:
- No taxonomy or JSONL change.
- Keep monitoring whether Hard Rule 11 is strong enough; if this pattern repeats in later cases, strengthen the prompt from “positively supported” to “directly evidenced by the scenario.”

## OCP-MR-004

Status: Pass with warning

Model tested:
- ChatGPT

Pass basis:
- Correctly did not treat CF = 7 alone as a triggered WRKUP-003 failure.
- Correctly excluded `CF > 3 with nonvolatile inventory present and undeclared`, `CF > 5 in acid/base sensitive system with heating to complete dryness`, and `CF > 10 without explicit override`.
- Correctly recognized that the main WRKUP-003 risk amplifiers are absent.
- Correctly avoided action recommendation leakage.
- No non-canonical reasoning anchor introduced.
- No deterministic threshold misuse.

Warning:
- The model used `WRKUP-003-SOLVENT-REMOVAL-DRIVEN-ACCUMULATION-AND-THERMAL-EXPOSURE-CONTROL` as a high-confidence primary snapshot, which is acceptable as a review-domain match but should be distinguished from a positive-risk match.
- The phrase “low-risk / exception-type WRKUP-003 case” is acceptable as review language, but future tests should avoid turning this into a new category unless registered.

Patch required:
- Revise OCP-MR-004 expected primary snapshot wording to distinguish review-domain snapshot from positive-risk conclusion.
- Consider adding a prompt output field: `Risk-positive conclusion: yes / no / uncertain`.

## OCP-MR-005

Status: Pass with minor warning

Model tested:
- ChatGPT

Pass basis:
- Correctly matched `WRKUP-003-SOLVENT-REMOVAL-DRIVEN-ACCUMULATION-AND-THERMAL-EXPOSURE-CONTROL` as the primary snapshot.
- Correctly set `Risk-positive conclusion: yes`.
- Correctly did not treat CF = 2.8 as clearance.
- Correctly identified qualitative WRKUP-003 risk signals including `nonvolatile salts, acids, bases, high-boiling residues, or modifiers remain during concentration`, `planned complete dryness` / near-dryness boundary, `final volume below minimum stirrable volume`, and `wet-product solvent target not defined`.
- Correctly used `forced_composition_path`, `nonvolatile_accumulation`, `thermal_exposure_accumulation`, and `equipment_transfer_boundary` as primary reasoning anchors.
- Correctly kept ISOL-003 as secondary downstream-facing relevance.
- No action recommendation leakage.
- No non-canonical reasoning anchor introduced.
- No deterministic threshold misuse.

Warning:
- `planned complete dryness` is not exactly proven because the scenario says near dryness, not confirmed complete dryness; acceptable as boundary-adjacent, but should be marked as partially supported.
- `solid residue without transfer plan`, `high-boiling solvent retention`, and some secondary ISOL-003 anchors are plausible but not fully evidenced.
- `control_authority_decay` and `misallocated_control_authority` are formally allowed anchors, but the directly evidenced WRKUP-003 anchors are stronger and should remain primary.

Patch required:
- No taxonomy or JSONL change.
- If repeated, strengthen prompt wording to separate “matched risk signals” from “partially supported / inferred risk signals.”

## OCP-MR-006

Status: Pass with minor warning

Model tested:
- ChatGPT

Pass basis:
- Correctly matched `WRKUP-003-SOLVENT-REMOVAL-DRIVEN-ACCUMULATION-AND-THERMAL-EXPOSURE-CONTROL` as the primary snapshot.
- Correctly set `Risk-positive conclusion: yes`.
- Correctly identified `mixed-solvent system without VRT volatility order`, `mixed-solvent system without CEP composition-drift assessment`, `lower-boiling solvent removal may cross instability zone`, and `oiling out during concentration` as matched WRKUP-003 risk signals.
- Correctly treated thermal stability as insufficient to clear composition-path risk.
- Correctly used `volatile_removal_trajectory`, `composition_evolution_path`, and `forced_composition_path` as core reasoning anchors.
- Correctly kept ISOL-001 as secondary and downstream-facing.
- No action recommendation leakage.
- No non-canonical reasoning anchor introduced.
- No deterministic threshold misuse.

Warning:
- `oil_out_flag observed` under secondary ISOL-001 is not directly supported because the case states crossing an oiling-out zone, not observed crystallization-stage oil-out.
- `control_authority_decay`, `misallocated_control_authority`, and `upstream_solvent_selection_coupling` are allowed anchors, but the directly evidenced anchors are `volatile_removal_trajectory`, `composition_evolution_path`, and `forced_composition_path`.

Patch required:
- No taxonomy or JSONL change.
- Continue monitoring whether the prompt needs a distinction between `matched`, `partially supported`, and `secondary/interface-relevant` signals.

## OCP-MR-007

Status: Pass

Model tested:
- ChatGPT

Pass basis:
- Correctly matched `ISOL-003-FILTRATION` as the primary review-domain snapshot.
- Correctly set `Risk-positive conclusion: uncertain / weak yes`, rather than high-risk failure.
- Correctly identified `WMR >= 2` as the only positively matched risk signal.
- Correctly excluded `washing displacement efficiency not demonstrated`, `nonlinear flux decline`, `mother liquor retention not quantified`, `drying burden dominates downstream`, and `WMR >= 3`.
- Correctly treated `WMR >= 2` as a review trigger / watch-risk, not as automatic non-scalability or deterministic failure.
- Correctly used `wet_mass_ratio`, `washing_displacement_efficiency`, and `mother_liquor_retention` as the main reasoning anchors.
- No action recommendation leakage.
- No non-canonical reasoning anchor introduced.
- No deterministic threshold misuse.

Warning:
- None material.

Patch required:
- None.

## OCP-MR-008

Status: Pass with warning

Model tested:
- ChatGPT

Pass basis:
- Correctly matched `ISOL-003-FILTRATION` as the primary snapshot.
- Correctly set `Risk-positive conclusion: yes`.
- Correctly did not treat lab `WMR = 1.35` as low-risk clearance.
- Correctly identified `nonlinear increase of separation time with cake thickness`, `dense or compressible cake`, `breakthrough due to non-uniform cake`, and `mother liquor retention not quantified` as the dominant ISOL-003 risk signals.
- Correctly interpreted the case as lab-scale masking and scale-up filtration failure rather than drying failure.
- Correctly avoided action recommendation leakage.
- No deterministic threshold misuse.

Warning:
- Output used Chinese in expert judgment, while the prompt/test format is intended to keep structured machine-review output in English.
- `lab_scale_masking / scale-up risk signal` was listed under matched risk signals, but `lab_scale_masking` is a reasoning anchor, not an exact JSONL risk signal.
- Some anchors such as `loss_amplification_interface` and `downstream_filtration_compatibility` are allowed, but the directly evidenced anchors are `lab_scale_masking`, `scalability_failure`, `structure_inheritance`, `wet_mass_ratio`, and `mother_liquor_retention`.

Patch required:
- Add or strengthen prompt language that matched risk signals must be exact risk signals from JSONL/taxonomy, while reasoning anchors must stay in the reasoning anchor section.
- Consider requiring English-only output for structured test results if these files are intended for machine-layer QA.

## OCP-MR-009

Status: Pass with warning

Model tested:
- ChatGPT

Pass basis:
- Correctly matched `ISOL-003-FILTRATION` as the primary snapshot.
- Correctly kept `ISOL-004-DRYING` as the secondary snapshot.
- Correctly set `Risk-positive conclusion: yes`.
- Correctly identified `WMR >= 2`, `washing cannot sustain impurity removal`, `washing displacement efficiency not demonstrated`, `residual solvent curve reaches plateau`, and `extended vacuum time used as sole corrective action`.
- Correctly did not treat drying plateau as a simple drying-time issue.
- Correctly excluded `surface_good_solvent_enrichment`, `surface_composition_drift`, `surface_redissolution`, and `rolling_agglomeration`.
- No action recommendation leakage.
- No non-canonical reasoning anchor introduced.
- No deterministic threshold misuse.

Warning:
- `wet cake ratio >= 2` may be acceptable only if WMR is treated as equivalent to wet cake ratio in this test context; otherwise it should be marked as inferred rather than directly matched.
- `high mother liquor retention` is plausible from WMR = 2.6 and failed washing, but not directly quantified.
- `drying burden dominates downstream` is plausible but not explicitly stated.
- `pore_bound_solvent_retention` is not directly evidenced; drying plateau supports drying-stage review but does not prove pore-bound retention mechanism.
- Several allowed anchors are listed, but the directly evidenced anchors should remain `wet_mass_ratio`, `washing_displacement_efficiency`, `mother_liquor_retention`, `consequence_stage_separation`, `structure_inheritance`, and `drying_plateau`.

Patch required:
- Same as OCP-MR-008: strengthen prompt separation between direct matched signals, inferred/partially supported signals, and reasoning anchors.
- No taxonomy or JSONL change.

## OCP-MR-010

Status: Pass

Model tested:
- ChatGPT

Pass basis:
- Correctly matched `ISOL-004-DRYING` as the review-domain snapshot.
- Correctly set `Risk-positive conclusion: no`.
- Correctly identified `rolling stage present in equipment` and `rolling_equipment_present: yes` as the only directly matched drying-context signals.
- Correctly did not treat rolling equipment alone as sufficient evidence for `rolling_agglomeration`, `surface_composition_drift`, `surface_redissolution`, balling, or drying plateau.
- Correctly separated inferred/partially supported signals and wrote `None`.
- Correctly avoided action recommendation leakage.
- No non-canonical reasoning anchor introduced.
- No deterministic threshold misuse.

Warning:
- None material.

Patch required:
- None.

## OCP-MR-011

Status: Pass

Model tested:
- ChatGPT

Pass basis:
- Correctly matched `ISOL-004-DRYING` as the primary snapshot.
- Correctly kept `ISOL-003-FILTRATION` as the possible secondary snapshot.
- Correctly set `Risk-positive conclusion: yes`.
- Correctly identified the pore-bound / bound-solvent drying plateau pathway despite the explicit absence of balling or agglomeration.
- Correctly matched direct ISOL-004 risk signals including `needle or rod morphology`, `solvent retained in internal or interparticle pores`, `salt form present`, `hydrogen-bond-capable solvent present`, `ionic or hydrogen-bond interaction between solvent and product suspected`, `residual solvent curve reaches plateau`, `plateau_check yes`, `thin-layer lab drying masks pore retention`, and `extended vacuum time used as sole corrective action`.
- Correctly separated partially supported signals into section 2b, including `pore structure likely from particle packing`, `thick-bed mass-transfer limitation suspected`, and `process relies only on vacuum, temperature, and time`.
- Correctly used `pore_bound_solvent_retention`, `bound_solvent_state`, `drying_plateau`, `lab_scale_masking`, and `solvent_state_location_lock_in` as core reasoning anchors.
- Correctly excluded the balling / rolling-agglomeration path from the dominant interpretation.
- No action recommendation leakage.
- No non-canonical reasoning anchor introduced.
- No deterministic threshold misuse.

Warning:
- Some higher-level anchors such as `upstream_failure_exposure`, `scalability_failure`, and `drying_compensation_boundary` are allowed, but the directly evidenced anchors are mainly `pore_bound_solvent_retention`, `bound_solvent_state`, `drying_plateau`, `lab_scale_masking`, `structure_inheritance`, and `solvent_state_location_lock_in`.

Patch required:
- None.

## OCP-MR-012

Status: Pass with minor warning

Model tested:
- ChatGPT

Pass basis:
- Correctly identified this as a reviewer-behavior compliance test rather than a normal process-scenario matching task.
- Correctly set `Primary snapshot: no confident primary snapshot`.
- Correctly set `Risk-positive conclusion: uncertain` because the underlying process evidence is missing.
- Correctly flagged `loss amplification`, `control-authority loss`, and `drying rescue failure` as non-canonical or non-exact terminology.
- Correctly identified `loss_amplification_interface` and `control_authority_decay` as the closest exact canonical terms, while noting that they require evidence support.
- Correctly flagged adding an anti-solvent wash, lowering vacuum, and switching dryer as SOP-like operational recommendations / action leakage.
- Correctly stated that no matched risk signals are supported by the provided reviewer statement alone.
- Correctly avoided deterministic threshold misuse.

Warning:
- The answer listed `process relies only on vacuum, temperature, and time`, `filtration relies only on strong compensatory measures`, and `scale operability cannot be established` under inferred or partially supported signals, but these are too weakly implied from the reviewed answer and should preferably be listed as “not supported” rather than partially supported.
- The answer listed canonical anchors under “Reasoning anchors” even though it later says they are only conceptual alignments. For this compliance-test case, those should ideally be placed under a separate “canonical correction / nearest allowed terms” field, not under positively supported reasoning anchors.

Patch required:
- No taxonomy or JSONL change.
- Consider adding one prompt rule for reviewer-output audit cases: when the input is another reviewer’s answer rather than a process scenario, do not list reasoning anchors as positively supported unless the underlying process evidence is present; instead list non-canonical terms and nearest canonical replacements separately.