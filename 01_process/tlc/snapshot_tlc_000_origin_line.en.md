---
snapshot_id: "TLC-000-ORIGIN-LINE"
status: "stable"
technique: "Thin Layer Chromatography"
topic: "Physical Baseline"
dependencies: ["TLC-PRE-001"]
priority: "Critical"
---

## 1. Definition and Purpose
The Origin Line is the physical baseline of a TLC experiment. It provides a uniform starting Y-coordinate for all samples, which is a logical prerequisite for calculating $R_f$ values and performing cross-lane comparisons.

## 2. Physical Specifications

### 2.1 Vertical Offset
- **Core Principle**: The height of the origin line must be high enough to **prevent the sample spots from being submerged** by the mobile phase.
- **Reference Value**: Typically set at **1.0 cm** from the bottom of the plate.
- **Invalidation Criteria**: If sample spots are submerged in the solvent, the data for those lanes will be marked as `Invalid`.

### 2.2 Horizontal Alignment
- **Standard**: The centers of all sample spots must be aligned on the same horizontal line.
- **Tolerance**: The vertical deviation between any two spots should be controlled within **2.0 mm**.
- **Impact**: Deviations exceeding this tolerance introduce artificial errors in relative $R_f$ calculations for AI models.

### 2.3 Marking Requirements
- Use a 2B pencil to mark the plate very lightly. 
- **Prohibited**: Do not score the silica layer (which disrupts capillary action) or use ink pens (which introduce chemical interference).

## 3. Spot Diameter
- **Ideal Range**: The initial diameter of the spot should be strictly controlled between **0.5 mm and 1.5 mm**.
- **Logical Significance**: Small initial diameters yield higher separation resolution and are critical for precise **Centroid Localization** in machine vision.