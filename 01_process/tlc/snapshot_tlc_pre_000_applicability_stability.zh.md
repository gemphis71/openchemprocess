---
snapshot_id: "TLC-PRE-000-APPLICABILITY-STABILITY"
status: "stable"
language: zh  
canonical_id: TLC-PRE-000-APPLICABILITY-STABILITY
technique: "Thin Layer Chromatography"
topic: "Entry Gate: Stability and Applicability"
dependencies: []
priority: "Critical"
---

# TLC-PRE-000 适用性 / 稳定性 Gate (Applicability & Stability)

## 1. Gate 定义
本 Gate 用于在执行任何 TLC 操作之前，评估样品在 TLC 特定物理化学环境下的生存状态。其核心目标是判断：**样品在板上呈现的信号，是否依然是其原始化学状态的真实投影。**

## 2. TLC 的环境约束 (Implicit Assumptions)
使用 TLC 即意味着样品必须暴露于以下三个维度，且无法规避：

### 2.1 时间尺度 (Time Scale)
- **暴露时间**：从取样、点板到放入展开缸，标准操作时间为 **30–60 秒**。
- **逻辑含义**：若化学转化半衰期小于此量级，TLC 将无法捕捉真实的初始状态。

### 2.2 物理化学环境 (Physicochemical Environment)
- **固相活性**：硅胶表面含有微酸性硅羟基 (Si–OH)。
- **共存物**：空气中的微量水分、氧气。
- **风险**：易导致酸催化分解、吸附重排或氧化。

### 2.3 温度跃迁 (Thermal Jump)
- **现象**：低温（如 -78°C）反应液点样后，样品会迅速回升至**室温**。
- **风险**：热力学不稳定的中间体可能在此过程中发生不可逆转化。

---

## 3. 判断清单 (Decision Checklist)

### Q1｜样品在 TLC 时间尺度内是否化学稳定？
- ✅ **Yes**：组成在 60 秒内基本保持恒定。
- ❌ **No**：在此尺度内发生显著分解或反应。

### Q2｜样品对硅胶/水/微酸环境是否敏感？
- ✅ **Yes**：对上述因素不敏感。
- ⚠️ **Conditional**：存在活性官能团（如酰氯、酸酐），需预处理规避。
- ❌ **No**：极易变质且无法通过常规手段规避。

### Q3｜体系是否处于“快速演化”状态？
- ✅ **Yes**：慢反应体系（$t_{1/2} \ge 1 \text{ h}$），可视为准静态。
- ⚠️ **Conditional**：快反应或含活性中间体，需淬灭/钝化处理。
- ❌ **No**：板上继续反应，结果不可信。

---

## 4. Gate 输出 (Outputs)

### ✅ 通过 Gate：直接使用 TLC
- 满足所有 Q 均为 Yes。进入 `TLC-000` 流程。

### ⚠️ 条件通过：需预处理
- 存在活性组分，必须经过“淬灭 (Quench)”或“衍生化 (Derivatization)”后再进行点板。

### ❌ 未通过 Gate：禁止使用 TLC
- 样品与 TLC 环境存在不可调和的冲突。应切换至 HPLC、GC 或 NMR 等分析手段。

> **核心箴言**：决定是否做 TLC，不是看“能不能点上去”，而是看“板上发生的是否还是原来的化学”。

## Machine Annotation

```yaml
schema_version: risk_annotation_schema_v0.2
canonical_id: TLC-PRE-000-APPLICABILITY-STABILITY
annotation_scope: chapter_level
process_stage: tlc_pre_observation_validity
source_language: zh
machine_review_role: evidence_admissibility_gate

transition_model: sample_state_to_tlc_environment_projection

core_judgment: >
  只有当样品在 TLC 暴露时间窗口和 TLC 物理化学环境中保持化学稳定时，
  TLC 才能作为有效的诊断投影。如果样品在取样、点板、板面接触、水氧暴露、
  或由低温快速升至室温的过程中发生转化，则板上信号不再可靠代表原始化学状态。

risk_signals:
  - 样品可能在 TLC 暴露时间窗口内发生转化
  - 样品半衰期短于取样至展开的操作时间尺度
  - 样品对硅胶表面微酸性敏感
  - 样品对 TLC 操作过程中的微量水分或氧气敏感
  - 低温样品点板后快速升温
  - 热不稳定中间体可能在 TLC 制备过程中发生转化
  - 反应在 TLC 板上继续发生
  - 板上信号可能不代表原始化学状态

reasoning_anchors:
  - observation_validity_gate
  - sample_state_projection

tlc_specific_review_triggers:
  exposure_window: "从取样、点板到进入展开缸约 30-60 秒"
  surface_environment: "硅胶表面、微酸性硅羟基、微量水分、氧气"
  thermal_jump: "低温反应样品点板后快速回升至室温"
  fast_evolving_system: "化学转化半衰期显著短于 TLC 操作窗口"

expert_judgment_patterns:
  - 只有先确认样品能在 TLC 环境中生存，TLC 才可作为诊断证据。
  - 若样品在取样、点板、板面接触或升温过程中发生转化，应先判定为证据有效性问题，而不是反应组成问题。
  - 应区分“能否使用 TLC”与“TLC 结果说明什么化学含义”。
  - 如果样品状态可能已在板上改变，不应把可见斑点模式直接作为反应证据。

uncertainty_and_exceptions:
  - 条件性样品处理只有在保留明确化学投影状态时，才可能恢复 TLC 证据资格。
  - 慢反应体系只是在给定 TLC 操作窗口内可视为准静态。
  - TLC 特异性时间与环境触发条件不得扩展为全局分析规则。

machine_use: >
  本 annotation 用于在使用 TLC 判断反应进度、转化率、杂质模式或中间体状态之前，
  先判断该 TLC 结果是否具备证据资格。若样品在 TLC 时间窗口或 TLC 环境中的稳定性未被建立，
  应降级或拒绝后续基于 TLC 的化学解释。