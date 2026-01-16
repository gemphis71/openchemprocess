---
snapshot_id: "TLC-PRE-002-SAMPLE-PREPARATION-GATE"
status: "stable"
technique: "Thin Layer Chromatography"
topic: "Entry Gate: Sample Preparation & Quench"
dependencies:
  - "TLC-PRE-000-APPLICABILITY-STABILITY"
  - "TLC-PRE-001-REPRESENTATIVENESS-SAMPLING"
priority: "High"
---

# TLC-PRE-001 Sample Preparation & Quench Gate

## 1. Gate Definition
Provided that the sample has met the criteria for TLC applicability (TLC-PRE-000-APPLICABILITY-STABILITY) and representativeness (TLC-PRE-001-REPRESENTATIVENESS-SAMPLING), this Gate determines: **Whether the sample must undergo pre-processing (such as quenching, dilution, or matrix adjustment) within the "sampling → spotting → development" timeframe to prevent ongoing reaction or informational distortion caused by system factors.**

This Gate only adjudicates **Requirement / Permission / Prohibition**; it does not define specific operational methods (detailed procedures are covered in subsequent process documentation).

## 2. Implicit Time and Environmental Scales (Decision Basis)
All judgments are based on the following unavoidable experimental facts:
- **Time Scale**: Sampling → Spotting → Entry into the developing chamber typically takes **30–60 seconds**.
- **Environmental Factors**:
  - Rapid temperature rise to Room Temperature (RT).
  - Exposure to ambient air and humidity.
  - **Silica Surface Activity**: Contains mildly acidic silanol groups (Si–OH), which possess catalytic or reactive properties.

**If a sample undergoes non-negligible chemical changes within these scales, pre-processing is mandatory.**

---

## 3. Quench Decision Logic

### 3.1 Mandatory Quenching
If any of the following conditions are met, **spotting without quenching = Gate Failure**:
- Extremely fast reaction rates (half-life $t_{1/2}$ in minutes or faster).
- Presence of highly reactive intermediates (strong nucleophiles/electrophiles, organometallic species, active redox species).
- High sensitivity to trace moisture, protons, or thermal transitions to RT.

**Decision Conclusion**: TLC results without quenching merely reflect "stochastic transformations after spotting" and do not represent the true state of the reaction system.

### 3.2 Legal Quench Forms
When Section 3.1 is triggered, the following two forms are permitted:
- **In-situ (On-plate) Quench**: Only applicable for low concentrations where the quenching exotherm is negligible.
- **Ex-situ (In-vial) Rapid Quench**: Reacting with a quenching agent in a sampling vial prior to spotting.

### 3.3 Allowed without Quench
- The reaction has been clearly terminated or quenched.
- The sample is a thermodynamically stable product or intermediate inert to air and silica.

---

## 4. Concentration & Dilution Gate

### 4.1 Standard Working Window
- **0.1–0.5 M**: Regarded as the standard TLC concentration window. Direct spotting is permitted.

### 4.2 Mandatory Dilution
Dilution (or ex-situ quenching) is mandatory if:
- Reaction concentration is **≥ 0.5 M**.
- High concentration leads to suspension, overloading, or uncontrollable spot diameter.
- **Decision Conclusion**: Spotting without dilution = Gate Failure.

### 4.3 Constraints on In-situ Quenching
- **Mandatory Constraint**: On-plate quenching is only permitted for equivalent concentrations of **0.1–0.5 M**.
- For high-concentration systems, relying solely on in-situ quenching is prohibited (leads to incomplete quenching and "ghost spots"); ex-situ complete quenching is required.

---

## 5. Solvent and System Matrix Judgment

Pre-processing (e.g., evaporation, displacement, or neutralization) is mandatory if system factors significantly distort migration behavior (Rf shift, spot diffusion, severe tailing):

- **High-boiling/Highly Polar Solvents**: e.g., DMSO, DMF, NMP.
- **Interfering Components**: Free water, strong acids, or strong bases.
- **Compatibility Principle**: Solvents introduced during pre-processing must be compatible with the eluent; neutralization must maintain a homogeneous system. If pre-processing itself introduces uncontrollable precipitation or new reactions, TLC is no longer applicable.

---

## 6. Gate Outputs

### ✅ Passed
- The sample is chemically inert within the TLC timeframe, and system factors do not cause migration distortion. Proceed to `TLC-002-SPOTTING-OPERATION` (Physical Operation).

### ⚠️ Conditional
- Must undergo specific pre-processing (Quench/Dilution/Solvent Swap) before spotting. 
- **Cross-reference**: For specific chemical quench recipes (e.g., MeOH, AcOH), refer to **`TLC-TECH-001-QUENCH-RECIPES`**.
- Details must be noted in experimental records.

### ❌ Failed
- Continuous transformation or system-induced uncontrollable distortion. TLC use is prohibited.

> **Gate Motto**: The prerequisite for TLC is not "spotting well," but "ensuring that both chemistry and migration behavior are controlled the moment the sample hits the plate."