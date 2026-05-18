---
snapshot_id: "ISOL-003-FILTRATION"
status: "draft"
domain: "Process"
process: "Isolation"
topic: "过滤：在无组成控制能力前提下的固液分离"
level: "001"
language: zh  
canonical_id: ISOL-003-FILTRATION
dependencies:
  - "ISOL-001-CRYSTALLIZATION"
  - "ISOL-002-RECRYSTALLIZATION"
  - "WRKUP-003-SOLVENT-REMOVAL-DRIVEN-ACCUMULATION-AND-THERMAL-EXPOSURE-CONTROL"
note:
  - "面向 machine-review：过滤不是新的分离设计，而是 solid-state commitment 之后的 consequence-stage separation；其核心任务是在固定固液状态下最小化损失放大，并识别何时应回到上游重构固体生成路径。"
---

# ISOL-003：过滤

## 1. 系统角色

过滤位于 ISOL-002（重结晶）之后、ISOL-004（干燥）之前，处于 **固态锁定** 已发生之后的第一个分离节点。

其在 OpenChemProcess 链条中的位置可表示为：

溶液态控制
→ 固态锁定
→ 过滤
→ 干燥

本章定义如下：

> **过滤 = 在无组成控制能力前提下的固液分离**

该步骤不再属于 **控制阶段**，而属于 **结果阶段**。

进入过滤时，以下对象默认已由上游锁定：

- 产品 / 杂质分布
- 晶型
- 粒径分布（PSD）
- 颗粒形貌
- 成饼倾向
- 液体滞留倾向

因此，过滤阶段：

- 不重新定义组成分配
- 不重新定义固体结构
- 不重新创造纯度
- 不重新创造收率

过滤阶段仅处理：

- 已形成固液状态的分离兑现
- 损失的显化与放大
- 下游干燥起始条件的设定

**控制权 ≈ 0**

实验室阶段对过滤风险存在系统性掩盖：

- 物料量小 → 滤饼薄、路径短、阻力低
- 有效过滤面积相对更大
- 绝对分离时间不敏感
- 母液残留通常未被量化

因此：

> **小试可接受 ≠ 工业可操作**

过滤的放大敏感性本质不是新的控制窗口，而是 **放大敏感性失效**。

---

## 2. 设计目标与控制定义（Design Objective / Control Definition）

过滤的主目标不是“把固体滤出来”，而是：在既定的固液状态下损失最小化

最小化对象包括：

- 母液滞留
- 过滤时间
- 下游干燥负担

控制定义如下：

> **过滤不改变结果；过滤只改变实现结果的代价。**

因此，本章的目标函数不是新的杂质判别，也不是新的固体形态选择，而是：

- 以最小损失兑现既有固液分离结果
- 以最小损失把既有问题向下游传递
- 在分离节点识别是否已进入路径级失败

过滤阶段不追求：

- 对上游失败的结构性修复
- 对粒径分布的再构建
- 对晶体形貌的再设计
- 对产品 / 杂质分配的再定义

---

## 3. 核心机制与约束（Core Mechanism / Core Constraint）

### 3.1 结构继承性（Structure Inheritance）

过滤性能首先是上游固体结构的函数，而不是过滤动作本身的函数。

关键决定因素包括：

- 粒径分布
- 形貌
- 细粉比例
- 堆积结构
- 毛细滞留倾向

核心判定：

> **过滤性能差，首先是固体结构问题，其次才是操作问题。**

---

### 3.2 中心变量：母液残留（Mother Liquor Retention）

本章中心变量不是单纯的分离时间，而是：

母液残留

母液残留直接决定：

- 杂质夹带
- 湿滤饼负担
- 滤饼中溶剂库存
- 下游干燥难度

其后果链为：

高残留  
→ 杂质夹带  
→ 纯度侵蚀  
→ 溶剂负荷增加  
→ 干燥负担增加  
→ 周期时间增加

---

