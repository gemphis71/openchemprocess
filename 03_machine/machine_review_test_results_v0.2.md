# Machine Review Test Results v0.2

status: final test log  
scope: results from upstream-control robustness test cases in `machine_review_test_cases_v0.2.md`  
date_started: 2026-05-15  
date_completed: 2026-05-15  

## Overall assessment

The v0.2 upstream-control robustness cycle broadly passed. The expanded machine layer can preserve attribution boundaries among `CHG-001-CHARGING-SEQUENCE`, `CHG-002-ADDITION-MODE-AND-RATE`, `MIX-001-MIXING-TIME-SCALE-FAILURE`, `THR-001-THERMAL-CONTROL-AUTHORITY`, and `WRKUP-001-WORKUP-CONTROL-AUTHORITY`. The tests confirmed that the Machine Reviewer can separate charging-sequence accumulation-before-trigger risk from downstream thermal manifestation, distinguish nominal dosing from effective material entry, avoid assigning apparent mixing phenomena to core MIX-001 when CHG-002 explains the behavior, recognize true MIX-001 local-history lock-in, distinguish temperature-as-primary-authority from temperature-rise symptoms, and separate true quench-completion control from ordinary workup cleanup.

No taxonomy, JSONL, schema, registry, or source snapshot change is required from this test cycle. The observed residual issue is section-placement discipline, not conceptual coverage. Several outputs correctly reached the final attribution judgment but placed weakly supported or explicitly excluded secondary-snapshot signals under `Inferred or partially supported signals`. This is most visible in CHG-002 / MIX-001 boundary cases. Future prompt wording should state that signals from explicitly excluded, eliminated, or manifestation-only secondary snapshots belong under excluded / not-established evidence unless independently supported by the scenario.

Patch scope: minor prompt/checklist refinement only. Recommended patch: update the machine-review test prompt, or create a v0.2 version, to strengthen separation among directly matched signals, weak inferred signals, excluded evidence, reasoning anchors, and review-trigger labels. Add a corresponding checklist watch item under section placement discipline. No machine-layer data terms should be added based on these test outputs.

## OCP-MR-013

Status: Pass with minor warning

Model tested:
- Not specified

Pass basis:
- Correctly matched `CHG-001-CHARGING-SEQUENCE` as the primary snapshot.
- Correctly kept `CHG-002-ADDITION-MODE-AND-RATE` and `THR-001-THERMAL-CONTROL-AUTHORITY` as secondary / manifestation review domains only.
- Correctly set `Risk-positive conclusion: yes` based on the accumulation-before-trigger structure, not on review-domain match alone.
- Correctly identified direct CHG-001 risk signals including accumulated reactants before triggering, catalyst-triggered initiation, reactive inventory before trigger, feed-rate control loss after trigger, generation-rate / heat-removal stress, and small-scale thermal masking.
- Correctly used canonical reasoning anchors: `charging_sequence_risk`, `accumulation_then_trigger`, `reactive_inventory_before_trigger`, `feed_rate_control_lost`, `control_authority_decay`, and `lab_scale_masking`.
- Correctly treated post-trigger heat-removal failure as consequence / manifestation rather than primary THR-001 attribution.
- No SOP-like recommendation leakage.
- No non-canonical reasoning anchor introduced.
- No deterministic threshold misuse.

Warning:
- `reaction shows induction period or auto-accelerating behavior during dosing` was placed under inferred / partially supported signals, but the case is not framed as a CHG-002 dosing-phase effective-entry failure. It should be treated as not-established CHG-002 evidence rather than a partially supported signal.
- `heat or gas generation relies entirely on removal capacity after triggering` is only partially supported for heat-removal dependence; gas generation is not stated.

Patch required:
- None.
- Monitoring note only: CHG-001 true-positive cases should not allow CHG-002 dosing-phase signals into inferred signals unless independently evidenced.

## OCP-MR-014

Status: Pass with minor warning

Model tested:
- Not specified

