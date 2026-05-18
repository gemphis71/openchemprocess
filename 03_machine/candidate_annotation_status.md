# Candidate Annotation Status

status: working governance note  
purpose: track candidate-only machine annotations that intentionally remain outside the formal JSONL index and annotation registry  
scope: TLC operation-heavy, diagnostic-example, and TECH toolbox files  
last_updated: 2026-05-17  

## Governance rule

Candidate-only annotations are source-level review notes, not formal machine-index entries. They may appear at the end of source snapshots as `Machine Annotation Candidate` blocks, but they must not be added to `openchemprocess_index.jsonl.md`, must not receive `completed / added` rows in `annotation_registry.md`, and must not promote example-specific morphology, operation, or recipe terms into taxonomy. Candidate-only files may be cited as supporting examples during human review, but they should not be treated as primary indexed snapshots unless a later explicit promotion decision creates a JSONL entry and registry row.

## Current candidate-only files

| canonical_id | source files | candidate scope | current status | reason not indexed | future watch status | prohibited promotion |
|---|---|---|---|---|---|---|
| TLC-002-SPOTTING-OPERATION | `01_process/tlc/snapshot_tlc_002_spotting_operation.zh.md` / `01_process/tlc/snapshot_tlc_002_spotting_operation.en.md` | operation_validity_candidate | candidate_only_not_indexed | The source contains useful review logic around spatial signal encoding, spot-size distortion, overload, drying completeness, and lateral drift, but it remains operation-heavy and includes capillary size, spotting motion, re-spotting limits, drying method, and concentration recommendations. | Reconsider only if later diagnostic examples repeatedly reuse spotting-related validity logic as review boundaries rather than operating instructions. | Do not promote capillary size, spotting motion, re-spotting limits, drying method, concentration recommendations, or `spatial_signal_encoding` terms into Machine Reviewer SOP or formal taxonomy. |
| TLC-DIAG-EX-001-FRONTING-BAND-AND-BASELINE-COMPRESSION | `01_process/tlc/snapshot_tlc_diag_ex_001_fronting_band_and_baseline_compression.zh.md` / `01_process/tlc/snapshot_tlc_diag_ex_001_fronting_band_and_baseline_compression.en.md` | diagnostic_example_candidate | candidate_only_not_indexed | The example reuses `interpretability_gate`, `interpretability_revoked`, and `data_object_boundary`, but the new content is mainly example-specific morphology such as fronting band, low-Rf crowding, baseline tailing, and projection-axis compression. | Watch for repeated cross-example use of projection-axis compression / fronting-band logic before promotion. | Do not promote `fronting_band`, `baseline_compression`, `axis_compression`, `projection_axis_compression`, or similar morphology terms from this single example into formal taxonomy. |
| TLC-DIAG-EX-002-OVERLOAD-AND-SOLVENT-CARRYOVER | `01_process/tlc/snapshot_tlc_diag_ex_002_overload_and_solvent_carryover.zh.md` / `01_process/tlc/snapshot_tlc_diag_ex_002_overload_and_solvent_carryover.en.md` | diagnostic_example_candidate | candidate_only_not_indexed | The example reuses `interpretability_revoked` for systemic physical plate failure, but the new content is mainly example-specific morphology and cause terms such as overload, solvent carryover, full-path streaking, and boundary annihilation. | Watch for repeated cross-example use of overload / solvent-carryover as review boundaries, not as TLC troubleshooting recipes. | Do not promote `spotting_overload`, `solvent_carryover`, `full_path_streaking`, `boundary_annihilation`, or recipe-like corrective logic into taxonomy or Machine Reviewer instructions. |
| TLC-DIAG-EX-003-LOW-RF-TRIANGULAR-TAILING-SURFACE-INTERACTION | `01_process/tlc/snapshot_tlc_diag_ex_003_low_rf_triangular_tailing_surface_interaction.zh.md` / `01_process/tlc/snapshot_tlc_diag_ex_003_low_rf_triangular_tailing_surface_interaction.en.md` | diagnostic_example_candidate | candidate_only_not_indexed | The example reuses `interpretability_downgraded`, `projection_axis_validity`, `non_inferable_zone`, and `surface_interaction_decoupling`, but the new content is low-Rf triangular or flame-like tailing morphology. | Watch for repeated reuse of surface-interaction morphology as a review category beyond current gate-level anchors. | Do not promote `low_rf_triangular_tailing`, `flame_like_tailing`, `adsorption_dominated_migration`, or acid/base modifier examples into taxonomy or SOP recommendations. |
| TLC-DIAG-EX-004-LOGIC-GAP-MISSING-SPIKE-AND-FRONTING-OVERFLOW | `01_process/tlc/snapshot_tlc_diag_ex_004_logic_gap_missing_spike_and_fronting_overflow.zh.md` / `01_process/tlc/snapshot_tlc_diag_ex_004_logic_gap_missing_spike_and_fronting_overflow.en.md` | diagnostic_example_candidate | candidate_only_not_indexed | The example strongly reuses `reference_layout_validity`, `co_spot_anchoring`, `identity_consistency_check`, `logical_void_status`, and `prohibited_quantitative_conversion`, but it is still a single diagnostic example and includes reconstruction / corrective-action language. | Future sub-snapshot watch. This is the highest-priority candidate for possible later promotion if repeated cases confirm missing-reference logical-void value. | Do not promote `logic_gap`, `information_vacuum`, `anchoring_failure`, `measurement_design_layer_failure`, or reconstruction actions into formal taxonomy or SOP. |
| TLC-DIAG-EX-005-STARTING-MATERIAL-STAGNATION-AND-POLARITY-GAP | `01_process/tlc/snapshot_tlc_diag_ex_005_starting_material_stagnation_and_polarity_gap.zh.md` / `01_process/tlc/snapshot_tlc_diag_ex_005_starting_material_stagnation_and_polarity_gap.en.md` | diagnostic_example_candidate | candidate_only_not_indexed | The example reuses `interpretability_revoked`, `origin_line_validity`, `rf_coordinate_validity`, `projection_axis_validity`, and `reference_layout_validity`, but the new content is starting-material stagnation / polarity-gap morphology. | Watch only if later cases repeatedly show starting-material projection failure as a reusable subcategory. | Do not promote `starting_material_projection_failure`, `starting_material_stagnation`, `polarity_gap`, or recovery actions into taxonomy or Machine Reviewer instructions. |
| TLC-TECH-001-QUENCH-RECIPES | `01_process/tlc/snapshot_tlc_tech_001_quench_recipes.zh.md` / `01_process/tlc/snapshot_tlc_tech_001_quench_recipes.en.md` | technical_recipe_candidate | candidate_only_not_indexed | The file is a TECH toolbox that supports TLC sample-preparation decisions after `TLC-PRE-002`; it contains reagent-specific recipes and operation boundaries, so it should not become a Machine Reviewer rule source. | No promotion unless future review extracts a non-recipe, cross-snapshot review boundary beyond recipe execution itself. | Do not promote MeOH, EtOH, ammonia, amines, AcOH, AcOH/MeOH, hydride-quench examples, or `tlc_quench_recipe` terms into taxonomy; do not treat TLC sample quench as process or workup quench completion evidence. |

