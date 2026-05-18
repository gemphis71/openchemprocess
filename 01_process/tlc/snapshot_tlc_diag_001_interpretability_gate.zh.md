---
snapshot_id: "TLC-DIAG-001-INTERPRETABILITY-GATE"
status: "stable"
language: zh  
canonical_id: TLC-DIAG-001-INTERPRETABILITY-GATE
technique: "Thin Layer Chromatography"
topic: "Interpretability gate for TLC plate diagnostics"
dependencies:
  - "TLC-004-PLATE-VISUAL-OBSERVATION"
---

# TLC-DIAG-001 TLC 判读解释权 Gate（Interpretability Gate）

## 0. Gate 定义与适用范围

本 Gate 用于判定一块 **已完成展开与视觉化的 TLC 板** 是否具备进入后续解释流程（DIAG-002）的资格。  
本文件仅裁定解释权的状态（PASS / DOWNGRADED / REVOKED / VOID），不负责解释具体的化学反应结果。

> **重要说明（数据对象边界）**  
> 本 Gate 的判定对象是“当前板面生成的视觉数据对象”。  
> 若需更换显色剂、重新显色或重复展开，应视为**新的数据输入**，需重新经过本 Gate 评估。

---

## Gate-0 显色有效性（Visualization Validity）

**判定规则**
- 若出现以下情况，判定为 **REVOKED**：
  - 点信号与局部背景的对比度极低，导致肉眼或机器无法提取清晰轮廓。
  - 背景噪音（如显色剂过浓、烘烤过度导致的焦黑）覆盖超过板面有效面积的 30%。

**逻辑说明**
- 此为最底层的物理网关。若视觉对象本身不可识别，后续所有形态学与逻辑判断均失去物质基础。

---

## Gate-1 起点投影完整性（Starting Material Projection）

**判定规则**
- 若原料对照点（SM）未形成可定义、可重复的迁移行为（即绝大部分信号滞留在点样原点，$R_f \approx 0$）。
- **处理结果**：**解释权直接 REVOKED**。

**逻辑说明**
- 原料未迁移意味着起点投影未生成，反应监测的最小物理参照缺失。  
- 此条为**前置断路网关**，一旦触发，不再检查后续 Gate。

---

## Gate-2 投影轴量程有效性（Projection Axis Capacity）

**判定规则**
- 若关键点位整体落入信息压缩区：
  - 低端：$R_f < 0.2$。
  - 高端：$R_f > 0.8$。
- 且在 0.2–0.7 的有效投影区间内无法建立可区分结构。
- **处理结果**：**解释权 REVOKED**。

**逻辑说明**
- 投影轴量程与体系极性失配，信息熵在物理层已被压缩，导致点数与相对比例推断不成立。

---

## Gate-3 点形物理完整性（Spot Morphology Integrity）

**判定规则**
- 若出现系统性物理失效形貌：条带化（Banding）、纵向涂抹（Streaking）或由于高沸点溶剂残留导致的整体推移。
- **处理结果**：**解释权 REVOKED**。

**逻辑说明**
- 层析平衡未建立，物理失效优先级高于任何化学解释或经验判断。

---

## Gate-4 协议锚点完整性（Anchoring & Co-spot）

**判定规则**
- 在反应监测场景中，若缺失 Co-spot（Spike）参照，且样品信号无法被明确锚定或校准。
- **处理结果**：**判读状态 VOID（逻辑作废）**。

**逻辑说明**
- 属于协议层失败。无法区分“未点上”、“原料消失”与“基质效应位移”等互斥状态。

---

## Gate-5 表面相互作用与低 Rf 拖尾（Surface Interaction & Tailing）

**判定规则**
- 若关键点位在低 $R_f$ 区（$< 0.2$）呈现稳定、方向一致的三角形或火焰状拖尾，且**拖尾沿迁移方向的延展长度**超过 **0.2 个 $R_f$ 单位**。
- **处理结果**：**解释权 DOWNGRADED**。

**逻辑说明**
- 信号可信度受限，禁止进行定量推断或基于点形的纯度判断，仅保留受限的定性观察权。

---

## Gate-6 Co-spot 锚定偏差的数值判定

**判定区间（基于原料对照点与 Co-spot 中原料点的 $|\Delta R_f|$）**
- **高度一致**：$|\Delta R_f| < 0.05$ → **PASS**。
- **可接受一致**：$0.05 \le |\Delta R_f| < 0.1$ → **CAUTION**。
- **明显降权**：$0.1 \le |\Delta R_f| < 0.2$ → **DOWNGRADED**。
- **不可接受**：$|\Delta R_f| \ge 0.2$ → **REVOKED**。

> **状态语义说明**  
> **CAUTION** 为 **DOWNGRADED** 的子态，用于提示锚定不稳定但尚可使用；不构成独立的最终状态类型。

