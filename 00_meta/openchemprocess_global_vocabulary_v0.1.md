# OpenChemProcess Global Vocabulary

Version: v0.1  
Status: working vocabulary  
Scope: cross-chapter terminology normalization  
Governance: vocabulary evolves with chapter development

This file defines canonical terminology used across the OpenChemProcess system.

Purpose:

- maintain machine parsing stability  
- improve expert readability  
- ensure semantic consistency across chapters  
- support future AI-assisted review and knowledge graph construction  

Only canonical terms defined here should be used across chapters unless a new concept is intentionally introduced.

---

## Usage Rule

Chapters should use canonical vocabulary defined in this file whenever applicable.

If a new concept appears during chapter writing:

1. the concept may be used locally within the chapter  
2. if the concept becomes cross-chapter relevant, it should be added to this vocabulary file in the next revision  

Vocabulary evolves gradually with the project.

---

# 1 Core Process Philosophy

| Term | Definition |
|-----|------------|
| Control Authority | The degree to which a process operator can still influence the system state. |
| Control Authority Decay | Progressive loss of control options as the process advances. |
| Irreversible Commitment Stage | A stage where the process trajectory cannot be easily reversed without major intervention. |
| Tolerance Envelope | The acceptable operating region where deviations remain recoverable. |
| Scale Sensitivity | Degree to which process behavior changes during scale-up. |

---

# 2 Inventory and Phase Logic

| Term | Definition |
|-----|------------|
| Inventory | Total quantity of material present in the system (product, impurities, solvents, reagents). |
| Inventory Redistribution | Movement of material between phases without net destruction or formation. |
| Partition Ratio (Kd) | Ratio describing distribution of species between phases. |
| Phase Environment | The chemical environment of a phase (solvent composition, ionic strength, pH, etc.). |
| Phase Environment Drift | Change in phase properties during processing. |

---

# 3 Solvent and Composition Evolution

| Term | Definition |
|-----|------------|
| Volatile Removal Trajectory (VRT) | Order and pattern by which volatile components leave during concentration. |
| Composition Evolution Path (CEP) | Trajectory describing how solvent composition changes during concentration. |
| Solvent Exchange | Replacement of one solvent with another through controlled evaporation and addition. |
| Early Solvent Exchange | Solvent replacement introduced before deep concentration occurs. |
| In-line Solvent Exchange | Continuous solvent replacement performed during concentration. |

---

# 4 Accumulation and Exposure

| Term | Definition |
|-----|------------|
| Nonvolatile Inventory (NV) | Species that remain and accumulate as solvent is removed. |
| Nonvolatile Accumulation | Concentration increase of NV species during solvent removal. |
| Thermal Exposure (TE) | Temperature × time × concentration trajectory experienced by the system. |
| Concentration Factor (CF) | Ratio of initial liquid volume to final liquid volume. |

---

# 5 Structural Metrics (Solid-State / Isolation-Relevant)

| Term | Definition |
|-----|------------|
| Wet Mass Ratio (WMR) | Ratio of wet cake mass to dry solid mass, reflecting mother liquor retention and solid-state packing structure. Measured at solid formation stage (crystallization/recrystallization) and used to predict downstream filtration behavior. |

---

# 5 Operational Constraints

| Term | Definition |
|-----|------------|
| Minimum Stirrable Volume | Lowest volume at which effective agitation is maintained in scale-up equipment. |
| Complete Dryness | State where essentially all solvent is removed. |
| Wet Product State | Isolation state where residual solvent remains intentionally. |
| Transfer Boundary | Operational boundary created by equipment limitations (discharge, slurry transfer, etc.). |

---

# 6 Process Design Routes

| Term | Definition |
|-----|------------|
| Route 1 — Product Disengagement | Strategy where the product leaves the reaction system early. |
| Route 2 — Concentration Reduction | Strategy focusing on lowering CF and reducing accumulation risk. |
| Route 3 — Concentration + Solvent Exchange | Strategy combining moderate concentration with solvent replacement. |

Priority order in workup design:

Route 1 > Route 2 > Route 3

---

# 7 Review and Audit Language

| Term | Definition |
|-----|------------|
| Soft Block | Review stop triggered by incomplete information or moderate risk. |
| Hard Block | Mandatory stop due to unacceptable or unassessed risk. |
| Override | Explicitly documented release of a block condition. |
| Audit Trace | Machine-readable record of review decisions. |

---

# 8 Safety Layer

| Term | Definition |
|-----|------------|
| Explosion Hazard Assessment | Formal safety evaluation of concentration hazards. |
| Peroxide Risk | Hazard caused by peroxide accumulation during solvent concentration. |
| Thermal Decomposition | Chemical degradation caused by heat exposure. |

---

End of vocabulary definition.