### 3.3 缓解边界（Mitigation Boundary）

过滤阶段仍可进行的动作仅属于 **结果管理**，不属于 **根因修复**。

| 可做的事        | 不能做的事      |
| ----------- | ---------- |
| 设备路径改变      | 生成更好的晶体    |
| 洗涤 / 喷淋     | 去除根本性细粉问题  |
| 薄层处理        | 重建粒径分布     |
| 省去过滤环节/连投   | 恢复已丧失的控制权  |
| 更换路线中结晶分离位点 | 从结构上修复上游失败 |

核心边界：

> **在不重构上游的前提下优化过滤，本质是补偿，而不是控制。**

---

## 4. 放大敏感性（放大敏感性）

过滤的放大敏感性表现为：实验室中被薄层、短路径、量小掩盖的问题，在放大中转化为显性可操作性问题。

放大因素包括：

- 滤饼厚度增加
- 压降累积
- 渗透性非线性下降
- 洗涤效率下降
- 滞留后果显化

因此，本章的放大本质为：

可放大性失效

核心句：

> **小试中的“还能做完”，不等于放大中的“可持续运行”。**

---

## 5. 非理想结果（非理想结果）

本章中的失败不定义为“过滤操作失误”，而定义为：

> **上游固体结构问题在分离阶段的显化模式**

### 5.1 物理层失效

|表现|上游原因|下游后果|
|---|---|---|
|通量非线性下降|细粉比例高|时间延长|
|穿滤|滤层不均|收率损失|
|湿重比高（≥2）|颗粒过细|干燥负担高|

---

### 5.2 杂质层失效

|表现|上游原因|下游后果|
|---|---|---|
|洗涤无法进入滤饼|滤饼致密|杂质残留|
|高沸点溶剂残留|洗涤不足|干燥团聚|
|低沸点优先挥发|未置换|表面溶解|

---

### 5.3 决策层失效

|表现|根源|
|---|---|
|放大低估难度|小试掩盖|
|未识别湿重比|上游未设计|
|薄层已困难仍推进|路径不可操作|

---

## 6. 决策逻辑（Decision Logic）

### Gate 1｜问题归属

若出现以下任一情况：

- 低渗透性
- 高母液残留
- 中等堵塞
- 湿滤饼不稳定

则优先判断：

上游固态来源 = 高概率原因

而非优先判断：

过滤操作错误

---

### Gate 2｜是否仍有上游控制权

若上游结晶 / 重结晶路径仍可调整：

返回上游

优先调整：

- 过饱和路径
- 熟化 / 晶体生长
- 溶剂体系
- 盐型 / 晶型
- 固体生成路径

---

### Gate 3｜是否进入路径级问题

若满足以下任一条件：

- 湿重比（WMR）≥ 2
- 小试过滤已明显困难
- 洗涤无法维持杂质去除
- 下游干燥负担成为主导

则判断：

当前固液分离路径 = 结构性薄弱

---

### Gate 4｜何时不再优化过滤

若满足：

- 湿重比（WMR）≥ 3
- 放大可操作性无法成立
- 过滤仅依赖强补偿手段

则优先策略不是“继续优化过滤”，而是：

需要工艺重构

路径包括：

- 改变固体形态
- 改变盐型
- 串联（telescope）
- 跳过当前固体分离节点
- 切换至替代分离路径
---

## 7. #Audit: 本章核心影子指标（Shadow Indicators）

---

### 7.1 影子指标

| 指标           | 阈值                                  | 意义                         |
| ------------ | ----------------------------------- | -------------------------- |
| **湿重比（WMR）** | <1.2：低风险；1.2–1.5：需关注；≥2：高风险；≥3：不可放大 | 分离效率与母液夹带的直接表征；决定干燥负荷与杂质残留 |
| **母液残留分数**   | 由工艺定义                               | 直接影响纯度与干燥时间                |
| 分离时间与滤饼厚度的关系 | 出现非线性增长即为风险信号                       | 识别实验室掩盖效应的关键判据             |
| **洗涤置换效率**   | 洗涤液组成 vs 残留液组成                      | 判断洗涤是否真正完成溶剂状态置换           |