Pass basis:
- Correctly treated `CHG-001-CHARGING-SEQUENCE` as a review-domain snapshot rather than a positive-risk match.
- Correctly set `Risk-positive conclusion: no / uncertain`.
- Correctly did not treat catalyst-last addition as automatic `accumulation_then_trigger`, `reactive_inventory_before_trigger`, or `feed_rate_control_lost` evidence.
- Correctly listed no matched risk signals.
- Correctly preserved the exception boundary for Pd-catalyzed coupling where catalyst-last addition may be normal sequence form without high-rate, heat-release, gas-evolution, or scale-up sensitivity evidence.
- No SOP-like recommendation leakage.
- No non-canonical reasoning anchor introduced.
- No deterministic threshold misuse.

Warning:
- `reactive inventory exists before triggering` was placed under inferred / partially supported signals. The scenario supports pre-charged substrate/base inventory, but does not establish risk-relevant reactive inventory before trigger.
- `charging_sequence_risk` as a reasoning anchor is acceptable as review-domain rationale, but should not be treated as equivalent to positive accumulation-trigger anchors in false-positive cases.

Patch required:
- None.
- Monitoring note only: false-positive sequence cases may use `charging_sequence_risk` as review-domain rationale, but stronger positive anchors require direct evidence.

## OCP-MR-015

Status: Pass with minor warning

Model tested:
- Not specified

Pass basis:
- Correctly matched `CHG-002-ADDITION-MODE-AND-RATE` as the primary snapshot.
- Correctly kept `MIX-001-MIXING-TIME-SCALE-FAILURE` and `THR-001-THERMAL-CONTROL-AUTHORITY` as secondary manifestation domains.
- Correctly set `Risk-positive conclusion: yes` based on nominal dosing decoupling from effective material entry.
- Correctly identified direct CHG-002 risk signals: nominal dosing profile differs from effective material entry profile, material forms floating or foaming layer before entering reaction mass, and unreacted inventory accumulates despite nominally controlled dosing.
- Correctly interpreted abrupt heat release after entrainment as consequence of hidden unreacted inventory rather than primary THR-001.
- Correctly excluded CHG-001 primary attribution because the scenario explicitly states the charging sequence itself was not accumulation-before-trigger.
- No SOP-like recommendation leakage.
- No non-canonical reasoning anchor introduced.
- No deterministic threshold misuse.

Warning:
- The user label said this was TC-014, but the content is clearly `OCP-MR-015`; this result should be archived under OCP-MR-015.
- `rate_matching_review_required` was placed under inferred / partially supported signals, but it is a review-trigger label rather than a risk signal.
- `dosing_inertia` was listed as a reasoning anchor, but the scenario does not directly establish line holdup, control delay, system inertia, or continued entry after a stop command. It would be better treated as weakly inferred or not listed.

Patch required:
- None.
- Monitoring note only: review-trigger labels should not be listed as matched or inferred risk signals; weakly evidenced anchors should stay outside the positive reasoning-anchor list.

## OCP-MR-016

Status: Pass with warning

Model tested:
- Not specified

Pass basis:
- Correctly matched `CHG-002-ADDITION-MODE-AND-RATE` as the primary snapshot.
- Correctly kept `MIX-001-MIXING-TIME-SCALE-FAILURE` as checked-but-not-confirmed / secondary manifestation.
- Correctly set `Risk-positive conclusion: yes` based on the catalyst addition structure driving transient local high activity and side-product formation.
- Correctly used pathway restoration after changing effective catalyst addition structure, without changing main reactor mixing hardware, as evidence against core MIX-001 attribution.
- Correctly treated the apparent poor-mixing phenotype as secondary manifestation rather than confirmed mixing-time-scale failure.
- Correctly avoided listing `mixing_time_scale_failure` or `logical_lock_in` as positive reasoning anchors.
- No SOP-like recommendation leakage.
- No non-canonical reasoning anchor introduced.
- No deterministic threshold misuse.

Warning:
- `local reaction history forms before spatial homogenization` and `side reaction onset precedes completion of mixing` were placed under inferred / partially supported signals, but these are MIX-001 positive signals and the case is designed to exclude core MIX-001 because changing addition structure restores the pathway. They should be placed under excluded / not-established MIX-001 evidence.
- `phase transition or phase separation occurs near the dosing point` and `dosing entry point is located in low-momentum or low-exchange region` were also weakly supported at best.
- `rate_matching_failure` is acceptable but should remain secondary to the stronger directly supported anchors `nominal_vs_effective_dosing` and `secondary_mixing_manifestation`.

