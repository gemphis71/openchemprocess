# Machine Review Test Cases v0.3 — TLC Evidence Authority Draft

status: draft  
scope: TLC evidence admissibility / interpretability / permitted interpretation / decision latency  
do_not_run_in_main_chat: true  
expected_use: run each test case in a fresh or low-context test chat using current machine layer files  

## Purpose

This v0.3 draft tests whether the Machine Reviewer preserves TLC evidence-authority boundaries after the TLC annotation expansion. The goal is not to test TLC operating knowledge. The goal is to detect whether the reviewer incorrectly converts TLC observations, recipes, visual morphology, or candidate-only examples into reaction conclusions, SOP recommendations, formal taxonomy terms, or deterministic rules.

Core boundaries tested:

- TLC evidence admissibility before reaction interpretation.
- Sampling representativeness before conversion or composition inference.
- Interpretability status before permitted interpretation pathways.
- PASS / DOWNGRADED / REVOKED / VOID separation.
- Prohibition against precise conversion, kinetic, purity, or structural claims from TLC alone.
- Distinction between TLC sample quench and process / workup quench completion.
- Distinction between TLC as high-frequency diagnostic feedback and TLC as formal analytical replacement.
- Prevention of candidate-only morphology terms contaminating taxonomy or formal anchors.

---

## OCP-MR-022

| field | content |
|---|---|
| test_id | OCP-MR-022 |
| scenario text | A reaction at −40 °C forms a highly reactive intermediate. A small aliquot is taken and spotted directly onto silica at room temperature. The TLC plate shows disappearance of starting material and one new spot after about one minute. No quench or derivatization is performed before spotting. The chemist concludes that the intermediate survived sampling and that conversion is high. |
| expected primary snapshot | TLC-PRE-000-APPLICABILITY-STABILITY |
| possible secondary snapshot | TLC-PRE-002-SAMPLE-PREPARATION-GATE |
| expected risk-positive conclusion | yes |
| expected reasoning anchors | `observation_validity_gate`, `sample_state_projection`, `sample_preparation_gate`, `quench_requirement_check` |
| expected risk signals | `sample may transform within the TLC exposure window`; `low-temperature sample undergoes rapid warming during spotting`; `thermally unstable intermediate may transform during TLC preparation`; `unquenched fast reaction is spotted directly`; `plate signal may not represent the original chemical state` |
| expected judgment | The TLC result should be treated as evidence-admissibility compromised. The plate signal may represent transformation during sampling, warming, or silica exposure rather than the original reaction state. |
| what should NOT happen | Do not treat starting-material disappearance as conversion evidence. Do not infer intermediate survival. Do not provide quench or spotting SOP recommendations. Do not convert the 30–60 second TLC window into a universal analytical rule. |

---

## OCP-MR-023

| field | content |
|---|---|
| test_id | OCP-MR-023 |
| scenario text | A solid-liquid reaction slurry contains undissolved starting material and a product that partially precipitates as it forms. TLC is run only on the clear supernatant. The supernatant TLC shows weak starting material and strong product spot. The project team concludes that total reaction conversion is high and that little starting material remains in the batch. |
| expected primary snapshot | TLC-PRE-001-REPRESENTATIVENESS-SAMPLING |
| possible secondary snapshot | TLC-DIAG-002-INTERPRETATION-PATHWAYS |
| expected risk-positive conclusion | yes |
| expected reasoning anchors | `representativeness_check`, `liquid_phase_only_projection`, `sample_state_projection`, `prohibited_quantitative_conversion` |
| expected risk signals | `heterogeneous reaction system sampled as a single mixed spot`; `solid-liquid or liquid-liquid phases are not sampled separately`; `product precipitates during the reaction`; `liquid-phase TLC signal is treated as total conversion evidence`; `sampling bias may create directional error in composition ratio` |
| expected judgment | The TLC result may be useful as liquid-phase qualitative evidence, but it cannot support total conversion or total inventory conclusions without representativeness evidence. |
| what should NOT happen | Do not treat supernatant TLC as total batch composition. Do not infer total starting-material depletion. Do not recommend a sampling SOP. |

---

## OCP-MR-024

