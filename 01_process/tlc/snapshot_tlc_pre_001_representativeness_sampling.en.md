---
snapshot_id: "TLC-PRE-001-REPRESENTATIVENESS-SAMPLING"
status: "stable"
technique: "Thin Layer Chromatography"
topic: "Entry Gate: Representativeness & Sampling"
dependencies: ["TLC-PRE-000-APPLICABILITY-STABILITY"]
priority: "High"
---

# TLC-PRE-001 Representativeness & Sampling Gate

## 1. Gate Definition
This Gate is used during the sampling stage to determine: **Whether the micro-sample intended for spotting truly represents the overall physical phase and composition of the reaction system.**

## 2. Core Assumption: Equivalency
The validity of TLC relies on the following assumption: **Sample composition at the spotting point = Total composition of the reaction system.**
Heterogeneous systems are the primary source of disruption to this assumption.

---

## 3. Mandatory Decision Logic for Heterogeneous Systems

### 3.1 Phase Separation Rule
- **Multi-phase Systems**: For solid-liquid or liquid-liquid systems, phases **must be spotted separately** (sampled individually) as a matter of principle.
- **Risk Warning**: "Mixed sampling" under high-speed stirring is generally non-representative. Such results should only be used as rough qualitative references, as they easily lead to directional errors in composition ratio.

### 3.2 Exemption Criteria: Irrelevant Phase Logic
Mixed sampling or single-phase sampling is permissible if the following conditions are met:
- The solid or second liquid phase is confirmed to be an **inert component** (e.g., inorganic salt precipitates, immiscible solvents).
- Target products and intermediates do not partition, adsorb, or react within the irrelevant phase.
- **Decision**: In this case, sampling bias does not constitute an informational misinterpretation.

### 3.3 High-Risk Alerts (Strictly Prohibited for Conversion Judgment)
TLC results will lead to systematic directional errors in the following scenarios:
- **Solubility Equilibrium Constraints**: Starting materials react while simultaneously dissolving.
- **Product Precipitation**: The product reaches saturation and precipitates during the reaction.
- **Surface Adsorption**: Components are strongly adsorbed onto catalysts (e.g., Pd/C) or inorganic supports, leading to artificially low liquid-phase signals.
- **Logical Conclusion**: In these cases, TLC represents only **"liquid-phase concentration changes"** rather than **"total conversion."**

---

## 4. Sampling Bias Management Principles

### 4.1 Statistical Sampling Recommendations (Scale-up Sampling)
When phase separation is impossible but qualitative monitoring is required, increase the sampling volume to reduce random error, followed by processing in `TLC-PRE-002-SAMPLE-PREPARATION-GATE`:
- **Laboratory Scale (≤1 L)**: Sample **1–5 mL** of the mixture.
- **Industrial Scale (≥1000 L)**: Sample **~1 L** of the mixture.



---

## 5. Gate Outputs

### ✅ Passed
- Sample possesses physical and proportional representativeness. Proceed to `TLC-PRE-002-SAMPLE-PREPARATION-GATE`.

### ⚠️ Conditional
- Sampling has only qualitative value. The experimental record must explicitly state: "Due to heterogeneity constraints, this TLC result is not used for quantitative conversion judgment."

### ❌ Failed
- Significant bias exists in the sampling process or phase monitoring is impossible. TLC results will lead to systematic misinterpretation; alternative analytical tools are required.

> **Core Motto**: The risk of TLC lies not in the "spotting," but in whether "this single drop represents the reaction."