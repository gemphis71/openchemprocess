# Machine Review Test Results v0.3 — TLC Evidence Authority

status: completed  
scope: TLC evidence admissibility / interpretability / permitted interpretation / decision latency  
test_range: OCP-MR-022 through OCP-MR-029  
result_type: robustness_checkpoint  

## Summary Judgment

The v0.3 TLC robustness cycle broadly passed with attribution-layer warnings. The Machine Reviewer consistently blocked the major prohibited conclusions: it did not treat TLC as a precise quantitative tool, did not convert blank lanes or starting-material disappearance into complete conversion, did not treat same Rf as definitive identity, did not treat TLC sample-quench success as process or workup-quench completion, did not promote candidate-only morphology terms into taxonomy, and did not provide SOP-like TLC operating recommendations.

The main residual weakness is attribution precision. When the correct governing snapshot was a more specific TLC layer — `TLC-001-SPOTTING-LAYOUT`, `TLC-PRE-002-SAMPLE-PREPARATION-GATE`, `TLC-DIAG-002-INTERPRETATION-PATHWAYS`, `TLC-META-001-EARLY-DIAGNOSTIC-VALUE-AND-LIMITS`, or `TLC-META-002-DECISION-LATENCY-AND-FEEDBACK-STRATEGY` — the model often collapsed the case into a broader generic gate such as `TLC-DIAG-001-INTERPRETABILITY-GATE` or `TLC-PRE-000-APPLICABILITY-STABILITY`. This did not usually produce wrong chemical conclusions, but it reduces machine-layer attribution stability and should be tracked in future tests.

Patch decision:

- No taxonomy update required.
- No JSONL update required.
- No source snapshot update required.
- No schema update required.
- Optional prompt wording patch only: future TLC tests should instruct the reviewer to select the narrowest governing snapshot and avoid collapsing meta-level, pathway-level, layout-level, or preparation-level boundaries into generic TLC gates.

---

## OCP-MR-022

Status: Pass with minor warning

Model tested:
- Not specified

Pass basis:
- Correctly matched `TLC-PRE-000-APPLICABILITY-STABILITY` as the primary review domain.
- Correctly separated review-domain match from risk-positive conclusion.
- Correctly treated the direct spotting of a low-temperature, highly reactive intermediate onto silica at room temperature as a sample-state projection risk.
- Correctly blocked the claimed inference that the intermediate survived sampling or that conversion was high.
- Correctly avoided SOP-like quench or spotting recommendations.

Warning:
- Minor warning: `TLC-PRE-002-SAMPLE-PREPARATION-GATE` could have been listed as a secondary snapshot because the scenario explicitly states that no quench or derivatization was performed before spotting. The model was conservative and did not mark it as secondary, but this did not affect the primary judgment.

Patch required:
- None.

---

## OCP-MR-023

Status: Pass

Model tested:
- Not specified

Pass basis:
- Correctly matched `TLC-PRE-001-REPRESENTATIVENESS-SAMPLING` as the primary review domain.
- Correctly identified the clear-supernatant-only TLC as liquid-phase-specific evidence in a heterogeneous solid-liquid slurry.
- Correctly blocked the inference from weak starting material in the supernatant to high total batch conversion or low total starting-material inventory.
- Correctly separated matched risk signals from inferred or partially supported signals.
- Correctly preserved uncertainty by not claiming that total conversion was definitely low.

Warning:
- None material.

Patch required:
- None.

---

## OCP-MR-024

Status: Pass with minor warning

Model tested:
- Not specified

Pass basis:
- Correctly matched `TLC-DIAG-001-INTERPRETABILITY-GATE` as the primary review domain.
- Correctly identified missing solvent-front marking, origin-locked starting-material reference, absence of a definable migration center, and unanchored high-Rf sample spots as interpretability and anchoring failures.
- Correctly blocked the inference that sample-spot migration compensates for starting-material reference failure.
- Correctly avoided entering `TLC-DIAG-002` interpretation after interpretability was revoked.

Warning:
- Minor warning: secondary linkage to `TLC-000-ORIGIN-LINE`, `TLC-003-ELUENT-SELECTION`, and candidate-only `TLC-DIAG-EX-005` was under-recognized. This reflects conservative secondary attribution rather than incorrect primary judgment.

Patch required:
- None.

---

## OCP-MR-025

Status: Pass with warning

Model tested:
- Not specified

Pass basis:
- Correctly blocked the claim that a blank sample lane proves reaction completion.
- Correctly identified missing co-spot anchoring, high-Rf starting-material reference, and edge diffusion as sufficient to invalidate strong completion inference.
- Correctly treated `Rf > 0.8` as a TLC-specific compression trigger rather than a universal analytical rule.
- Correctly avoided SOP-like layout reconstruction recommendations.