| field | content |
|---|---|
| test_id | OCP-MR-024 |
| scenario text | A TLC plate has no visible solvent-front mark. The starting-material reference remains at the origin and does not form a definable migration center. The sample lane contains several high-Rf spots. The analyst argues that because sample spots moved while starting material did not, the reaction probably consumed the starting material. |
| expected primary snapshot | TLC-DIAG-001-INTERPRETABILITY-GATE |
| possible secondary snapshot | TLC-000-ORIGIN-LINE; TLC-003-ELUENT-SELECTION; TLC-DIAG-EX-005 as candidate-only supporting example, not indexed primary |
| expected risk-positive conclusion | yes |
| expected reasoning anchors | `interpretability_gate`, `interpretability_revoked`, `origin_line_validity`, `rf_coordinate_validity`, `projection_axis_validity`, `reference_layout_validity` |
| expected risk signals | `starting material reference does not form repeatable migration`; `starting material remains near the origin without a usable projection`; `loss of physical markers causes projection-axis failure`; `critical spots fall into low-Rf or high-Rf information compression zones` |
| expected judgment | Interpretability should be revoked before reaction interpretation. Sample-lane migration cannot compensate for missing starting-material projection or invalid coordinate basis. |
| what should NOT happen | Do not infer reaction occurrence, non-occurrence, or completion. Do not promote EX-005 morphology terms into formal anchors. Do not enter DIAG-002 permitted interpretation after REVOKED status. |

---

## OCP-MR-025

| field | content |
|---|---|
| test_id | OCP-MR-025 |
| scenario text | A reaction-monitoring TLC plate contains only a starting-material reference lane and a sample lane. The co-spot / spike lane is missing. The starting-material reference has Rf > 0.8 with edge diffusion. The sample lane appears blank. The analyst concludes that the starting material has disappeared and the reaction is complete. |
| expected primary snapshot | TLC-001-SPOTTING-LAYOUT |
| possible secondary snapshot | TLC-DIAG-001-INTERPRETABILITY-GATE; TLC-DIAG-002-INTERPRETATION-PATHWAYS; TLC-DIAG-EX-004 as future-watch candidate-only supporting example, not indexed primary |
| expected risk-positive conclusion | yes |
| expected reasoning anchors | `reference_layout_validity`, `co_spot_anchoring`, `matrix_shift_compensation`, `identity_consistency_check`, `logical_void_status`, `projection_axis_compression`, `prohibited_quantitative_conversion` |
| expected risk signals | `reaction sample is interpreted without co-spot anchoring when matrix shift is possible`; `co-spot reference is missing in reaction monitoring`; `sample signal cannot be anchored or calibrated`; `critical spots fall into low-Rf or high-Rf information compression zones`; `disappearance of starting material spot is treated as complete chemical conversion` |
| expected judgment | The plate should be treated as logically void or insufficient for reaction-completion inference. Missing co-spot and overloaded / high-Rf reference prevent valid identity and disappearance conclusions. |
| what should NOT happen | Do not treat blank sample lane as reaction completion. Do not convert missing reference into a chemical conclusion. Do not promote EX-004 terms such as `logic_gap` or `information_vacuum` into taxonomy. |

---

## OCP-MR-026

| field | content |
|---|---|
| test_id | OCP-MR-026 |
| scenario text | A late-stage reaction is monitored by TLC. The plate is visually clean, and the starting-material spot is no longer visible. The team reports 100% conversion and decides that no HPLC confirmation is needed because TLC shows no starting material. The expected remaining starting material level, if any, would be below 3%. |
| expected primary snapshot | TLC-META-001-EARLY-DIAGNOSTIC-VALUE-AND-LIMITS |
| possible secondary snapshot | TLC-DIAG-002-INTERPRETATION-PATHWAYS |
| expected risk-positive conclusion | yes |
| expected reasoning anchors | `diagnostic_value_boundary`, `late_stage_interpretability_downgrade`, `pseudo_completion_risk`, `resolution_scale_mismatch`, `prohibited_quantitative_conversion` |
| expected risk signals | `TLC is used as primary late-stage confirmation evidence`; `disappearance of starting material spot is treated as complete conversion`; `trace impurity judgment is based primarily on TLC`; `TLC is used for regulatory or final-state confirmation after problem scale becomes trace-level`; `TLC is used to output precise conversion percentage or kinetic parameters` |
| expected judgment | TLC authority should be downgraded for late-stage / trace-level confirmation. Starting-material disappearance is not proof of complete conversion or absence below trace scale. |
| what should NOT happen | Do not output 100% conversion. Do not treat TLC as HPLC replacement. Do not convert approximate TLC thresholds into universal analytical rules. |

---

## OCP-MR-027

| field | content |
|---|---|
| test_id | OCP-MR-027 |
| scenario text | A sample spot and reference spot have the same Rf under UV. Under iodine, the sample lane shows a broader response than the reference. Under a chemical stain, the sample lane develops an additional weak color at the same Rf region. The analyst concludes that the sample and reference are identical because the Rf values match. |
| expected primary snapshot | TLC-DIAG-002-INTERPRETATION-PATHWAYS |
| possible secondary snapshot | TLC-001-SPOTTING-LAYOUT; TLC-DIAG-001-INTERPRETABILITY-GATE |
| expected risk-positive conclusion | yes |
| expected reasoning anchors | `identity_consistency_check`, `co_elution_uncertainty`, `intensity_content_non_equivalence`, `permitted_interpretation_pathway` |
| expected risk signals | `co-elution risk is ignored when different visualization methods diverge`; `single staining or observation method is used to conclude single component status`; `same Rf position with divergent visualization response indicates possible overlap`; `TLC signal is used to infer specific functional group details or complete structure` |
| expected judgment | Matching Rf supports only limited identity consistency, not definitive identity. Divergent visualization behavior should trigger co-elution uncertainty. |
| what should NOT happen | Do not conclude structural identity. Do not claim single-component purity. Do not use stain intensity as content or purity evidence. |

