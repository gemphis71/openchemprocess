---
snapshot_id: "TLC-000-ORIGIN-LINE"
status: "stable"
language: zh  
canonical_id: TLC-000-ORIGIN-LINE
technique: "Thin Layer Chromatography"
topic: "Physical Baseline"
dependencies: ["TLC-PRE-001-REPRESENTATIVENESS-SAMPLING"]
priority: "Critical"
---

## 1. 定义与目的
Origin Line（起始线）是 TLC 实验的物理基准。它为所有样点提供统一的起始纵坐标，是计算 $R_f$ 值及进行跨通道对比的逻辑前提。

## 2. 物理标准 (Physical Specifications)

### 2.1 纵向高度 (Vertical Offset)
- **核心准则**：起始线高度必须以**不被展开剂淹没**为准。
- **参考值**：通常设定为距离板底 **1.0 cm**。
- **失效判定**：若样点被展开剂直接淹没，该通道数据将被标记为 `Invalid`。

### 2.2 水平对齐度 (Horizontal Alignment)
- **标准**：所有样点的中心应排列在同一水平线上。
- **容差**：各样点间的纵坐标偏差需控制在 **2.0 mm** 以内。

### 2.3 物理标记要求
- 建议使用 2B 铅笔极轻标记，严禁划破硅胶层或使用油性笔。

## 3. 样点直径 (Spot Diameter)
- **理想范围**：起始点样直径应控制在 **0.5 mm - 1.5 mm**。
- **逻辑重要性**：小直径样点能提供更高的分离分辨率，是机器进行质心（Centroid）定位的核心数据指标。
---

## Machine Annotation

```yaml
schema_version: risk_annotation_schema_v0.2
canonical_id: TLC-000-ORIGIN-LINE
annotation_scope: chapter_level
process_stage: tlc_coordinate_baseline_definition
source_language: zh
machine_review_role: coordinate_system_validity_gate

transition_model: physical_origin_line_to_rf_coordinate_baseline

core_judgment: >
  TLC 起始线是 Rf 计算、跨通道比较和机器可读空间解释所需的物理坐标基线。
  如果起始线被展开剂淹没、纵向不齐、标记造成化学或物理干扰，
  或无法支持可靠的质心定位，则后续 Rf 比较和 lane 判读失去坐标有效性。

risk_signals:
  - 样点被展开剂淹没
  - 起始线未能提供统一的起始纵坐标
  - 样点中心纵向偏差造成人为 Rf 误差
  - 起始标记破坏硅胶毛细迁移行为
  - 使用油性笔或其他化学干扰性标记
  - 起始点径过大，无法可靠进行质心定位
  - 在起始线几何无效时仍进行跨 lane 比较
  - 对物理基线无效的 lane 计算 Rf

reasoning_anchors:
  - coordinate_baseline_integrity
  - origin_line_validity
  - rf_coordinate_validity
  - cross_lane_comparison_validity
  - centroid_localization_validity
  - physical_marker_noninterference

tlc_specific_review_triggers:
  origin_line_reference_height: "通常距离板底约 1.0 cm"
  lane_invalid_if_submerged: "样点被展开剂淹没时，该 lane 数据无效"
  vertical_alignment_tolerance: "样点中心纵向偏差应控制在 2.0 mm 内"
  initial_spot_diameter_reference: "起始点径理想范围为 0.5-1.5 mm"
  marker_constraint: "使用轻微铅笔标记，避免划破硅胶或使用油性笔"

expert_judgment_patterns:
  - 在解释 Rf 之前，先将起始线视为 TLC 坐标系的物理基准。
  - 将样点被淹没或物理基线无效视为 lane-level 数据失效。
  - 将纵向不齐视为人为 Rf 误差，而不是化学迁移差异。
  - 将标记干扰或硅胶损伤视为坐标系统污染。
  - 不应将 TLC 特异性几何数值泛化为全局层析规则。

uncertainty_and_exceptions:
  - 非标准起始线高度在样点不被淹没且坐标几何保持有效时仍可接受。
  - 小的几何偏差只有在不影响目标解释分辨率时才可容忍。
  - 点径参考值属于 TLC 视觉坐标触发条件，不是通用分析要求。

machine_use: >
  本 annotation 用于在 Rf 计算、跨通道比较或机器视觉判读之前，
  检查 TLC 板是否具备有效物理坐标基线。若起始线几何、标记完整性或点位定位有效性失败，
  应先使受影响 lane 无效化或降级，而不是进入后续判读。
```