---

## 优先级规则与输出汇总

| 触发 Gate | 优先级 | 最终状态 | 核心语义 |
| :--- | :--- | :--- | :--- |
| **Gate-0/1/2/3** | 极高 | **REVOKED** | 物理/层析失效，禁止解释 |
| **Gate-4** | 高 | **VOID** | 逻辑引用断裂，数据无效 |
| **Gate-5/6** | 中 | **DOWNGRADED** | 信号畸变，解释权受限 |
| **无触发** | - | **PASS** | 进入 DIAG-002 正常判读 |

---

## 边界声明

本 Gate 仅裁定解释权是否成立，不提供任何反应机理、转化率或结构判断。  
所有解释路径选择与化学推断，均属于 **DIAG-002** 的权限范围。

## Machine Annotation

```yaml
schema_version: risk_annotation_schema_v0.2
canonical_id: TLC-DIAG-001-INTERPRETABILITY-GATE
annotation_scope: chapter_level
process_stage: tlc_diagnostic_interpretability
source_language: zh
machine_review_role: interpretability_authority_gate

transition_model: developed_plate_visual_object_to_interpretation_authority

core_judgment: >
  在允许进行化学解释之前，必须先建立 TLC 板的解释权。
  一块已展开并显色的 TLC 板首先是当前板面生成的视觉数据对象，
  其物理有效性、层析有效性和锚定有效性必须先被裁定为 PASS、DOWNGRADED、REVOKED 或 VOID，
  然后才可进入反应判读。

risk_signals:
  - 点信号与背景对比度过低，无法提取清晰轮廓
  - 背景噪音遮蔽板面有效区域
  - 原料对照点未形成可重复迁移
  - 原料主要停留在原点附近，无法形成有效投影
  - 关键点位落入低 Rf 或高 Rf 信息压缩区
  - 有效投影区间内无法建立可区分结构
  - 条带化、纵向涂抹或整体推移提示层析失效
  - 反应监测中缺失 co-spot 参照
  - 样品信号无法被锚定或校准
  - 低 Rf 拖尾限制基于点形的解释
  - co-spot 锚定偏差限制解释权

reasoning_anchors:
  - interpretability_gate
  - data_object_boundary
  - interpretability_revoked
  - interpretability_downgraded
  - logical_void_status

tlc_specific_review_triggers:
  visualization_revoked: "点/背景对比度极低或板面背景噪音过高"
  background_noise_area: "背景噪音覆盖超过 30% 有效板面"
  origin_projection_failure: "原料对照点停留在 Rf 约等于 0 的原点附近"
  projection_axis_compression: "关键点位低于 Rf 0.2 或高于 Rf 0.8，且 Rf 0.2-0.7 区间内无可区分结构"
  morphology_failure: "条带化、纵向涂抹或整体推移提示物理/层析失效"
  co_spot_missing: "反应监测中缺失 co-spot 参照且样品信号无法锚定"
  low_rf_tailing: "Rf 0.2 以下出现方向一致的三角形或火焰状拖尾"
  tail_extension_threshold: "拖尾沿迁移方向延展超过 0.2 个 Rf 单位"
  co_spot_delta_rf_intervals:
    pass: "|Delta Rf| < 0.05"
    caution: "0.05 <= |Delta Rf| < 0.1"
    downgraded: "0.1 <= |Delta Rf| < 0.2"
    revoked: "|Delta Rf| >= 0.2"

interpretability_status_semantics:
  PASS: "视觉和协议证据支持正常进入解释路径"
  DOWNGRADED: "信号存在畸变，仅保留受限定性解释权"
  REVOKED: "物理或层析失效导致解释权被撤销"
  VOID: "逻辑参照或锚定失败导致当前数据对象对反应解释作废"

expert_judgment_patterns:
  - 先把已展开 TLC 板视为视觉数据对象，再视为化学证据。
  - 在判断转化率、杂质、机理或反应状态之前，先裁定解释权是否成立。
  - 更换显色剂、重新显色或重新展开应视为新的数据输入，需要重新评估。
  - 不应把物理/层析失效形貌当作化学反应证据。
  - 应区分受限定性观察权与完整化学解释权。

uncertainty_and_exceptions:
  - CAUTION 是 DOWNGRADED 的子状态，不应作为独立最终状态。
  - TLC 特异性 Rf 与背景噪音阈值是解释权触发条件，不是全局分析规则。
  - 本 Gate 不选择解释路径，也不推断反应机理；这些属于后续诊断逻辑。

machine_use: >
  本 annotation 用于判断一块已展开 TLC 板是否具备足够的视觉、层析和锚定有效性，
  可以进入化学解释。如果解释权被撤销、降级或逻辑作废，应限制或拒绝后续反应结论，
  而不是直接把斑点模式解释为反应证据。
