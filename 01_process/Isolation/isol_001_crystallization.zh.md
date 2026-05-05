---
snapshot_id: "ISOL-001-CRYSTALLIZATION"
status: "draft"
domain: "Process"
process: "Isolation"
topic: "一次结晶：从 solution-phase control 到 solid-state commitment"
level: "001"
language: zh  
canonical_id: ISOL-001-CRYSTALLIZATION
dependencies:
  - "WRKUP-003-SOLVENT-REMOVAL-DRIVEN-ACCUMULATION-AND-THERMAL-EXPOSURE-CONTROL"
  - "WRKUP-002-PARTITION-RATIO-DRIFT-INVENTORY-CONTROL"
  - "MIX-001-MIXING-TIME-SCALE-FAILURE"
  - "THR-001-THERMAL-CONTROL-AUTHORITY"
note:
  - "面向 machine-review：以回收率、first-pass impurity rejection、过饱和控制与固态形式控制共同定义一次结晶的控制窗口与放大风险。"
---

# ISOL-001：结晶（Crystallization）

## 1. 系统角色 (System Role)

结晶是 OpenChemProcess 序列中**第一个相转变：液相至固相的单元操作**。

前序章节（WRKUP-001 至 WRKUP-003）均在**液相世界**中运作：操作者可以通过溶剂组成、相比例、温度、浓度、酸碱状态、转相与浓缩等变量，持续、可逆地改变体系未来的演化路径。结晶一旦发生，**控制权发生根本性转移**：体系从以溶液分布为主的可调节状态，进入以固体形态为主的部分锁定状态。

其核心转移可表示为：

```text
solution inventory → solid inventory
solution-phase control → solid-state commitment
```

因此，本章的核心定义是：

> **Crystallization is the transition from solution-phase control to solid-state commitment.**

固态锁定’并非指所有性质完全不可变，而是指：一旦 product 进入固相，后续可调自由度显著减少；晶型、盐型、形貌、母液夹带等问题在此阶段形成后，后续单元只能处理其后果，难以逆转其来源。

因此，ISOL-001 的重点不是把结晶写成传统教材中的晶体学理论综述，而是要回答一个更工艺化的问题：

> **如何在仍然存在 solution-phase control 的最后窗口内，把 product 以尽可能高的回收率、并带着尽可能少的高含量杂质，送入 solid phase。**

## 2. 设计目标 (Design Objectives)

### 2.1 一次结晶的首要目标：最大回收率

一次结晶（primary crystallization）的首要目标是：

```text
maximum product recovery
```

即尽可能让 product 从 workup 后的溶液体系中脱离出来，进入可分离、可转运、可进一步处理的固体状态。

在这一步，所得固体**不必已经是最终最优固态形式**。允许出现：
- imperfect crystals
- impurity-containing crystals
- amorphous solids
- poorly defined morphology
- non-final polymorph
- salt / hydrate / solvate forms

判据是：该固体能够完成有效的 product isolation，并为后续固液分离创造条件。

### 2.2 一次结晶的第二任务：first-pass impurity rejection

