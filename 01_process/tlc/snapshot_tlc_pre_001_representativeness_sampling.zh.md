---
snapshot_id: "TLC-PRE-001-REPRESENTATIVENESS-SAMPLING"
status: "stable"
language: zh  
canonical_id: TLC-PRE-001-REPRESENTATIVENESS-SAMPLING
technique: "Thin Layer Chromatography"
topic: "Entry Gate: Representativeness & Sampling"
dependencies: ["TLC-PRE-000-APPLICABILITY-STABILITY"]
priority: "High"
---

# TLC-PRE-001 代表性 / 取样策略 Gate (Representativeness & Sampling)

## 1. Gate 定义
本 Gate 用于在取样阶段判断：**当前用于点板的微量样品，是否在物理相态与组成比例上，真实代表了反应体系全貌。**

## 2. 核心假设：等价性 (Equivalency)
TLC 有效性的前提是：**点到板上的样品比例 = 反应体系总比例。**
非均相体系（Heterogeneous System）是破坏该假设的最主要来源。

---

## 3. 非均相体系的强制判定逻辑

### 3.1 分相原则 (Phase Separation Rule)
- **多相共存**：固-液或液-液体系，原则上**必须分开点板**（分别取样）。
- **风险提示**：在高速搅拌下进行“混合吸取”通常是不具代表性的，其结果仅能作为粗略定性参考，极易产生比例误判。

### 3.2 豁免条件：无关相逻辑
若满足以下前提，可进行混合取样或仅取单相：
- 确认固体或另一液相为**惰性组分**（如无机盐沉淀、不混溶的溶剂）。
- 目标产物与中间体在无关相中无分布、无吸附、无反应。
- **判定**：此时取样偏差不构成信息误判。

### 3.3 高风险预警（严禁直接作为转化率判断）
以下情形会导致 TLC 结果产生方向性误判：
- **溶解平衡限制**：原辅料边溶解边反应，液相浓度不代表反应进度。
- **产物析出**：产物在反应过程中达到饱和并析出。
- **表面吸附**：组分强力吸附在催化剂（如 Pd/C）或无机载体表面，导致液相信号偏低。
- **逻辑结论**：此时的 TLC 仅代表**“液相浓度变化”**，不代表**“总转化率”**。

---

## 4. 取样偏差管理原则

### 4.1 统计学取样建议 (Scale-up Sampling)
在无法分相但必须获取定性信息时，应通过放大取样体积来降低随机误差，并在后续 `TLC-PRE-002-SAMPLE-PREPARATION-GATE` 中进行处理：
- **实验室规模 (≤1 L)**：建议取 **1–5 mL** 混合样。
- **工业规模 (≥1000 L)**：建议取 **~1 L** 混合样。



## 5. Gate 输出 (Outputs)

### ✅ 通过 Gate
- 样品具有物理与比例代表性。进入 `TLC-PRE-002-SAMPLE-PREPARATION-GATE`。

### ⚠️ 条件通过 (Conditional)
- 取样仅具定性价值。必须在实验记录中明确标注：“由于非均相限制，本 TLC 结果不用于转化率定量判断”。

### ❌ 未通过 Gate
- 取样过程存在严重偏差或无法分相监测。TLC 结果将导致系统性误判，建议更换分析手段。

> **核心箴言**：TLC 的风险不在“点板”，而在“这一滴是否代表了反应”。

## Machine Annotation

```yaml
schema_version: risk_annotation_schema_v0.2
canonical_id: TLC-PRE-001-REPRESENTATIVENESS-SAMPLING
annotation_scope: chapter_level
process_stage: tlc_pre_sampling_representativeness
source_language: zh
machine_review_role: evidence_admissibility_gate

transition_model: reaction_system_to_spotted_micro_sample_projection

core_judgment: >
  点到板上的微量样品必须代表反应体系的物理相态和组成比例。
  在非均相体系中，TLC 可能只反映液相浓度或被取样偏差放大的局部组分，
  而不代表总转化率或整体体系组成。

risk_signals:
  - 非均相反应体系被作为单一混合样点板
  - 固液或液液相未被分别取样
  - 高速搅拌下混合吸取被当作代表性样品
  - 原料边溶解边反应
  - 产物在反应过程中析出
  - 产物或中间体分配至另一相
  - 目标组分吸附在催化剂或无机载体上
  - 液相 TLC 信号被当作总转化证据
  - 取样偏差可能造成组成比例方向性误判

reasoning_anchors:
  - representativeness_check
  - liquid_phase_only_projection
  - sample_state_projection

tlc_specific_review_triggers:
  heterogeneous_system: "固液或液液非均相体系"
  mixed_sampling_risk: "高速搅拌混合吸取被用作组成代理"
  solubility_equilibrium_constraint: "原料边溶解边反应"
  product_precipitation: "产物达到饱和并在反应中析出"
  surface_adsorption: "组分吸附于催化剂或无机载体"
  qualitative_only_record: "非均相限制下 TLC 结果不应用于定量转化率判断"

expert_judgment_patterns:
  - 在解释反应进度之前，先把 TLC 取样视为证据代表性问题。
  - 对非均相体系，除非已建立物理和比例代表性，否则 TLC 只应视为相特异性证据。
  - 存在溶解、析出、吸附或分配时，不应把液相浓度变化当作总转化。
  - 应区分定性监测价值与定量转化判断。

uncertainty_and_exceptions:
  - 若未取样相被证明为化学无关相，混合取样或单相取样可具有可接受解释性。
  - 取样偏差不必然否定所有定性监测价值，但可能否定总转化或组成比例推断。
  - 放大取样体积建议为 TLC 特异性取样提示，不应泛化为通用取样规则。

machine_use: >
  本 annotation 用于在使用 TLC 判断转化、原料消失、产物生成或杂质比例之前，
  先检查点板样品是否代表反应体系整体。若样品不能代表体系的物理和组成状态，
  TLC 解释应限制为相特异性或定性证据。