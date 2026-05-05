---
snapshot_id: "ISOL-002-RECRYSTALLIZATION"
status: "draft"
domain: "Process"
process: "Isolation"
topic: "重结晶：选择性分配与固态重构（Selective Re-partitioning under Constrained Solubility Space）"
level: "002"
language: zh  
canonical_id: ISOL-002-RECRYSTALLIZATION
dependencies:
  - "ISOL-001-CRYSTALLIZATION"
  - "WRKUP-003-SOLVENT-REMOVAL-DRIVEN-ACCUMULATION-AND-THERMAL-EXPOSURE-CONTROL"
  - "WRKUP-002-PARTITION-RATIO-DRIFT-INVENTORY-CONTROL"
  - "THR-001-THERMAL-CONTROL-AUTHORITY"
note:
  - "面向 machine-review：以选择性（Selectivity）、回收率（Recovery）与溶解度路径（ΔSolubility）定义重结晶的控制边界与失效信号。"
  - "本章节对应 control regain 的短暂窗口：solid → solution → solid，但控制权受限且不可完全恢复。"
---

# ISOL-002：重结晶（Recrystallization）


## 1. System Role（系统角色）

> control regain

重结晶不是一次结晶的重复，而是**在固液分配边界上进行的选择性重构过程**。

solid → solution → solid

系统短暂回到溶液态，重新获得有限的分配控制能力，并在再次进入固相时重新定义各组分的归属。

Recrystallization = selective re‑partitioning under constrained solubility space

---

### 控制本质

Recrystallization is a control problem, not a precipitation problem.

---

### 操作目标明确化（设计前置）

重结晶可以服务于不同目的，在进入设计前必须明确：

- **除杂为主**：提升纯度，选择性分配杂质
- **转晶为主**：改变晶型/盐型，不显著改变纯度
- **除杂 + 转晶**：两者兼有

> 本章以“除杂为主”的重结晶为核心，但所建立的选择性框架同样适用于转晶或复合目标的场景。

---

## 2. Design Objective（设计目标）

> control definition

本章定义重结晶的控制目标与评价体系。后续所有模块（Selectivity Landscape、Solubility Envelope、Kinetic Stability、Downstream Interface）均围绕这些目标展开。

---

### 2.1 目标函数

maximize impurity rejection  
subject to recovery constraint

---

### 2.2 Recovery（回收率）

**定义**：  
Recovery = 1 − (S_final / S_initial)

- S_initial = 结晶前溶液中目标产物的质量  
- S_final = 结晶后母液中残留的目标产物质量

| 区间 | 状态 | 动作 |
|------|------|------|
| ≥85% | 理想 | 设计目标 |
| 80–85% | 可接受 | 可接受 |
| <80% | Hard Warning | 必须说明原因（补偿性操作除外） |
| <70% | 不可接受 | 除非有充分理由，否则应重新设计 |

#### 常见影响回收率的工程因素

- 高沸点溶剂残留（DMF、DMSO >5%）
- 共溶剂效应（co‑solvent retention）
- 盐型未完全转化
- 晶体粒径过小导致溶解损失

---

### 2.3 Impurity Rejection（去除率）

**定义**：  
Rejection = 1 − (C_solid / C_feed)

- C_solid = 结晶后固体中该杂质的浓度（质量分数）  
- C_feed = 结晶前溶液中该杂质的浓度（质量分数）

| 去除率 | 评估 |
|--------|------|
| ≥90% | 可作为主要杂质控制手段 |
| 80%-90% | 可行但不理想，需上游配合或多次结晶 |
| <80% | 不应作为主控制步骤 |

---

### 2.4 Evaluation Window（数据有效性）

**关键原则**：去除率必须在 **回收率 ∈ [40%, 85%]** 的区间内测量，数据才可信。

| 回收率区间 | 偏差 |
|------------|------|
| <40% | 去除率可能虚高 |
| >85% | 去除率可能被低估 |

---

## 3. Selectivity Landscape（选择性空间与决策框架）

> control allocation
> Gate Type: Hard Gate

本章的准入条件：在进入具体设计前，先判定本步在工艺中的角色。