Warning:
- Material attribution warning: the expected primary snapshot was `TLC-001-SPOTTING-LAYOUT`, but the model selected `TLC-DIAG-001-INTERPRETABILITY-GATE`. The conclusion was correct, but the attribution layer was too downstream. This case was intended to test whether reference-layout validity and co-spot anchoring can be recognized as the governing upstream failure before generic interpretability failure.
- Minor warning: key anchors such as `reference_layout_validity`, `co_spot_anchoring`, `matrix_shift_compensation`, `identity_consistency_check`, and `prohibited_quantitative_conversion` were underused.

Patch required:
- None for taxonomy, JSONL, source snapshots, or schema.
- Optional prompt wording patch: emphasize selection of the narrowest governing snapshot.

---

## OCP-MR-026

Status: Pass with warning

Model tested:
- Not specified

Pass basis:
- Correctly blocked the claim of `100% conversion` from absence of a visible starting-material spot.
- Correctly rejected the use of TLC as a replacement for HPLC or other confirmatory analytical methods at late-stage / trace-level residual scale.
- Correctly treated `<3%` as an evidence-sufficiency issue rather than a deterministic pass/fail threshold.
- Correctly preserved uncertainty: the model did not claim that actual conversion was not complete, only that TLC did not prove it.

Warning:
- Material attribution warning: the expected primary snapshot was `TLC-META-001-EARLY-DIAGNOSTIC-VALUE-AND-LIMITS`, but the model selected `TLC-DIAG-001-INTERPRETABILITY-GATE`. The model reached the correct blocked conclusion but under-attributed the problem to a generic diagnostic gate rather than the meta-level diagnostic authority boundary.
- Material warning: key anchors such as `diagnostic_value_boundary`, `late_stage_interpretability_downgrade`, `pseudo_completion_risk`, `resolution_scale_mismatch`, and `prohibited_quantitative_conversion` were not used.

Patch required:
- None for taxonomy, JSONL, source snapshots, or schema.
- Optional prompt wording patch: when the scenario concerns late-stage confirmation, trace residuals, final-state evidence, or regulatory / release-style claims, prefer `TLC-META-001` over generic interpretability gates.

---

## OCP-MR-027

Status: Pass with warning

Model tested:
- Not specified

Pass basis:
- Correctly blocked the conclusion that same Rf under UV proves sample/reference identity.
- Correctly treated divergent iodine and chemical-stain responses as uncertainty for identity interpretation.
- Correctly avoided claiming definite structural difference, purity, or single-component status.
- Correctly avoided SOP recommendations and morphology-term promotion.

Warning:
- Material attribution warning: the expected primary snapshot was `TLC-DIAG-002-INTERPRETATION-PATHWAYS`, but the model selected `TLC-DIAG-001-INTERPRETABILITY-GATE`. The case was not primarily about whether the plate could enter interpretation; it was about what interpretation is permitted after signals exist.
- Material warning: the model underused `identity_consistency_check`, `co_elution_uncertainty`, `intensity_content_non_equivalence`, and `permitted_interpretation_pathway`, and used the broader `sample signal cannot be anchored or calibrated` signal instead of the more specific DIAG-002 co-elution / visualization-divergence signals.

Patch required:
- None for taxonomy, JSONL, source snapshots, or schema.
- Optional prompt wording patch: when the central issue is over-claiming identity, composition, purity, conversion, or structure from an interpretable TLC signal, prefer `TLC-DIAG-002` over `TLC-DIAG-001`.

---

## OCP-MR-028

Status: Pass with warning

Model tested:
- Not specified

Pass basis:
- Correctly blocked the inference that a clean ester-like spot after methanol TLC quench proves original reaction completion, workup-quench completion, or process termination.
- Correctly identified `WRKUP-001-WORKUP-CONTROL-AUTHORITY` as a secondary concern for batch quench-completion evidence sufficiency.
- Correctly avoided converting MeOH quench, acid chloride derivatization, or TECH recipe content into SOP or formal Machine Reviewer rules.
- Correctly preserved uncertainty: the model did not assert that the actual workup quench was incomplete, only that the evidence did not prove completion.

Warning:
- Material attribution warning: the expected primary snapshot was `TLC-PRE-002-SAMPLE-PREPARATION-GATE`, but the model selected `TLC-PRE-000-APPLICABILITY-STABILITY`. The case was primarily about controlled sample preparation / derivatization and the boundary between analytical sample quench and process completion, not spontaneous sample instability during TLC exposure.
- Minor warning: the key anchors `sample_preparation_gate` and `quench_requirement_check` were underused, while `sample transformation within TLC window` was used in a less precise way.

Patch required:
- None for taxonomy, JSONL, source snapshots, or schema.
- Optional prompt wording patch: when quench / derivatization is deliberately used to create a TLC-interpretable sample, prefer `TLC-PRE-002` as the governing snapshot and keep `TLC-TECH-001` candidate-only.

---

## OCP-MR-029

Status: Pass with warning

Model tested:
- Not specified

Pass basis:
- Correctly recognized that high-resolution, low-frequency LC-MS does not automatically replace high-frequency TLC situational awareness when the reaction state changes faster than LC-MS turnaround.
- Correctly treated the transient dark origin band as an early-warning / situational-awareness signal rather than definitive structure, impurity, or quantitative evidence.
- Correctly avoided claiming that TLC replaces LC-MS or compliance-grade precision analysis.
- Correctly avoided SOP recommendations and deterministic threshold misuse.

