---
snapshot_id: "TLC-DIAG-EX-001-FRONTING-BAND-AND-BASELINE-COMPRESSION"
status: "stable"
technique: "Thin Layer Chromatography"
topic: "Non-interpretable plate due to axis compression (fronting + baseline crowding)"
dependencies:
  - "TLC-003-ELUENT-SELECTION"
  - "TLC-004-PLATE-VISUAL-OBSERVATION"
---

# TLC-DIAG-EX-001 Horizontal Banding + Low Rf Tailing: Interpretability Revoked Due to Axis Compression

## 1. Visual Observations

Through visual inspection, this plate exhibits the following typical failure characteristics:

- **High Rf Zone**: Signals in the upper-middle section ($R_f \approx 0.6$) appear as distinct horizontal "Bands" rather than circular spots. The edges diffuse laterally with blurred contours, a morphology characteristic of banding caused by the solvent front.
- **Low Rf Zone**: Critical sample signals (e.g., Lane 3) are concentrated in the low $R_f$ zone ($< 0.2$) and are accompanied by significant concave or comet-like tailing, indicating a failure of the spot to converge.
- **Distribution State**: The plate shows a typical "crowded ends, empty middle" distribution. Information is sparse within the effective projection interval (0.2–0.7).

## 2. Diagnostic Status and Logical Rationale

- **Interpretability Status**: **REVOKED / Non-interpretable**
- **Failure Type**: **Axis Compression**

In this case, the failure is a result of overlapping logical violations:

- **Scale Mismatch**: The polarity span between the starting material and product in the reaction system is too large. A single eluent ratio cannot simultaneously cover the effective projection intervals of both.
- **Loss of Information Entropy**: The horizontal banding at the high end flattens polarity differences, creating a high risk of component overlap. Signals at the low end have not entered the "high-resolution projection zone," making any inference about spot count or purity unreliable.

## 3. Mandatory Blocking Rules

To ensure logical consistency in the diagnostic layer, the following blocking rules are established:

- **Rule-001**: If a spot is flattened into a "Horizontal Band/Fronting Band," that region is judged to be an information compression zone. Quantitative inferences regarding "single component" status or "conversion rate" based on this signal are prohibited.
- **Rule-002**: When critical spots are in the $R_f < 0.2$ zone and exhibit abnormal morphology (tailing or irregularity), spot identification or purity determination for that lane is prohibited.
- **Rule-003**: Physical failure judgment. The formation of a horizontal band indicates that migration is dominated by solvent front effects, causing non-linear distortion of the projection axis. Overall interpretability is automatically weakened.

## 4. Corrective Actions

The following actions are intended only to **restore observability** and do not constitute an extension of interpretation or supplementary diagnosis of the current plate:

1. **High-end Optimization**: Use a lower-polarity system (e.g., significantly decrease the EtOAc ratio) to pull the compressed fronting band back into the 0.2–0.7 interval to observe if trace impurities exist near the starting material.
2. **Low-end Optimization**: Use a higher-polarity system (e.g., significantly increase the EtOAc ratio) to push the spots clustered near the baseline into the 0.2–0.7 interval to restore observability of spot counts and conversion behavior.

## 5. Physical Evidence

- **Correlation with Front**: The flatness of the high $R_f$ band is highly consistent with the direction of the solvent front.
- **Projection Distortion**: Due to the compromise in eluent polarity, high-$R_f$ components "collide" due to excessive elution strength, while low-$R_f$ components "stagnate" due to insufficient elution strength. This results in a significant reduction in the Information Capacity of the entire projection axis.