---

### 3.1 可行性判定

是否存在体系使**关键杂质去除率 ≥90%** 且 **回收率 ≥80%**？

| 判定结果 | 条件 | 工艺角色 | 后续策略 |
|----------|------|----------|----------|
| **Optimal Use** | 满足 | 主杂质控制步骤 | 单次或少次结晶，回收率可维持较高 |
| **Compensatory Use** | 不满足 | 辅助步骤 | 多次结晶 + 母液套用，回收率显著下降 |

#### Failure Signal（Compensatory Use 警告）

- 需要 ≥2 次结晶才能达到纯度目标  
- 母液反复套用且纯度波动明显  
- 回收率持续低于 70%

---

### 3.2 低去除率（<70%）的应对策略

若主要杂质去除率 <70%，**应优先考虑在其他环节控制该杂质**，而非在本步进行低效重结晶。

可选路径：

- 调整反应条件（改变杂质种类/分布）
- 优化萃取/洗涤条件（利用分配差异）
- 将杂质延后至后续去除率更高的步骤

除非万不得已，避免在低去除率（<70%）的环节进行重结晶。

---

### 3.3 杂质含量匹配原则

去除率要求 ≠ 统一标准，而是 **f(杂质含量)**。

| 杂质类型 | 去除率要求 | 策略 |
|----------|------------|------|
| **Major impurity**（高含量） | ≥85% | 必须由本步承担主要去除 |
| **Minor impurity**（低含量） | 可接受 70–85%，甚至更低 | 允许本步不重点处理 |

#### Failure Signal

- 低含量杂质去除率高，但总纯度仍不达标  
  → major impurity 未被有效控制  
- 高含量杂质去除率 <85% 且无上游补偿  
  → 工艺设计缺陷

---

### 3.4 工艺含义（Hard Rule）

Selectivity 不足 → 优先回溯上游，而非继续优化结晶操作。

**Trigger**：主要杂质去除率 <80%  
→ 必须评估反应路径或粗品质量。

---

### 硬原则

> Insufficient selectivity = misallocated control authority

---

## 4. Solubility Envelope（溶解度包络）

> control space

本章定义如何构建选择性所需的溶解度空间。

---

### 4.1 单一溶剂锚点

必须找到至少一种溶剂，使**关键杂质去除率 ≥90%**（或满足匹配原则）。

- 溶剂类型（良/不良）不重要，去除能力最重要。
- 该溶剂定义 selectivity 主方向。

---

### 4.2 多杂质 → 溶剂组合

不同杂质可能对应不同溶剂，最终通过组合实现多杂质控制。

设计顺序：
1. 确定高去除率溶剂（锚点）
2. 构建良溶剂/反溶剂组合
3. 基于溶解度关系计算回收率

---

### 4.3 反溶剂的作用边界

| 影响对象 | 反溶剂作用 |
|----------|------------|
| 去除率 | 通常不破坏，但异常情况下可能改变分配路径 |
| 回收率 | 强影响（通过降低溶解度） |

**Failure Signal**：加入反溶剂后  
- 杂质分布异常  
- 去除率明显下降  
→ 表明溶剂组合改变了选择性机制，需重新评估。

---

### 4.4 ΔSolubility 驱动路径

所有结晶驱动力统一表达为 ΔSolubility。

| Path | 机制 | 典型操作 | Failure Signal |
|------|------|----------|----------------|
| **温度** | 高温溶 → 降温析 | cooling crystallization | 降温过快 → crash crystallization |
| **盐型** | free ↔ salt | pH 调节、反离子加入 | pH 偏移、含量 >100% → 盐型混合 |
| **溶剂** | good → + anti‑solvent | 反溶剂添加 | 局部暴析、细晶大量生成 |
| **晶型** | amorphous ↔ polymorph | 晶种、陈化 | 同一条件下溶解度变化、去除率波动 |

---

## 5. Kinetic Stability（动力学稳定性）

> control stability
> Gate Type: Soft Gate

本章确保结晶过程平稳、可重复，避免失控。

---

### 5.1 过饱和度控制

**核心要求**：避免瞬间过饱和度过高（burst nucleation）。

