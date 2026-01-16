---
snapshot_id: "TLC-PRE-000-APPLICABILITY-STABILITY"
status: "stable"
technique: "Thin Layer Chromatography"
topic: "Entry Gate: Stability and Applicability"
dependencies: []
priority: "Critical"
---

# TLC-PRE-000 Applicability & Stability Gate

## 1. Gate Definition
This Gate is used to evaluate the survival status of a sample within the specific physicochemical environment of TLC before any operation. The core objective is to determine: **Whether the signal presented on the plate is still a true projection of its original chemical state.**

## 2. Inherent Assumptions & Constraints
Using TLC implies that the sample is inevitably exposed to the following three dimensions:

### 2.1 Time Scale
- **Exposure Window**: The standard duration from sampling and spotting to being placed in the developing chamber is **30–60 seconds**.
- **Logical Implication**: If the half-life ($t_{1/2}$) of a chemical transformation is significantly shorter than this window, TLC will fail to capture the true initial state.

### 2.2 Physicochemical Environment
- **Stationary Phase Activity**: The silica gel surface contains mildly acidic silanol groups (Si–OH).
- **Co-existing Factors**: Trace moisture and oxygen from the atmosphere.
- **Risks**: High probability of acid-catalyzed decomposition, adsorptive rearrangement, or oxidation.

### 2.3 Thermal Jump (Temperature Transition)
- **Phenomenon**: When a low-temperature (e.g., -78°C) reaction solution is spotted, the sample temperature **rapidly rises to Room Temperature (RT)**.
- **Risks**: Thermally unstable intermediates may undergo irreversible transformation during this rapid warming process.

---

## 3. Decision Checklist

### Q1 | Is the sample chemically stable within the TLC time scale?
- ✅ **Yes**: Composition remains essentially constant within 60 seconds.
- ❌ **No**: Significant decomposition or reaction occurs within this timeframe.

### Q2 | Is the sample sensitive to silica, moisture, or mild acidity?
- ✅ **Yes**: Insensitive to the factors mentioned above.
- ⚠️ **Conditional**: Contains reactive functional groups (e.g., acid chlorides, anhydrides) that require pre-processing.
- ❌ **No**: Highly unstable and cannot be bypassed by standard means.

### Q3 | Is the system in a "rapidly evolving" state?
- ✅ **Yes**: Slow reaction system ($t_{1/2} \ge 1 \text{ h}$), can be treated as quasi-static.
- ⚠️ **Conditional**: Fast reaction or contains active intermediates requiring quenching/derivatization.
- ❌ **No**: Reaction continues on the plate, leading to untrustworthy results.

---

## 4. Gate Outputs

### ✅ Passed: Proceed with TLC
- All questions answered with "Yes". Proceed to the `TLC-000` series.

### ⚠️ Conditional: Pre-processing Required
- Reactive components are present. The sample must undergo "Quenching" or "Derivatization" before spotting (refer to `TLC-PRE-002`).

### ❌ Failed: TLC Prohibited
- Irreconcilable conflict between the sample and the TLC environment. Alternative analytical tools (e.g., HPLC, GC, or NMR) must be selected.

> **Core Motto**: Deciding whether to perform TLC is not about whether you *can* spot the sample, but whether the chemistry on the plate remains the *original* chemistry.