---

### 7.2 审计要求

1. **WMR 的测定时点前移**  
    WMR 不是过滤操作指标，而是由上游固体结构决定的分离行为表征。WMR 应在固体刚形成时（结晶 / 重结晶后）测定，用于预测后续过滤风险。
2. **过滤问题必须向上游追溯**  
    若 ISOL-003 出现低渗透性、高残留或堵塞，归因不应停留在设备层面，而应追溯至结晶 / 重结晶的颗粒结构与固体生成路径。
3. **实验室掩盖效应必须单独审计**  
    小试“可快速完成”不代表放大可行；必须结合 WMR、滤层结构与单位质量分离时间共同判断。
4. **设备改变路径时必须区分“路径改变”与“控制恢复”**  
    若设备选型改变了工艺路径（如省略打浆、缩短干燥），属于有效结果管理；不应误判为控制权恢复。

---

### 7.3 本质总结

#Audit: 过滤不是新的分离设计；它是上游固体结构的结果兑现。  
#Audit: 如果问题第一次在过滤阶段被清晰看见，问题通常不产生于过滤阶段。  
#Audit: 过滤能调节的是损失的表现形式，而不是损失的来源。  
#Audit: 湿重比不是过滤技巧指标，而是控制权消失后的结构投影。

## 8. Machine Annotation