## Current formal-index boundary

The formal machine index should include only completed JSONL entries with corresponding registry rows. Candidate-only files listed here should remain absent from:

- `03_machine/openchemprocess_index.jsonl.md`
- completed / added rows in `03_machine/annotation_registry.md`
- formal or candidate taxonomy promotion sections, unless a later explicit promotion decision is recorded

## Promotion criteria

A candidate-only file may be considered for promotion only if all of the following conditions are met:

1. The candidate contributes a reusable review boundary that is not already captured by an existing formal snapshot.
2. The reusable boundary appears across multiple source examples or is explicitly elevated by a source snapshot, not only by model output.
3. The promoted term can be expressed as Machine Reviewer behavior rather than operation, recipe, troubleshooting, or SOP guidance.
4. The promotion creates a JSONL entry, registry row, taxonomy delta, and machine change log entry in the same batch.
5. The promotion does not convert TLC-specific parameters, morphology descriptions, or recipe details into global analytical rules.

## Non-promotion defaults

Unless explicitly promoted later, candidate-only content should be interpreted as:

- supporting example, not primary indexed snapshot;
- source-level review note, not machine-index entry;
- watchlist vocabulary, not taxonomy term;
- boundary reinforcement, not SOP recommendation;
- evidence-governance context, not deterministic operating rule.