Patch required:
- Prompt patch, minor: signals from explicitly excluded or eliminated secondary snapshots should be placed under excluded / not-established evidence, not under inferred / partially supported signals, unless independently evidenced by the scenario.
- No taxonomy, JSONL, registry, schema, or source snapshot change.

## OCP-MR-017

Status: Pass with minor warning

Model tested:
- Not specified

Pass basis:
- Correctly matched `MIX-001-MIXING-TIME-SCALE-FAILURE` as the primary snapshot.
- Correctly treated `CHG-002-ADDITION-MODE-AND-RATE` as eliminated attribution and `THR-001-THERMAL-CONTROL-AUTHORITY` as not primary.
- Correctly set `Risk-positive conclusion: yes` based on local reaction history forming before homogenization and becoming non-recoverable by later controls.
- Correctly matched direct MIX-001 risk signals including local reaction history before spatial homogenization, side reaction onset before completion of mixing, failure of dosing-rate reduction, time extension amplifying side reactions, and non-recoverable local concentration history.
- Correctly used canonical reasoning anchors: `mixing_time_scale_failure`, `logical_lock_in`, `pre_homogenization_history_lock_in`, `control_authority_decay`, and `misallocated_control_authority`.
- Correctly avoided CHG-002-only review when dosing-rate adjustment had failed.
- Correctly avoided THR-001 attribution when the issue was observed before meaningful thermal excursion.
- No SOP-like recommendation leakage.
- No non-canonical reasoning anchor introduced.
- No deterministic threshold misuse.

Warning:
- `phenomenological mixing issue remains after CHG-002 dosing-rate explanation is eliminated` functions more as an attribution-test / boundary-justification phrase than as a process risk signal.
- `extending reaction time fails to recover intended pathway` is acceptable but largely overlaps with the directly matched signal `extending reaction time amplifies side reactions`.

Patch required:
- None.
- Monitoring note only: attribution-test labels should not be promoted into matched risk signals or new JSONL/taxonomy language.

## OCP-MR-018

Status: Pass

Model tested:
- Not specified

Pass basis:
- Correctly matched `THR-001-THERMAL-CONTROL-AUTHORITY` as the primary snapshot.
- Correctly excluded CHG-001, CHG-002, and MIX-001 because charging sequence, dosing mode, and mixing are explicitly controlled.
- Correctly set `Risk-positive conclusion: yes` based on temperature determining competing pathway dominance and selectivity.
- Correctly identified direct THR-001 risk signals: temperature change alters product composition or selectivity, temperature change alters dominance between competing pathways, extending time does not recover selectivity or pathway dominance, and cooling suppresses the desired catalytic or selective pathway.
- Correctly used canonical reasoning anchors: `thermal_control_authority`, `temperature_as_primary_authority`, `competing_pathway_authority`, and `control_authority_decay`.
- Correctly did not treat lower temperature as automatically safer or more selective.
- Correctly did not provide a temperature-program recommendation.
- No non-canonical reasoning anchor introduced.
- No deterministic threshold misuse.

Warning:
- None material.

Patch required:
- None.

## OCP-MR-019

Status: Pass

Model tested:
- Not specified

Pass basis:
- Correctly matched `CHG-001-CHARGING-SEQUENCE` as the primary snapshot.
- Correctly treated `THR-001-THERMAL-CONTROL-AUTHORITY` as explicitly excluded / manifestation only.
- Correctly set `Risk-positive conclusion: yes` for CHG-001, not for THR-001.
- Correctly identified direct CHG-001 risk signals: most or all reactants accumulated before reaction triggering, later initiation by heating / activation / catalyst addition, reactive inventory before triggering, and feed-rate control lost after triggering.
- Correctly used canonical reasoning anchors: `charging_sequence_risk`, `accumulation_then_trigger`, `reactive_inventory_before_trigger`, `feed_rate_control_lost`, and `control_authority_decay`.
- Correctly rejected temperature rise itself as sufficient evidence for THR-001 positive attribution.
- Correctly avoided listing `thermal_control_authority`, `temperature_as_primary_authority`, or `competing_pathway_authority` as positive anchors.
- No SOP-like recommendation leakage.
- No non-canonical reasoning anchor introduced.
- No deterministic threshold misuse.

Warning:
- None material.

Patch required:
- None.

## OCP-MR-020

Status: Pass with minor warning

