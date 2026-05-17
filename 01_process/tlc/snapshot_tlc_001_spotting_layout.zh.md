---
snapshot_id: "TLC-001-SPOTTING-LAYOUT"
status: "stable"
language: zh  
canonical_id: TLC-001-SPOTTING-LAYOUT
technique: "Thin Layer Chromatography"
topic: "Spotting Layout"
dependencies: ["TLC-000-ORIGIN-LINE"]
---

## 1. 讨论核心
本 Snapshot 定义 TLC 板的横向布局及其逻辑语义。这种布局构建了一个“相对坐标系”，用于推理反应体系与物料之间的演变关系。

## 2. 标准 4 点布局 (Standard 4-Lane Layout)

基于最佳实践，点样应遵循以下标准序列（从左至右）：

| 通道 (Lane)  | 标签          | 成分                    | 逻辑功能                                                                   |
| :--------- | :---------- | :-------------------- | :--------------------------------------------------------------------- |
| **Lane 1** | **Ref**     | 起始原料 (SM)             | 提供 Rf 与显色的绝对参照。                                                        |
| **Lane 2** | **Spike**   | SM + Reaction Mixture | **协同定位与校准**：通过消除基质效应（如酸碱干扰）引起的 $R_f$ 微小位移，判定 Sample 中的点是否与 SM 具有物理恒等性。 |
| **Lane 3** | **Sample**  | 反应体系样品                | **核心观测对象**：监测原料向产物的转化速度与程度，观测副产物的生成速度及其粗略比例。                           |
| **Lane 4** | **Product** | 产物/杂质标样 (可选)          | 锁定目标产物位置，完善坐标系。                                                        |

## 3. 空间约束 (Spatial Constraints)
- **点间距 (Pitch)**：建议 **3 mm - 6 mm**。高密度的点样有助于在有限的板宽内承载更多逻辑对照，同时要求点样直径严格控制以防重叠。
- **边距 (Margin)**：边缘样点距离板边缘 $\ge 5$ mm，以减少边缘效应（Smiling Effect）引起的畸变。

## 4. 机器判读逻辑
- **基质效应校准 (Matrix Shift Compensation)**：由于反应液中的酸、碱或副产物可能微弱改变原料的迁移率，导致 Lane 3 的点相对于 Lane 1 产生微小位移。
- **Spike 判定准则**：
  - 如果 Lane 3 的点有微移，但 Lane 2 (Spike) 对应位置仍呈现为一个圆润、不分裂的单点，机器判定该位移由体系环境引起，物理性质仍等同于原料。
  - 如果 Lane 2 出现“双斑”或“拉长豆”状，则判定为性质不同的新物质。
- **转化率推理**：机器通过计算 Lane 3 中 SM 点位与 Product 点位的显色强度/面积比，给出粗略的转化比例预测。
---

## Machine Annotation

```yaml
schema_version: risk_annotation_schema_v0.2
canonical_id: TLC-001-SPOTTING-LAYOUT
annotation_scope: chapter_level
process_stage: tlc_lane_layout_and_reference_anchoring
source_language: zh
machine_review_role: reference_layout_validity_gate

transition_model: lane_layout_to_relative_coordinate_and_reference_system

core_judgment: >
  TLC 点样布局定义了用于比较原料、反应液、混合点和可选产物/杂质标样的相对坐标与参照系统。
  Ref、Spike、Sample 和 Product lane 建立身份一致性与基质位移校准所需的锚定逻辑；
  若参照布局无效，存在性判断和身份解释都会变得不稳定。

risk_signals:
  - TLC 板缺少原料参照 lane
  - 可能存在基质位移时，反应样品未通过 co-spot 锚定即被解释
  - 未进行 spike 比较就将 sample lane 的 Rf 位移解释为化学变化
  - spike lane 出现双斑或拉长双点形貌
  - 需要目标位置锚定时缺少产物或杂质标样
  - lane 间距过窄导致重叠
  - 外侧 lane 距离板边过近并受边缘效应影响
  - 身份一致性判断中忽略基质效应
  - 使用显色强度或面积比进行精确转化率推断

reasoning_anchors:
  - reference_layout_validity
  - relative_coordinate_system
  - co_spot_anchoring
  - matrix_shift_compensation
  - identity_consistency_check
  - lane_geometry_validity
  - edge_effect_control
  - prohibited_quantitative_conversion

tlc_specific_review_triggers:
  standard_lane_set: "Ref / Spike / Sample / Product-or-impurity-standard"
  lane_spacing_reference: "推荐点间距 3-6 mm"
  edge_margin_reference: "最外侧样点距离板边应至少 5 mm"
  spike_single_spot_logic: "Spike 中形成单一圆润点，支持基质位移解释"
  spike_split_logic: "出现两个清晰点或拉长双点形貌，提示不同实体"
  conversion_inference_boundary: "强度/面积比只能支持粗略趋势或相对估计，不支持精确转化率"

expert_judgment_patterns:
  - 在解释点位身份之前，先将 TLC 布局视为参照与锚定系统。
  - 使用 spike 行为区分基质位移与化学身份变化。
  - 将缺少参照或 co-spot 视为身份一致性解释权降低。
  - 将 lane 重叠和边缘效应视为布局层面的判读威胁。
  - 不应将 Lane 3 的显色强度或面积比转化为精确转化率百分比。

uncertainty_and_exceptions:
  - 当本板不需要锚定目标产物身份时，产物或杂质标样 lane 可为可选。
  - 当 pH、盐、副产物或反应液基质可能造成迁移位移时，co-spot 锚定尤其关键。
  - 布局层面的身份一致性不是确定性结构确认，必须受限于 TLC 判读边界。

machine_use: >
  本 annotation 用于在解释存在/消失、身份一致性、基质位移或反应趋势之前，
  检查 TLC 板是否具备有效的 lane 参照布局。若参照 lane、spike 逻辑、lane 间距或边缘有效性不足，
  应降级身份判断和转化相关结论。
```