```yaml
schema_version: "risk_annotation_schema_v0.2"
annotation_scope: "chapter_level"
canonical_id: "ISOL-003-FILTRATION"
process_stage: "isolation_filtration"

transition_model: "solid_state_commitment_to_consequence_stage_separation"

control_window: >
  Filtration occurs after solid-state commitment. Product/impurity distribution, polymorph, PSD, morphology, cake-forming tendency, and liquid-retention tendency are already inherited from upstream solid formation. Filtration has little to no composition control authority and mainly manages loss realization, mother-liquor carryover, washing effectiveness, and downstream drying burden.

core_judgment: >
  The central machine-review task is to detect whether a filtration problem is being misattributed to filtration operation when it is more likely a manifestation of upstream solid-structure failure. Filtration optimization without upstream restructuring should be treated as compensation rather than restored control authority.

review_gates:
  problem_attribution_gate:
    - "low permeability"
    - "high mother liquor retention"
    - "moderate clogging"
    - "unstable wet cake"
    - "nonlinear flux decline"
  upstream_control_gate:
    - "if crystallization or recrystallization path remains adjustable, return upstream before optimizing filtration"
    - "review supersaturation path, aging/crystal growth, solvent system, salt form, polymorph, and solid formation pathway"
  path_level_failure_gate:
    - "WMR >= 2"
    - "lab filtration already difficult"
    - "washing cannot sustain impurity removal"
    - "drying burden dominates downstream"
  redesign_gate:
    - "WMR >= 3"
    - "scale operability cannot be established"
    - "filtration relies only on strong compensatory measures"

risk_signals:
  - "WMR >= 2"
  - "WMR >= 3"
  - "wet cake ratio >= 2"
  - "lab filtration already difficult"
  - "low permeability"
  - "nonlinear flux decline"
  - "nonlinear increase of separation time with cake thickness"
  - "high mother liquor retention"
  - "mother liquor retention not quantified"
  - "moderate clogging"
  - "unstable wet cake"
  - "high fines fraction"
  - "dense or compressible cake"
  - "wash cannot penetrate cake"
  - "washing cannot sustain impurity removal"
  - "washing displacement efficiency not demonstrated"
  - "breakthrough due to non-uniform cake"
  - "high-boiling solvent retention"
  - "preferential evaporation of low-boiling solvent without solvent exchange"
  - "drying burden dominates downstream"
  - "thin-layer lab filtration difficulty ignored"
  - "filtration relies only on strong compensatory measures"
  - "scale operability cannot be established"

reasoning_anchors:
  - "control_authority_decay"
  - "solid_state_commitment"
  - "misallocated_control_authority"
  - "mother_liquor_retention"
  - "downstream_filtration_compatibility"
  - "downstream_interface"
  - "consequence_stage_separation"
  - "loss_amplification_interface"
  - "structure_inheritance"
  - "upstream_failure_exposure"
  - "lab_scale_masking"
  - "scalability_failure"
  - "wet_mass_ratio"
  - "washing_displacement_efficiency"
  - "compensatory_filtration"

taxonomy_role:
  reused_formal_anchors:
    - "control_authority_decay"
    - "solid_state_commitment"
    - "misallocated_control_authority"
    - "mother_liquor_retention"
  reused_candidate_terms:
    - "downstream_filtration_compatibility"
    - "downstream_interface"
  candidate_anchors:
    - "consequence_stage_separation"
    - "loss_amplification_interface"
    - "structure_inheritance"
    - "upstream_failure_exposure"
    - "lab_scale_masking"
    - "scalability_failure"
    - "wet_mass_ratio"
    - "washing_displacement_efficiency"
    - "compensatory_filtration"

expert_judgment:
  - "Poor filtration performance should first be reviewed as a possible upstream solid-structure problem, not as a filtration operation error."
  - "Filtration does not recreate purity, yield, PSD, morphology, polymorph, or product/impurity partitioning; it only realizes the already formed solid-liquid state."
  - "WMR is not merely a filtration metric; it is a projection of upstream solid structure after control authority has largely disappeared."
  - "Lab-scale completion is not evidence of scale operability because thin cake, short path, small inventory, and unquantified retention can mask filtration risk."
  - "Changing equipment or separation path may be valid outcome management, but it should not be mislabeled as recovery of composition control authority."
  - "When WMR is high, washing fails, or drying burden dominates, the review should consider upstream restructuring or path redesign rather than continued filtration optimization."

uncertainty_and_exceptions:
  - "Filtration equipment changes may be acceptable when they reduce loss realization or change the separation path, but they should not be interpreted as root-cause repair unless upstream solid formation changes."
  - "WMR thresholds are review triggers, not universal deterministic rejection rules; interpretation depends on product value, impurity risk, drying constraints, equipment path, and scale."
  - "Washing failure should not be inferred from wet cake mass alone unless supported by residual liquid composition, impurity carryover, or displacement-efficiency evidence."
  - "High mother-liquor retention may be tolerable only when impurity carryover, solvent inventory, and downstream drying burden remain acceptable under scale-relevant conditions."

quantitative_triggers:
  wmr_low_risk: "<1.2"
  wmr_watch: "1.2-1.5"
  wmr_high_risk: ">=2"
  wmr_non_scalable_trigger: ">=3"
  wet_cake_ratio_high_burden: ">=2"
  nonlinear_cake_thickness_signal: "nonlinear increase of separation time with cake thickness"
  washing_displacement_check: "washing liquid composition vs residual liquid composition"

required_review_fields:
  - "WMR"
  - "mother_liquor_retention_fraction"
  - "filtration_time_or_flux_profile"
  - "cake_thickness_or_scale_basis"
  - "washing_displacement_efficiency"
  - "drying_burden_assessment"
  - "upstream_solid_structure_assessment"
  - "scale_operability_assessment"
  - "compensatory_measures_if_any"
  - "upstream_restructuring_option_if_any"

machine_use: >
  Review whether a filtration difficulty should be attributed to inherited solid structure rather than filtration operation, whether WMR and mother-liquor retention have been quantified early enough, whether lab-scale masking has been addressed, and whether the process has crossed from manageable loss realization into path-level failure requiring upstream restructuring or separation-path redesign.

```