| 状态 | 表现 | 处理 |
|------|------|------|
| 正常 | 成核与生长平衡 | — |
| 暴析 | 细晶增多、过滤困难 | 升温 → 陈化 → 粒径放大 |

**Trigger**：过饱和快速建立 → 高风险。

---

### 5.2 晶种控制

**操作规则**：必须使用晶种，seed loading ≥1%（建议 1–5%）。

**Failure Signal**：
- 起晶延迟  
- 批间收率波动 >5%  
→ 晶型不稳定或晶种失效

---

### 5.3 粒径效应

| 变化方向 | 对回收率影响 | 对去除率影响 |
|----------|--------------|--------------|
| 粒径↑ | 轻微↑ | 基本不变 |
| 粒径↓ | 轻微↓ | 基本不变 |

**判别规则**：
- Recovery 变化 + Rejection 稳定 → 粒径效应
- Recovery 变化 + Rejection 变化 → 晶型变化

---

## 6. Downstream Interface（下游接口）

> control loss
> Gate Type: Soft Gate

本章确保结晶产物在后续固液分离、干燥等操作中可处理，不引入额外风险。

---

### 6.1 固液分离与母液残留

**指标**：Wet/Dry = 湿重 / 干重

| 区间 | 评估 |
|------|------|
| <1.2 | 良好，易过滤 |
| 1.2–1.5 | 可接受，注意颗粒度 |
| 1.5–2.0 | 高风险，需优化过滤或离心 |
| >2.0 | 不可接受，母液残留严重 |

**Failure Signal**：纯度异常但结晶本身无问题 → 母液夹带。

---

### 6.2 与结晶参数的关联

- 粒径过小 → 过滤困难、干湿比升高
- 晶型不稳定 → 可能影响滤饼结构
- 暴析 → 细晶堵塞滤层

---

## 7. #Audit（影子指标）

| 指标 | 含义 | Trigger / 记录点 |
|------|------|------------------|
| `Selectivity_major` | 主杂质去除率 | <80% 触发重新评估 |
| `Recovery_loss_flag` | 多次结晶累计损失 | >15% 记录 |
| `Rejection_variance` | 批间去除率波动 | >10% 需调查 |
| `Solubility_ratio_shift` | 溶解度变化倍数 | >2× 记录 |
| `Wet_cake_ratio` | 干湿比 | >1.5 警告，>2.0 硬触发 |
| `Crash_flag` | 暴析发生 | 出现即记录 |
| `Polymorph_drift` | 晶型漂移 | 收率波动 >5% 记录 |

---

## #Audit 总结

Recrystallization 的真正风险，  
不是“结晶失败”，  
而是“在错误的选择性前提下仍继续结晶”。

## 8. Machine Annotation

