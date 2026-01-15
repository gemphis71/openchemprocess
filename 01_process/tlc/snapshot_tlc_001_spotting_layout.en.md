---
snapshot_id: "TLC-001-SPOTTING-LAYOUT"
status: "stable"
technique: "Thin Layer Chromatography"
topic: "Spotting Layout"
dependencies: ["TLC-000-ORIGIN-LINE"]
---

## 1. Core Discussion
This Snapshot defines the horizontal layout and logical semantics of a TLC plate. This layout establishes a "Relative Coordinate System" to infer the relationship between the reaction mixture and the starting materials.

## 2. Standard 4-Lane Layout

Based on best practices, spotting should follow this standard sequence (from left to right):

| Lane       | Label       | Composition                     | Logical Function                                                                                                                                                             |
| :--------- | :---------- | :------------------------------ | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Lane 1** | **Ref**     | Starting Material (SM)          | Provides absolute reference for $R_f$ and visualization.                                                                                                                     |
| **Lane 2** | **Spike**   | SM + Reaction Mixture           | **Co-localization & Calibration**: Eliminates $R_f$ shifts caused by matrix effects (e.g., pH, salts) to confirm the identity of spots in Lane 3 via synchronized migration. |
| **Lane 3** | **Sample**  | Reaction Mixture                | **Core Observation**: Monitors conversion rate, byproduct formation speed, and crude ratios.                                                                                 |
| **Lane 4** | **Product** | Product/Impurity Std (Optional) | Anchors the target product position to complete the coordinate system.                                                                                                       |

## 3. Spatial Constraints
- **Pitch (Lane Spacing)**: Recommended **3 mm - 6 mm**. High-density spotting allows more logical controls per plate but requires strict control of spot diameter to prevent overlapping.
- **Margin**: The distance from the outermost spots to the edge of the plate should be $\ge 5$ mm to minimize distortion caused by the **Edge Effect (Smiling Effect)**.

## 4. Machine Reasoning Logic
- **Matrix Shift Compensation**: Due to pH, salts, or byproducts in the reaction mixture, the migration of the SM in Lane 3 might shift slightly compared to Lane 1.
- **Spike Decision Rule**:
  - If a spot in Lane 3 shows a slight $R_f$ deviation, but the corresponding spot in Lane 2 (Spike) remains a single, cohesive, and unsplit spot, the AI shall conclude the displacement is caused by the matrix environment rather than a chemical change.
  - If Lane 2 displays two distinct spots or an elongated "double-spot" shape, they are identified as different chemical entities.
- **Conversion Inference**: The AI estimates conversion by calculating the intensity/area ratio between the SM spot and the Product spot in Lane 3.