一次结晶首要目标：回收；并行目标：杂质剥离 (Primary Objective: Recovery; Concurrent Objective: Impurity Rejection）。

这里所说的 impurity，主要不是 ppm 或痕量 level 的 minor impurity，而是 bulk impurities，例如：
- 反应溶剂或高沸点残留溶剂
- 反应中使用的酸、碱、有机碱
- 未反应原料
- 高含量副产物
- 原料或产物分解产物
- 萃取中带入或残留的水、盐、有机酸、无机酸、有机碱、无机碱
- 其他显著改变 product 溶解行为的 residual modifiers

经验上：
- 杂质含量 **≥10 wt%** 时需要关注
- 杂质含量 **≥20 wt%** 时通常必须在工艺中明确设计其去除路径

因此，一次结晶的正确提问方式不是：“这个产物能不能析出来？”而应是：“体系里哪几种高含量组分必须尽量留在母液中，不能带进固体中？”

### 2.3 与重结晶的边界

一次结晶与重结晶的优化目标不同。
- **Crystallization = isolation + first-pass impurity rejection**
- **Recrystallization = purification + impurity discrimination**

前者首先追求 recovery，后者首先追求 purity。  
前者主要处理 bulk impurities，后者主要处理 structurally similar minor impurities 或难去除痕量杂质。

因此，本章不把一次结晶写成 final purification，而把它界定为：

> **高回收率前提下的第一次定向杂质剥离。**

## 3. 溶解度工程 (Solubility Engineering)

### 3.1 核心设计逻辑：从 workup solution 到最低溶解度条件

一次结晶设计的起点，不是先讨论晶体长得是否完美，而是先回答：

> **在什么条件下，product 的溶解度最低？**

也就是：

```text
find minimum solubility state
drive workup solution toward minimum solubility condition
```

这里的起点应明确为：

```text
workup solution
```

而不是原始 reaction mixture。结晶通常面对的是已经历经后处理、萃取、相转移、浓缩之后的 solution inventory，而不是未经整理的反应液本身。

决定这一最低溶解度状态的因素通常包括：
- solvent type
- solvent mixture ratio
- temperature
- salt form
- polymorph
- hydrate / solvate formation
- ionic strength / phase environment

结晶设计的核心，是把当前的 workup solution 逐步推向这一最低溶解度条件。

可用的实现方式包括：
- 冷却（cooling）
- 溶剂交换（solvent exchange）
- 反溶剂加入（anti-solvent addition）
- 溶剂组成改变（solvent composition change）
- 成盐（salt formation）
- hydrate / solvate 诱导
- 优先去除显著提高 product 溶解度的组分

### 3.2 经验性溶解度分级 (Empirical Solubility Classification)

在工艺开发中，结晶体系可先用经验性溶解度窗口进行初筛。

对于一次结晶，通常要求 product 在“不良溶剂”中的溶解度足够低，在“良溶剂”中的溶解度足够高，以形成可利用的溶解度差。

经验上可参考：
- **不良溶剂 (anti-solvent)**：product 溶解度应 **< 1 g / 15 g 溶剂**  
  更理想时应低于 **1 g / 30 g 溶剂**
- **良溶剂 (good solvent, usually with heating)**：product 溶解度应 **> 3 g / 10 g 溶剂**

这些数值只是工艺开发中的经验范围，**不是固定标准**；具体阈值仍需根据产品价值、目标收率、操作温度、过滤损失及后续纯化需求调整。

> 对一次结晶而言，理想体系通常要求：**热态可充分溶解，冷态或加入反溶剂后溶解度显著下降。** 关键判据不是单点溶解度绝对值，而是 **工艺可利用的溶解度差 (usable solubility gap)**。

### 3.3 纯品溶解度与粗品溶解度必须分开测

> **核心规则：溶解度测量必须区分“纯品”与“粗品”。**

**操作原则：**
1. 先测量 **高纯度产物（约93–97%以上）** 的溶解度基准
2. 再测量 **粗品体系** 在同一结晶体系中的溶解度

**判断逻辑：**
- 如果 `纯品溶解度 ≈ 粗品溶解度` → 适合直接结晶
- 如果 `粗品溶解度 >> 纯品溶解度`（**差异达到 2–3 倍或以上**）→ 粗品中存在显著提高溶解度的组分

**分析思路：**
这类影响显著的杂质通常在体系中含量较高（**5–20% 质量比例**），可通过反应平衡、质量平衡推理来源，并在前处理步骤中去除。

### 3.4 杂质对溶解度的改变

在一次结晶中，应以纯品溶解度作为结晶体系判据；粗品溶解度偏高时，应优先判定为助溶组分干扰，并通过前处理消除，而不应调整结晶体系本身。

**案例 #1：五氟苯酚提高 product 溶解度**  
酯化反应后，当量级副产物五氟苯酚具有一定酸性和脂溶性，显著提高 product 在有机相中的溶解度。通过将后处理溶液切换至 DCM / MTBE 结晶体系，product 溶解度极低而析出，五氟苯酚则留在母液中。

**案例 #2：DMF 残留导致结晶失效**  
DMF 沸点高，浓缩后仍有 5–10% 残留，显著提高产物在低溶解度体系中的溶解能力。通过加强萃取将 DMF 去除至 1% 以下，结晶恢复正常。

### 3.5 溶剂合物与水合物

某些 product 能够形成 **solvate / hydrate**，并由此显著改变其溶解度与结晶行为。

**案例 #3-A：DCM solvate**  
索菲布韦某晶型为 DCM solvate。在体系中加入 >1 eq DCM 诱导形成溶剂合物后，溶解度显著降低，产物完全析出，回收率大幅提高。

**案例 #3-B：hydrate**  
某产物在 DCM 中难以直接析晶，但加入 >1 eq 水后形成 hydrate，溶解度显著降低并以固体形式析出。尽管 DCM 与水不互溶，hydrate 仍可成为关键固态中介。

**常见类型：**
羧酸、胺、氨基酸类化合物较易形成水合物（氢键稳定）。

因此，solvate / hydrate 不应视为附带现象，而应视为 **一次结晶可主动利用的设计变量**。

### 3.6 成盐结晶 (Salt Formation Crystallization)

当目标产物为胺或酸时，可通过成盐改变溶解度，诱导结晶析出。

**关键研究点：**
- 测量 `free form 溶解度` 与 `salt form 溶解度` 并比较
- 多酸体系需关注 **1:1 盐、1:2 盐** 等不同盐型

**复杂情况（两性分子）：**
同时含酸性与碱性官能团的分子（如含磷酸基与氨基），可能存在钠盐、内盐、酸式盐的平衡。

**#案例6（盐型平衡）**  
若过饱和形成过快，可能出现**多种盐型同时结晶析出**。表现为含量偏差 1–2%、pH 偏差、离子摩尔比偏差。

**#案例7（free form 与盐共结晶）**  
当 `free form 溶解度 > salt form 溶解度` 但差异较小时，若加酸/碱过快、降温过快，可能发生 free form 与 salt 共结晶。表现为产品含量略高于标准品（100–101%）、回收率低于理论值、产品中混入 3–5% free form。

## 4. 过饱和控制 (Supersaturation Control)

### 4.1 过饱和不是越高越好，而是一个控制窗口

过饱和度是结晶的唯一驱动力，也是最关键的可调变量。但过饱和并非越高越好：过低则结晶缓慢或无法启动，过高则可能引发非理想析出（暴析、油析、多晶型失控等）。因此，工艺控制的核心是以合适速率建立过饱和，并以可控方式消耗过饱和，使体系始终处于**过饱和控制窗口**内。

实现这一目标的手段包括：
- 冷却速率控制
- 反溶剂加入速率控制
- 加酸 / 加碱速率控制
- 晶种引入
- 在析晶温度点保温（熟化）
- 控制局部浓度梯度（加料点、搅拌）

这里不将 MSZW 作为中心概念，而强调实验可观察的**操作窗口**：即体系能够稳定结晶而不发生失控的范围。

### 4.2 暴析 (Crash Crystallization)

若过饱和在短时间内建立过快，体系就可能转入暴析。

暴析的常见后果包括：
- 晶体形貌不规则
- 表面积显著增大
- 细晶增多
- 杂质夹带加重
- 过滤性变差
- 溶解损失增大
- 回收率与纯度同时受损

**案例 #8：放大过程中的暴析**  
小试中常在玻璃瓶里缓慢降温搅拌过夜，看似“缓慢结晶”；但放大体系通常是主动降温析晶，如果到达析晶温度后仍继续快速降温或加反溶剂，就会积累更高过饱和，最终暴析。因此小试阶段必须提前识别：
- 开始析晶的温度点
- 固体析出的速度
- 该温度下需要停留多久才能消耗过饱和

### 4.3 局部过饱和与加入顺序

总体浓度并不极端不代表局部没有问题。在加入反溶剂、加酸、加碱时，局部加料点附近可能瞬间形成极高过饱和，进而导致局部暴析、非目标固态形式、细晶、油析或多盐型共析。

工业上通常通过缓慢加料、合理加料点、移动泵等方式降低风险。此外，反溶剂加入顺序也会改变过饱和轨迹：
- 通常采用 `antisolvent → product solution`（反溶剂加入产品溶液）
- 但在某些体系中，若 product 在反溶剂中几乎不溶，也可采用 `product solution → antisolvent`，该方式会影响成核与生长路径。

## 5. 成核与晶种 (Nucleation and Seeding)

很多体系不加晶种也会自己结晶，因此容易低估晶种的重要性。晶种的意义不仅是“帮助起晶”，更在于：
- 提供优势成核中心
- 缩短诱导期
- 引导目标固态形式
- 使过饱和优先在既定表面消耗
- 提高结晶过程的重现性与放大可控性

因此，晶种虽然不一定是绝对必须步骤，但通常应视为重要的 **control safeguard**。

**案例 #4：放大时起晶失效**  
小试中加晶种后 15–30 分钟即可顺利结晶；放大后长时间搅拌不析晶，即使补加晶种也无效。最终通过延长搅拌、继续补种，甚至先取样在小体系中形成稳定 slurry 后再回加，才逐步建立顺畅析晶。该案例说明：小试能结出来，并不等于放大能稳定结出来。

经验上，初次放大时应特别关注：
- 诱导期是否明显延长
- 晶种加入量是否过少（建议 **1–5%**）
- 晶种是否真正形成优势结晶中心

## 6. 固态形式控制 (Solid Form Control)

一次结晶虽然以回收为主，但这并不意味着可以忽略固态形式。在 ISOL-001 中，关注固态形式的核心目的是**选择有利于高回收率的最低溶解度形式**，而不是最终产品意义上的“确定最终目标晶型”。

一次结晶中至少应关注：
- polymorph
- hydrate
- solvate
- salt form
- mixed solid forms

### 6.1 批间固态形式一致性监测

在长期生产中，晶型或固态形式漂移可能导致结晶行为、溶解度、收率、质量波动。当生产中出现收率变化超过约 **5%**（无论升降），应优先排查是否出现固态形式变化。

建议逐步建立 `IR_form_consistency_flag` 作为批间固态形式一致性的抽查指标。

**案例 #5：长期生产中的固态形式漂移**  
某产品连续生产数十批次后，收率突然下降 6%，经 IR 比对发现晶型已从稳定晶型转为亚稳晶型，溶解度升高导致结晶不完全。调整结晶条件（引入晶种、控制降温速率）后恢复。

### 6.2 不稳定产物的固态形式策略

对于稳定性较差的产物（如醛类、易消旋化合物、在粗品中会继续反应的中间体），一次结晶的优先级更前移：目标是**快速将 product 从反应体系中脱离**，避免长时间接触杂质。此时应选择溶解度极低的体系，必要时采用稳定的中间固态形式（如盐、亚硫酸氢钠加成物）实现快速隔离。

**案例 #8 补充**：对于不稳定 product，一次结晶是针对化学不稳定物种的快速隔离策略，真正的纯度精制留待重结晶。

## 7. 放大敏感性 (Scale Sensitivity)

结晶是一个高度 scale-sensitive 的单元操作。热力学正确并不保证放大成功，因为结晶是**动力学主导**的过程，对设备条件极其敏感。

放大中的关键差异来源包括：
- 加热 / 冷却速率
- 釜体热惯性与保温性
- 搅拌强度与局部流场
- 反溶剂加入速率与位置
- 晶种分散效率
- 诱导期延长

这些因素共同决定过饱和的形成方式、成核能否顺利启动、生长是否占优势，以及下游过滤是否可行。

### 7.1 热力学正确 ≠ 放大可行

**小试阶段必须考察的动力学参数：**
- 析晶温度点
- 析晶速度
- 过饱和形成与消耗速度
- 晶种有效性

**案例 #4** 和 **#8** 已说明：小试有效的条件在放大时可能因热历史、混合效果改变而失效。

### 7.2 与过滤的接口 (Interface to Filtration)

一次结晶不能只看产品是否析出，还需评估后续过滤的可行性：
- 晶体形态是否易于过滤（针状、片状、块状）
- 粒度分布是否导致过滤时间过长或洗涤困难
- 母液保留率是否影响杂质去除

经验上，可关注**湿重与干重比**所反映的母液夹带水平：
- **湿重 < 干重 × 1.2**（夹带母液 < 20% 干品重量）：通常较安全
- **湿重 ≥ 干重 × 1.5**（夹带母液 ≥ 50% 干品重量）：需注意，可能带入较多母液杂质
- **湿重 ≥ 干重 × 2.0**（夹带母液 ≥ 100% 干品重量）：高度警惕，杂质剥离效果可能被抵消

若结晶体系浓度较高，湿重大量夹带母液，则原本希望留在母液中的 bulk impurities 会被重新带入滤饼，削弱纯度提升。因此，结晶设计必须从一开始就考虑其与下游过滤的兼容性。

## 8. 非理想结果 (Non-Ideal Outcomes)

成功准则：不限于固体形成，需满足质量与过滤性阈值 (Success Criteria: Adherence to quality and filtrability thresholds)。常见非理想结果包括：
- amorphous precipitation
- oil-out
- mixed salt / mixed polymorph
- excessive fines
- impurity trapping
- mother liquor retention driven purity loss

### 8.1 Oil-out

Oil-out 应作为独立风险模块，其准确描述为：

> **体系未进入稳定的固液析晶路径，而转入了 product-rich liquid-like phase / oil phase formation。**

一旦形成油相，product 会持续溶于该相中，难以进一步稳定转化为晶体，从而使整个结晶失去可控性。

常见相关因素包括：
- 过高的局部过饱和
- 成核启动困难
- 降温过快
- 反溶剂轨迹不合适
- 体系中存在易乳化、易聚集的微量成分
- amorphous precursor 聚集成油状相

因此，oil-out 不是“结晶不好”的普通变体，而是应单独研究原因、单独管理风险的 disaster signal。

### 8.2 无定形沉淀 (Amorphous Precipitation)

无定形沉淀通常意味着过饱和形成过快，规则晶体生长跟不上过饱和释放。其典型问题包括表面积大、易吸附母液和杂质、后续重结晶负担增加。但 amorphous 并非绝对不可接受，若其在体系中溶解度极低、可稳定过滤、可安全转运，有时仍可作为权宜中间状态。

### 8.3 多盐型 / 多固态形式共析

当不同盐型或固态形式的溶解度接近，而过饱和形成又过快时，可能出现 mixed forms co-precipitation。其信号往往很小（含量略高、pH 略偏、离子计量略偏），但本质上已是混合固态形式。

## 9. #Audit: 本章核心影子指标 (Shadow Indicators)

| 指标 | 含义 | 触发阈值 |
|------|------|----------|
| `Crude_solubility_ratio` | 粗品溶解度 / 纯品溶解度 | >2 触发调查 |
| `Residual_modifier_content` | 残留助溶组分含量（如 DMF） | >5% 触发 Soft Block |
| `IR_form_consistency_flag` | 批间固态形式一致性抽查标记 | 收率变化 >5% 时必查 |
| `Salt_stoichiometry_deviation` | 盐型计量偏差 | >3% 提示混合盐型 |
| `Wet_cake_retention_ratio` | 滤饼湿重 / 干重比值 | >1.5 需注意，>2.0 高度警惕 |
| `Crash_risk_flag` | 快速降温 / 加料导致的暴析风险 | 放大前重点复核 |
| `Oil_out_flag` | 是否出现 product-rich liquid-like phase | 一旦出现需单独追因 |

#Audit: 一次结晶的真正价值，不是“先把产物拿出来”，而是在 liquid control 尚未完全消失之前，利用最后的设计窗口，把 bulk impurity 尽量压回母液，并把 product 带入一个可继续处理的 solid inventory。

## 10. Machine Annotation

```yaml
schema_version: "risk_annotation_schema_v0.2"
annotation_scope: "chapter_level"
canonical_id: "ISOL-001-CRYSTALLIZATION"
process_stage: "isolation_crystallization"

transition_model: "solution_phase_control_to_solid_state_commitment"

control_window: >
  Primary crystallization is the last major window in which solution-phase variables can still be used to recover product, reject bulk impurities, and define the first solid inventory before later operations mainly handle consequences.

core_judgment: >
  The main machine-review task is to detect whether the crystallization design has addressed solubility gap, residual solubilizing modifiers, supersaturation generation, nucleation robustness, solid-form risk, and filtration compatibility before the system crosses into solid-state commitment.

risk_signals:
  - "crude_solubility_ratio > 2"
  - "residual_modifier_content > 5%"
  - "rapid supersaturation buildup"
  - "local supersaturation near antisolvent, acid, or base addition point"
  - "delayed or failed nucleation after seeding"
  - "yield shift > 5% across batches"
  - "wet_cake_retention_ratio > 1.5"
  - "wet_cake_retention_ratio > 2.0"
  - "oil_out_flag observed"
  - "salt_stoichiometry_deviation > 3%"
  - "mixed solid form or mixed salt form suspected"

expert_judgment:
  - "If crude solubility is significantly higher than pure-product solubility, crystallization failure is likely driven by residual solubilizing modifiers rather than by the intrinsic solvent system."
  - "If supersaturation is generated faster than it can be consumed through controlled nucleation and growth, the process is at risk of crash crystallization, amorphous precipitation, oil-out, or mixed solid-form precipitation."
  - "If nucleation depends on small-scale behavior and seeding is not robust, crystallization may fail to scale even when small-scale recovery appears acceptable."
  - "If wet cake retention is high, first-pass impurity rejection may be negated by mother liquor carryover."
  - "If solid-form consistency drifts across batches, yield and purity variation should be treated as a solid-state control issue rather than only as a solvent or recovery issue."

reasoning_anchors:
  - "control_authority_decay"
  - "solid_state_commitment"
  - "usable_solubility_gap"
  - "residual_modifier_effect"
  - "supersaturation_control_window"
  - "local_supersaturation"
  - "nucleation_scale_sensitivity"
  - "solid_form_drift"
  - "mother_liquor_retention"
  - "downstream_filtration_compatibility"

quantitative_triggers:
  crude_solubility_ratio: ">2"
  residual_modifier_content: ">5%"
  wet_cake_retention_ratio_warning: ">1.5"
  wet_cake_retention_ratio_high_risk: ">2.0"
  yield_shift_solid_form_check: ">5%"
  salt_stoichiometry_deviation: ">3%"

uncertainty: "medium"

exceptions:
  - "Amorphous or imperfect solids may be acceptable if they are stable, filterable, transferable, and intended only as an intermediate isolation form."
  - "High impurity content does not automatically invalidate crystallization if impurities are designed to remain in the mother liquor and wet cake retention is low."
  - "Oil-out and mixed solid forms require case-specific investigation and should not be treated as ordinary crystallization variation."
  - "Thresholds are empirical screening triggers, not universal pass/fail specifications."

machine_use: >
  Use this annotation to review whether a proposed primary crystallization design has addressed solubility gap, residual modifiers, supersaturation generation rate, nucleation robustness, solid-form risk, and filtration interface before the system crosses from solution-phase control into solid-state commitment.