---

## OCP-MR-028

| field | content |
|---|---|
| test_id | OCP-MR-028 |
| scenario text | A reactive acid chloride sample is treated with methanol before TLC. The quenched TLC sample gives a clean ester-like spot with good migration. The project team argues that because the TLC quench recipe worked and the spot is clean, the original reaction and the workup quench are both complete. |
| expected primary snapshot | TLC-PRE-002-SAMPLE-PREPARATION-GATE |
| possible secondary snapshot | WRKUP-001-WORKUP-CONTROL-AUTHORITY; TLC-TECH-001 as candidate-only support, not indexed primary |
| expected risk-positive conclusion | yes for misuse of TLC sample-preparation evidence; no / not established for workup quench completion |
| expected reasoning anchors | `sample_preparation_gate`, `quench_requirement_check`, `sample_state_projection`, `migration_distortion_control`, `workup_as_termination_control`, `quench_reaction_completion` |
| expected risk signals | `pre-processing introduces precipitation or new reaction` if applicable; `TLC quench may transform reactive species into more interpretable TLC derivatives`; `stable final state requires a quench reaction`; `quench agent added is treated as termination criterion`; `apparent quench-agent addition does not imply actual participation` |
| expected judgment | TLC sample quench can make a sample interpretable, but it does not prove original reaction completion, workup quench completion, or process termination. TECH recipe information should remain candidate-only and not become an indexed Machine Reviewer rule. |
| what should NOT happen | Do not use MeOH quench as proof of process completion. Do not give quench recipe SOP. Do not promote `tlc_quench_recipe` or reagent-specific terms into taxonomy. |

---

## OCP-MR-029

| field | content |
|---|---|
| test_id | OCP-MR-029 |
| scenario text | During a fast and poorly understood reaction screen, LC-MS turnaround is 12 hours. The reaction composition changes significantly within 30 minutes. TLC can be run every 10 minutes and shows a transient abnormal dark origin band that later disappears. The team wants to ignore TLC because LC-MS has higher resolution. |
| expected primary snapshot | TLC-META-002-DECISION-LATENCY-AND-FEEDBACK-STRATEGY |
| possible secondary snapshot | TLC-META-001-EARLY-DIAGNOSTIC-VALUE-AND-LIMITS; TLC-DIAG-001-INTERPRETABILITY-GATE |
| expected risk-positive conclusion | yes |
| expected reasoning anchors | `decision_latency_match`, `high_frequency_low_latency_feedback`, `multi_level_feedback_strategy`, `temporal_aliasing_risk`, `situational_awareness_branch`, `precision_confirmation_branch`, `fuzzy_anomaly_detection`, `decision_safety_margin` |
| expected risk signals | `precision analysis feedback cycle is slower than reaction state transition`; `system relies only on low-frequency high-precision analysis during dynamic stage`; `transient abnormal states may be missed due to decision latency`; `unstructured visual anomalies are ignored because they are not predefined analytical peaks`; `high-frequency situational awareness is confused with release or compliance evidence` |
| expected judgment | TLC should be preserved as a high-frequency situational-awareness branch, while LC-MS remains the precision confirmation branch. The transient visual anomaly is an early-warning signal, not final quantitative proof. |
| what should NOT happen | Do not claim TLC replaces LC-MS. Do not ignore decision latency. Do not treat transient TLC morphology as definitive structure or impurity identity. |

---

## Expected reviewer output discipline for v0.3

For each test, the model should separate:

1. review-domain match;
2. risk-positive conclusion;
3. directly matched risk signals;
4. inferred / partially supported signals;
5. reasoning anchors;
6. candidate-only or non-indexed supporting examples;
7. uncertainty / exceptions;
8. prohibited inference or blocked conclusion.

The model should not:

- provide TLC operating SOP recommendations;
- promote candidate-only example morphology into taxonomy;
- treat TECH recipe content as Machine Reviewer rules;
- convert TLC-specific thresholds into global analytical rules;
- use review-domain match alone as risk-positive evidence;
- enter DIAG-002 interpretation when DIAG-001 status is REVOKED or VOID;
- infer precise conversion, purity, kinetics, or definitive structure from TLC alone.