Warning:
- Material attribution warning: the expected primary snapshot was `TLC-META-002-DECISION-LATENCY-AND-FEEDBACK-STRATEGY`, but the model selected `TLC-PRE-000-APPLICABILITY-STABILITY`. The core problem was feedback-cycle mismatch and temporal aliasing, not sample instability within the TLC exposure window.
- Material warning: matched risk signals were from the wrong family. The directly supported signals should have been `precision analysis feedback cycle is slower than reaction state transition`, `system relies only on low-frequency high-precision analysis during dynamic stage`, `transient abnormal states may be missed due to decision latency`, and `unstructured visual anomalies are ignored because they are not predefined analytical peaks`.
- Minor warning: `misallocated_control_authority` was a reasonable cross-chapter analogy but less precise than the TLC-META-002 anchors `decision_latency_match`, `high_frequency_low_latency_feedback`, `multi_level_feedback_strategy`, `temporal_aliasing_risk`, `situational_awareness_branch`, and `precision_confirmation_branch`.

Patch required:
- None for taxonomy, JSONL, source snapshots, or schema.
- Optional prompt wording patch: when the scenario concerns monitoring frequency, feedback-cycle mismatch, transient states, or TLC-versus-LC-MS role separation, prefer `TLC-META-002` over TLC pre-observation gates.

---

## Cross-Case Failure Pattern

### 1. Correct blocked conclusions, weaker primary attribution

The model generally blocked the correct prohibited inferences. The main failure was not chemical judgment but primary-snapshot specificity. It often selected a broader generic TLC gate even when a narrower governance layer existed.

Observed attribution collapse patterns:

- `TLC-001-SPOTTING-LAYOUT` collapsed into `TLC-DIAG-001` in OCP-MR-025.
- `TLC-META-001` collapsed into `TLC-DIAG-001` in OCP-MR-026.
- `TLC-DIAG-002` collapsed into `TLC-DIAG-001` in OCP-MR-027.
- `TLC-PRE-002` collapsed into `TLC-PRE-000` in OCP-MR-028.
- `TLC-META-002` collapsed into `TLC-PRE-000` in OCP-MR-029.

This indicates that the model understands the broad TLC evidence-authority frame but does not yet reliably select the narrowest governing snapshot when the case involves meta authority, permitted interpretation, reference layout, or controlled sample-preparation boundaries.

### 2. Candidate-only boundary preserved

The model did not promote candidate-only diagnostic examples or TECH recipe terms into taxonomy or formal JSONL-level reasoning anchors. `TLC-DIAG-EX-*`, `TLC-002-SPOTTING-OPERATION`, and `TLC-TECH-001-QUENCH-RECIPES` remained non-indexed supporting structures in the adjudication. This is an important pass condition for long-term taxonomy stability.

### 3. SOP boundary preserved

The model did not provide TLC operating recommendations in the tested outputs. It did not prescribe co-spot reconstruction, eluent optimization, quench recipes, spotting techniques, or LC-MS/TLC procedural workflows. This confirms that the Machine Reviewer frame is mostly preserved.

### 4. TLC-specific triggers were not over-hardened

The model generally did not convert TLC-specific thresholds such as `Rf > 0.8`, trace residual levels, or feedback time mismatch into universal analytical rules. These were treated as review triggers or evidence-sufficiency signals rather than deterministic process rules.

---

## Recommended Prompt Patch — Optional

Future test prompts may add the following instruction:

```text
When multiple snapshots match, select the narrowest governing snapshot as primary. Do not collapse meta-level authority boundaries, permitted interpretation pathways, layout/reference failures, or sample-preparation gates into broader generic TLC-PRE or TLC-DIAG gates when a more specific snapshot directly governs the review question.

Use generic gates such as TLC-PRE-000 or TLC-DIAG-001 only when the core failure is actually sample-state admissibility or pre-interpretation data-object validity. If the case concerns late-stage TLC authority, decision latency, permitted identity/conversion interpretation, missing co-spot layout, or controlled derivatization/quench before TLC, prefer the corresponding specific snapshot.
```

This is a prompt-discipline patch only. It does not require changing machine taxonomy, JSONL entries, schema, source snapshots, or candidate annotations.

---

## Final Assessment

v0.3 TLC robustness testing passes as a machine-review behavior checkpoint with attribution-layer warnings. The current TLC machine layer is strong enough to block major evidence-authority overclaims and SOP drift. The next improvement target is primary-snapshot specificity, especially for `TLC-META-001`, `TLC-META-002`, `TLC-DIAG-002`, `TLC-PRE-002`, and `TLC-001`.

Recommended next action:

- Save this file as `03_machine/machine_review_test_results_v0.3_tlc.md`.
- Add one change-log entry noting that v0.3 TLC robustness results were completed.
- Do not update taxonomy, JSONL, schema, registry, or source snapshots based on this cycle.
