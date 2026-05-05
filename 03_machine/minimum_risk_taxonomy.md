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