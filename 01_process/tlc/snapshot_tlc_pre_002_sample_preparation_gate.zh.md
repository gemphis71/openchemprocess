---
snapshot_id: "TLC-PRE-002-SAMPLE-PREPARATION-GATE"
status: "stable"
language: zh  
canonical_id: TLC-PRE-002-SAMPLE-PREPARATION-GATE
technique: "Thin Layer Chromatography"
topic: "Entry Gate: Sample Preparation & Quench"
dependencies:
  - "TLC-PRE-000-APPLICABILITY-STABILITY"
  - "TLC-PRE-001-REPRESENTATIVENESS-SAMPLING"
priority: "High"
---

# TLC-PRE-002 点板样品的预处理 Gate (Sample Preparation & Quench)

## 1. Gate 定义
本 Gate 用于在样品已具备 TLC 适用性（TLC-PRE-000-APPLICABILITY-STABILITY）且取样具有代表性（TLC-PRE-001-REPRESENTATIVENESS-SAMPLING）的前提下，判断：**样品在“取样 → 点板 → 展开”的时间尺度内，是否必须经过预处理（如淬灭、稀释、体系调整），以避免继续反应或因体系因素导致 TLC 信息失真。**

本 Gate 仅裁定 **是否需要 / 是否允许 / 是否禁止**，不定义具体操作方法（操作细节见后续工艺文档）。

## 2. TLC 的隐含时间与环境尺度（判断基础）
所有判断基于以下不可回避的实验事实：
- **时间尺度**：取样 → 点板 → 进入展开缸，总计耗时约 **30–60 秒**。
- **环境变化**：
  - 温度迅速升至室温。
  - 暴露于空气与环境湿度。
  - **硅胶表面的活性**：含有微酸性的硅羟基（Si–OH），具有一定的催化或反应活性。

**若样品在上述尺度内会发生不可忽略的化学变化，则必须进行预处理。**

---

## 3. 淬灭 (Quench) 判定逻辑

### 3.1 必须淬灭 (Mandatory)
满足以下任一条件时，**不经淬灭直接点板 = Gate 不通过**：
- 反应速率极快（分钟级半衰期 $t_{1/2}$ 或更高）。
- 存在高活性中间体（强亲核/强亲电试剂、有机金属物种、活泼氧化还原物种）。
- 对痕量水分、质子或温升高度敏感。

**判定结论**：未淬灭的 TLC 结果仅反映“点板后的随机转化”，不能代表反应体系的真实状态。

### 3.2 淬灭的合法形式 (Legal Quench Forms)
当触发 3.1 时，允许以下两种淬灭形式：
- **In-situ（板上）淬灭**：仅适用于低浓度且淬灭放热不剧烈的情况。
- **Ex-situ（体外）快速淬灭**：在取样瓶中先与淬灭剂反应，再行点板。

### 3.3 可不淬灭 (Allowed without Quench)
- 反应已明确终止或猝灭。
- 样品为热力学稳定、对空气/硅胶惰性的成品或中间体。

---

## 4. 浓度与稀释 Gate (Concentration Limits)

### 4.1 正常工作窗口
- **0.1–0.5 M**：视为 TLC 的标准点样浓度窗口，允许直接进入点板流程。

### 4.2 必须稀释 (Mandatory Dilution)
满足以下任一条件时，必须先进行稀释（或体外淬灭）：
- 反应浓度 **≥ 0.5 M**。
- 浓度较高且出现混悬、过载或点样半径不可控。
- **判定结论**：不稀释直接点板 = Gate 不通过。

### 4.3 In-situ 淬灭的浓度约束
- **强制约束**：板上淬灭仅适用于 **0.1–0.5 M** 等效浓度。
- 对于高浓度体系，禁止仅依赖板上淬灭（易导致淬灭不完全产生假斑点），必须进行体外完全淬灭。

---

## 5. 溶剂与体系状态判定

若体系中存在以下因素，且会显著扭曲组分在板上的迁移行为（Rf 偏移、点形扩散、严重拖尾），必须进行预处理（如挥发、置换或中和）：

- **高沸点/强极性溶剂**：如 DMSO、DMF、NMP。
- **干扰组分**：游离水、强酸、强碱。
- **兼容性原则**：预处理引入的溶剂必须与展开剂兼容；中和过程必须保持体系均相。若预处理本身引入不可控的沉淀或新反应，则 TLC 不再适用。

---