```yaml
schema_version: "risk_annotation_schema_v0.2"
annotation_scope: "chapter_level"
canonical_id: "ISOL-002-RECRYSTALLIZATION"
process_stage: "isolation_recrystallization"

transition_model: "solid_to_solution_to_solid_under_constrained_solubility_space"

control_window: >
  Recrystallization temporarily regains limited solution-phase control by dissolving a solid inventory and re-partitioning product and impurities before the system re-enters solid state. This control window is narrower than primary crystallization and must be justified by selectivity rather than by the ability to precipitate solids again.

core_judgment: >
  Recrystallization is structurally valid only when it provides meaningful impurity discrimination under an acceptable recovery constraint. The central failure mode is not crystallization failure itself, but continued optimization under an invalid selectivity premise.

review_gates:
  hard_gate:
    - "key_impurity_rejection >= 90% and recovery >= 80% indicates optimal use as a main impurity-control step"
    - "major_impurity_rejection < 80% requires upstream reassessment rather than continued recrystallization optimization"
    - "major_impurity_rejection < 70% indicates recrystallization should usually not be used as the main control step"
  soft_gate:
    - "recovery < 80% requires justification unless the step is intentionally compensatory"
    - "recovery < 70% is generally unacceptable without strong process rationale"
    - "wet_cake_ratio > 1.5 indicates downstream handling risk"
    - "wet_cake_ratio > 2.0 indicates severe mother liquor retention risk"

risk_signals:
  - "key impurity rejection < 80%"
  - "major impurity rejection < 85% without upstream compensation"
  - "recovery persistently < 70%"
  - "two or more recrystallizations required to meet purity target"
  - "mother liquor recycle required with unstable purity"
  - "rejection measured outside recovery evaluation window"
  - "recovery < 40%, causing apparent rejection to appear artificially high"
  - "recovery > 85%, causing rejection to appear artificially low"
  - "antisolvent addition causes abnormal impurity distribution"
  - "rejection decreases after solvent combination change"
  - "rapid supersaturation buildup or burst nucleation"
  - "delayed nucleation after seeding"
  - "batch yield fluctuation > 5%"
  - "recovery changes while rejection remains stable"
  - "recovery and rejection change together"
  - "wet_cake_ratio > 1.5"
  - "wet_cake_ratio > 2.0"
  - "crash crystallization observed"
  - "polymorph drift suspected"
  - "solubility_ratio_shift > 2x"

expert_judgment:
  - "If selectivity is insufficient, continued recrystallization optimization is likely a misallocation of control authority."
  - "If major impurity rejection is low, the impurity should usually be controlled upstream or in a different step rather than forced through repeated recrystallization."
  - "If acceptable purity requires repeated recrystallization and mother liquor recycle, the step is compensatory rather than optimal and should be treated as structurally weak."
  - "If rejection is measured outside the recovery evaluation window, the data may not represent true impurity discrimination."
  - "If antisolvent addition changes impurity rejection, the solvent combination has altered the selectivity mechanism and must be re-evaluated."
  - "If recovery varies while rejection remains stable, particle-size or handling effects may dominate."
  - "If recovery and rejection vary together, solid form or selectivity drift should be suspected."
  - "If wet cake retention is high, apparent impurity rejection may be negated by mother liquor carryover."

reasoning_anchors:
  - "limited_control_regain"
  - "selective_repartitioning"
  - "constrained_solubility_space"
  - "selectivity_landscape"
  - "misallocated_control_authority"
  - "recovery_constraint"
  - "evaluation_window"
  - "solubility_envelope"
  - "delta_solubility_path"
  - "kinetic_stability"
  - "burst_nucleation"
  - "solid_form_drift"
  - "mother_liquor_retention"
  - "downstream_interface"

quantitative_triggers:
  key_impurity_rejection_main_control: ">=90%"
  major_impurity_rejection_minimum: ">=85%"
  upstream_reassessment_trigger: "<80%"
  low_rejection_warning: "<70%"
  ideal_recovery: ">=85%"
  acceptable_recovery: "80-85%"
  recovery_hard_warning: "<80%"
  recovery_unacceptable_without_rationale: "<70%"
  valid_rejection_evaluation_window: "recovery 40-85%"
  rejection_variance_investigation: ">10%"
  solubility_ratio_shift_record: ">2x"
  wet_cake_ratio_warning: ">1.5"
  wet_cake_ratio_hard_trigger: ">2.0"
  polymorph_drift_signal: "yield fluctuation >5%"
  seed_loading_recommendation: "1-5%"

uncertainty: "medium"

exceptions:
  - "Low recovery may be acceptable if the step is intentionally compensatory and mother liquor recovery or recycle is designed and controlled."
  - "A lower rejection threshold may be acceptable for minor impurities if major impurities are already controlled elsewhere."
  - "A high rejection value is not reliable when measured at very low recovery."
  - "Repeated recrystallization may be acceptable for high-value products, but should be recorded as a compensatory strategy rather than an optimal design."
  - "Antisolvent-driven recovery improvement is acceptable only if the selectivity mechanism remains unchanged."
  - "Particle-size-related recovery loss should not be misclassified as poor impurity selectivity."

machine_use: >
  Use this annotation to review whether a proposed recrystallization design has a valid selectivity premise, whether impurity rejection is evaluated under a meaningful recovery window, whether control authority is being misallocated to a low-selectivity step, and whether downstream mother liquor retention or kinetic instability may invalidate the apparent purification benefit.

