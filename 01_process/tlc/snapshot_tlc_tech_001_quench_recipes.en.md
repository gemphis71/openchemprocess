---
snapshot_id: "TLC-TECH-001-QUENCH-RECIPES"
status: "stable"
layer: "TECH"
technique: "Thin Layer Chromatography"
topic: "Standardized Quench Recipes for TLC"
dependencies:
  - "TLC-PRE-002-SAMPLE-PREPARATION-GATE"
used_by:
  - "TLC-002-SPOTTING-OPERATION"
priority: "High"
---

# TLC-TECH-001 Quench Recipes for TLC (Toolbox)

## 0. Scope

This document defines a set of **reusable and predictable TLC quench recipes**. It serves as a **Toolbox (TECH)** module, where the invocation logic is determined by PRE gates, and physical execution is defined by PROCESS operational standards.

---

## 1. Core Chemical Logic: Quenching as Derivatization

TLC quenching is performed not only to "stop the reaction" but also to **proactively adjust $R_f$ values**:
- **Decrease Polarity (Increase $R_f$)**: Convert active electrophiles into esters using alcohols.
- **Increase Polarity (Decrease $R_f$)**: Convert active electrophiles into amides or ureas using ammonia/amines.

---

## 2. Alcohol & Amine Recipe Families (Electrophile Capture)

### 2.1 Alcohol-based Quench
- **Applicability**: Acid chlorides, anhydrides, isocyanates, etc.
- **Recipe**: Anhydrous MeOH (Preferred) or Anhydrous EtOH.
- **Rationale**: Generates thermodynamically stable esters or carbamates, typically resulting in rounded spot shapes and moderate mobility.

### 2.2 Amine-based Quench
- **Applicability**: Highly reactive electrophilic intermediates.
- **Recipe**: Ammonia solution (saturated $NH_3$) or low-molecular-weight primary/secondary amines.
- **Rationale**: Generates amides or ureas. Due to hydrogen bonding, the product polarity is significantly higher than that of corresponding esters, preventing components from running with the solvent front.

---

## 3. Weak Acid & Reductive System Handling

### 3.1 Weak Acid Family (Protonation)
- **Applicability**: Grignard reagents, organolithiums, and strongly basic systems.
- **Recipe**: **Glacial Acetic Acid (AcOH)** or 10% AcOH/MeOH.
- **Operational Standard (In-situ)**: Must follow the **"reagent first, then sample"** sequence. Pre-wet the silica spotting site with the acid to ensure immediate protonation upon sample entry.

### 3.2 Strong Reductive Systems (Hydride Quench)
- **Applicability**: $NaBH_4, DIBAL-H, LiAlH_4$.
- **Recipe**: 10% AcOH/MeOH.
- **Safety Warning**: **In-situ (on-plate) quenching is strictly prohibited** for high concentrations. Violent hydrogen evolution ($H_2$) will physically damage the silica layer, creating "craters" and destroying the integrity of migration behavior.

---

## 4. Concentration & Operational Boundaries (Integration with TLC-PRE-002)

- **Equivalent Concentration < 0.5 M**: In-situ (on-plate) quenching is permitted, provided the "reagent pre-wetting" protocol is followed.
- **Equivalent Concentration > 0.5 M**: Ex-situ (in-vial) quenching is strongly recommended, where pre-mixing occurs in a sampling vial prior to spotting.
- **Equivalent Concentration ≥ 1.0 M**: **Mandatory** Ex-situ quenching to ensure complete reaction and controlled loading volume.

---

## 5. Module Integration

- **TLC-PRE-002-SAMPLE-PREPARATION-GATE**: Decides "if" quenching is mandatory.
- **TLC-002-SPOTTING-OPERATION**: Defines physical spotting mechanics (e.g., capillary use).
- **TLC-TECH-001-QUENCH-RECIPES**: Provides specific chemical recipes.

---

> **TECH Motto**: The goal of quenching is not to "finish the reaction," but to transform the system into a form that TLC can interpret.