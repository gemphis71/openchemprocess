---
snapshot_id: "TLC-PRE-000-APPLICABILITY-STABILITY"
status: "stable"
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