Model tested:
- Not specified

Pass basis:
- Correctly matched `WRKUP-001-WORKUP-CONTROL-AUTHORITY` as the primary snapshot.
- Correctly kept `WRKUP-002-PARTITION-RATIO-DRIFT-INVENTORY-CONTROL` as secondary only if later phase redistribution, Kd drift, speciation-driven partition change, rag/emulsion inventory, or reactive-wash-as-partition evidence is supplied.
- Correctly set `Risk-positive conclusion: yes` based on residual reactive organometallic species after nominal HPLC completion and missing evidence of chemical deactivation.
- Correctly identified the central WRKUP-001 risk signals: primary reaction nominally stopped but reactive species remain, reaction end state is not chemically stable final state, stable final state requires a quench reaction, quench agent added is treated as termination criterion, and final pH is used as sole quench criterion.
- Correctly used canonical reasoning anchors: `workup_as_termination_control`, `reaction_end_state_not_final_state`, `quench_reaction_completion`, `chemically_incomplete_quench`, and `control_authority_decay`.
- Correctly did not treat water addition or final pH as quench completion evidence.
- Correctly did not classify the case as ordinary workup cleanup or WRKUP-002 partition issue.
- No SOP-like recommendation leakage.
- No non-canonical reasoning anchor introduced.
- No deterministic threshold misuse.

Warning:
- `quench reaction has non-negligible kinetic time scale` was listed as matched, but the scenario does not directly provide kinetic time-scale data. It is better treated as inferred from side reaction continuing during workup.
- `critical_quench_window` is acceptable but somewhat boundary-adjacent; the scenario supports a reactive workup window before phase separation but does not fully specify early-quench / late-quench condition drift.
- `quench depends on temperature, pH, or phase conditions` and `early quench-stage conditions differ from late quench-stage conditions` are weakly supported and should remain at most uncertainty / partially supported items.

Patch required:
- None.
- Monitoring note only: WRKUP-001 positive cases should not automatically expand from incomplete quench evidence into kinetic-time-scale, phase-condition dependence, or early/late quench-stage drift unless scenario evidence supports those fields.

## OCP-MR-021

Status: Pass

Model tested:
- Not specified

Pass basis:
- Correctly treated `WRKUP-001-WORKUP-CONTROL-AUTHORITY` as review-domain snapshot only.
- Correctly set `Risk-positive conclusion: no`.
- Correctly did not treat ordinary water wash or salt removal as quench-control authority.
- Correctly listed no matched risk signals, no inferred / partially supported signals, and no reasoning anchors.
- Correctly did not list `workup_as_termination_control`, `chemically_incomplete_quench`, `critical_quench_window`, or `quench_reaction_completion` as positive anchors.
- Correctly kept WRKUP-002 secondary only if future evidence shows partition-ratio drift, target inventory redistribution, phase-environment drift, emulsion/rag-layer inventory, or related washing-sequence behavior.
- No SOP-like recommendation leakage.
- No non-canonical reasoning anchor introduced.
- No deterministic threshold misuse.

Warning:
- None material.

Patch required:
- None.

## Recommended follow-up patches

### Prompt patch

Add or strengthen the following rule in the machine-review test prompt:

> Signals belonging to explicitly excluded, eliminated, or manifestation-only secondary snapshots should be placed under excluded / not-established evidence, not under `Inferred or partially supported signals`, unless the scenario independently supports them. Review-trigger labels, attribution-test labels, and quantitative trigger-family labels should not be listed as matched risk signals or inferred risk signals.

### Integrity checklist patch

Add a corresponding watch item under section placement discipline:

> In robustness-test outputs, secondary-snapshot similarity signals must not be promoted into inferred signals when the scenario explicitly excludes that attribution. Boundary-test language such as eliminated attribution, manifestation only, review trigger required, or nearest allowed term is QA metadata, not machine-layer risk evidence.

### Machine change log note

Suggested entry:

> Completed upstream-control robustness testing v0.2 for OCP-MR-013 through OCP-MR-021. Overall result: passed with minor section-placement warnings. No taxonomy, JSONL, schema, registry, or source snapshot changes required. Minor prompt/checklist refinement recommended to prevent excluded secondary-snapshot signals and review-trigger labels from being placed under inferred / partially supported signals.