## 6. Gate 输出 (Outputs)

### ✅ 通过 Gate
- 样品在 TLC 尺度内化学惰性，且体系因素不会导致迁移失真。进入 `TLC-002-SPOTTING-OPERATION` 物理操作。

### ⚠️ 条件通过 (Conditional)
- 必须经过明确的预处理（淬灭/稀释/溶剂置换）后方可点板。
-- **关联指引**：具体的化学淬灭配方（如 MeOH, AcOH 等）请参考 **`TLC-TECH-001-QUENCH-RECIPES`**。
- 处理细节需在实验记录中注明。

### ❌ 未通过 Gate
- 样品持续转化或体系因素导致不可控的失真。禁止使用 TLC。

> **Gate 箴言**：TLC 的前提不是“点得好”，而是“点上去的那一刻，化学与迁移行为都已经被控制住”。
---

## Machine Annotation

```yaml
schema_version: risk_annotation_schema_v0.2
canonical_id: TLC-PRE-002-SAMPLE-PREPARATION-GATE
annotation_scope: chapter_level
process_stage: tlc_pre_sample_preparation
source_language: zh
machine_review_role: evidence_admissibility_gate

transition_model: admissible_sample_to_controlled_spotting_input

core_judgment: >
  TLC 样品预处理是证据准入 gate。只有在适用性与取样代表性已经成立后，
  样品还必须在取样、点板、展开的时间窗口内保持化学状态和迁移行为受控。
  如果持续反应、高浓度、不完全淬灭、溶剂基质或体系组分导致化学状态或迁移行为失真，
  该 TLC 结果不能被视为真实诊断投影。

risk_signals:
  - 样品在 TLC 制备时间窗口内发生不可忽略的化学变化
  - 未淬灭的快速反应样品被直接点板
  - 高活性中间体在取样或点板过程中仍保持活性
  - 样品对痕量水分、质子或室温跃迁高度敏感
  - 未淬灭 TLC 结果反映点板后的随机转化
  - 反应浓度超过 TLC 工作浓度窗口
  - 高浓度导致混悬、过载或点径不可控
  - 板上淬灭超出其浓度适用边界
  - 高沸点或强极性溶剂扭曲迁移行为
  - 游离水、强酸或强碱导致 Rf 或点形失真
  - 预处理本身引入沉淀或新反应

reasoning_anchors:
  - observation_validity_gate
  - sample_state_projection
  - sample_preparation_gate
  - quench_requirement_check
  - dilution_requirement_check
  - matrix_compatibility_check
  - migration_distortion_control

tlc_specific_review_triggers:
  preparation_time_window: "取样到点板再到展开通常为 30-60 秒"
  mandatory_quench_context: "快速反应、高活性中间体，或对水分、质子、温度跃迁高度敏感"
  working_concentration_window: "0.1-0.5 M 作为 TLC 工作浓度窗口"
  high_concentration_trigger: "反应浓度 >= 0.5 M，或出现点径失控、混悬、过载"
  in_situ_quench_constraint: "板上淬灭仅适用于低等效浓度且淬灭放热和不完全淬灭不占主导的场景"
  matrix_distortion_context: "DMSO、DMF、NMP、游离水、强酸或强碱可能导致 Rf、扩散或拖尾失真"

expert_judgment_patterns:
  - 将样品预处理视为 TLC 证据准入前提，而不是后续判读步骤。
  - 将淬灭、稀释和体系调整视为对化学状态保真和迁移状态有效性的控制。
  - 不应把未淬灭快速反应样品的 TLC 当作原始反应状态。
  - 不应把高浓度或基质失真的点样结果作为半定量 TLC 证据。
  - 应区分是否需要/允许/禁止预处理的 review 与具体淬灭或点样配方。

uncertainty_and_exceptions:
  - 当样品在 TLC 时间窗口内化学惰性且基质不扭曲迁移时，可直接点板。
  - 条件性预处理只有在生成均相且化学状态明确的样品输入时，才恢复 TLC 证据资格。
  - TLC 特异性浓度与时间窗口不得泛化为全局分析规则。

machine_use: >
  本 annotation 用于在 TLC-PRE-000 和 TLC-PRE-001 通过后，判断样品在点板前是否必须
  淬灭、稀释或调整基质。若化学状态保真或迁移有效性未被控制，应降级或拒绝后续 TLC 判读，
  而不是把板面结果当作可靠证据。
```