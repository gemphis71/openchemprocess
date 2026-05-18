---
snapshot_id: "WRKUP-003-SOLVENT-REMOVAL-DRIVEN-ACCUMULATION-AND-THERMAL-EXPOSURE-CONTROL"
status: "draft"
domain: "Process"
process: "Workup"
topic: "溶剂移除驱动的富集与热暴露控制（Hard Gate + Route Priority）"
level: "001"
language: zh  
canonical_id: WRKUP-003-SOLVENT-REMOVAL-DRIVEN-ACCUMULATION-AND-THERMAL-EXPOSURE-CONTROL
dependencies:
  - "WRKUP-001-WORKUP-CONTROL-AUTHORITY"
  - "WRKUP-002-PARTITION-RATIO-DRIFT-INVENTORY-CONTROL"
  - "THR-001-THERMAL-CONTROL-AUTHORITY"
---


# WRKUP-003｜溶剂移除驱动的富集与热暴露控制

## 1 设计意图与审查目标

浓缩与溶剂置换是液相操作中最后一个仍处于“液相世界”的步骤。本章的控制权目标不是“如何蒸掉溶剂”，而是管理一个不可逆的推进过程：通过移除挥发性组分，迫使体系组成沿特定轨迹前进，并触发非挥发物富集、相行为重写、热暴露累积与设备边界暴露。

浓缩是高风险的强不友好动作。危险源自同一类根因：

> 高浓度 + 热暴露累积 + 非挥发物（盐/酸碱/高沸残留）富集 + 相/物种被重写

本章工程目标：

- 缩短浓缩时间（降低热暴露）
- 降低浓缩过程中杂质/环境对产物的影响
- 通过上游选择消灭“必须大幅浓缩”的结构性风险

核心审查原则：

> 优先减少或绕开“萃取→浓缩”的高风险不可逆路径；若不可避免，则通过降低浓缩倍数与提前溶剂置换，控制热暴露与富集路径，避免末段高浓度灾难窗口。

上游耦合要求：

WRKUP-003 的 machine review 必须包含萃取溶剂选择的审查，必要时包含前一步反应溶剂选择的审查。后处理安全边界反向约束前序溶剂选择。

---

## 2 审计字段（Review Fields & Accounting Basis）

本章所有审查与阻断均基于以下核心审计字段。机器在审查方案时必须检查字段是否填写、口径是否合理、最小子项是否齐全。

### 2.1 核心指标

#### CF（Concentration Factor）

**定义：**

CF = 初始液相体积 / 终点液相体积

**用途：**

CF 是多个风险模式的公共依赖指标（非挥发物富集、热暴露、酸碱富集等）。

> 注：本章中出现的 CF 阈值（如 >3、>5、>10）均为经验初设阈值（Tunable）。  
> 实际项目中需根据产品特性、公司标准、风险承受度调整。

### 2.2 核心字段列表（含最小可检查子项）

| 字段（首次出现即固定缩写） | 定义/口径 | 必填条件 | 最小可检查子项（缺失即触发） | 审查要点 |
|---|---|---|---|---|
| 挥发组分移除路径（VRT） | 明确哪些组分优先挥发；是否存在共沸带水；是否存在目标或关键杂质的共蒸风险 | 混合溶剂或含水体系必须填 | (1) **挥发顺序**（至少声明主要低沸组分先后） (2) **共沸/共蒸声明**（有/无/未知 + 一句依据） | 是否识别全部挥发性组分？是否声明共沸/共蒸风险？ |
| 非挥发物库存（NV） | 列出会在浓缩中富集的非挥发物：盐、酸碱、高沸残留、催化剂、聚合物、关键杂质前体等 | 任何含非挥发组分体系必须填 | (1) **NV 清单**（至少覆盖盐/酸碱/高沸残留三类中的适用项） (2) **富集/析出风险声明**（有/无/未知 + 一句依据） | 清单是否完整？是否估算初始量或浓度？ |
| 组成演化轨迹（CEP） | 混合溶剂比例随时间/体积变化路径；关键互溶组分（水/共溶剂）比例变化 | 混合溶剂体系必须填 | (1) **比例漂移描述**（低沸先走导致比例如何变化） (2) **不稳定区提示**（析盐/析油/相反转/结晶窗口：有/无/未知） (3) **形态变化关键点**（若观察到：给出体积/时间/温度点；未知则标注未知） | 是否记录形态变化点（体积/时间/温度）？是否与 WRKUP-002 的相行为/分配风险衔接？ |
| 热暴露（TE） | 允许温度上限、最大加热时间窗口、末段高浓度持续时间；是否完成热破坏实验 | 任何加热浓缩必须填 | (1) **Tmax** (2) **加热时间窗口** (3) **热破坏实验声明**（有/无/覆盖范围一句话；且包含杂质谱观察与否） | 热破坏实验是否覆盖放大条件（温度×时间×浓度轨迹）？ |
| 可操作边界（OC） | 最小可搅拌体积、是否允许全干、目标湿品含溶剂量、出料路径、固体残渣转移方案 | 放大步骤必须填 | (1) **最小可搅拌体积** (2) **是否允许全干**（是/否） (3) **出料/转移方案**（底拔/转釜/离心/返溶等之一） (4) **湿品残溶目标与影响依据**（若得湿品：残溶目标 + “对收率/下一步影响依据”一句话；不适用则NA） | 是否核算最小可搅拌体积？湿品残溶是否有影响依据（收率/杂质/下一步）？ |

---

## 3 风险模式与阻断规则

> 统一约定：阻断等级仅使用 **Soft-block / Hard-block**。  
> “未评估/未声明”一律以“最小可检查子项缺失或为空”来判定。

### 3.1 非挥发物富集模式

#### 机制描述

盐、酸碱、高沸残留、催化剂、杂质前体等在溶剂移除过程中被浓缩。  
浓度倍数 ≈ CF。

富集后可能触发：

- 盐析出
- 酸碱度跃迁导致产物或杂质降解
- 黏度异常
- 杂质或产物二次反应

#### 控制策略

- 优先通过上游水洗降低 NV 负载
- 必要时通过**溶剂**置换使产品提前析出并分离

#### 触发条件（Tunable 阈值，子项缺失可检查）

| 条件 | 阻断等级 | 依赖字段 |
|---|---|---|
| 存在 NV 负载，且 CF > 3，但 **NV.富集/析出风险声明** 缺失/为空 | Soft-block | CF；NV |
| 产物对酸碱敏感，存在酸碱负载，CF > 5 且计划长时间加热至全干燥 | Hard-block | CF；NV（酸碱负载）；TE；OC（是否全干） |

> CF 阈值为经验初设，可调整。

---

### 3.2 组成轨迹跨越不稳定区模式

#### 机制描述

混合溶剂浓缩时，低沸组分优先挥发，比例沿特定路径漂移。  
若路径穿越不稳定区（析盐、析油、相反转、结晶窗口），体系可能发生突发相变或物种重写。

补充案例（已归类）：

- 浓缩过程中大量固体析出  
- 浓缩初期因蒸发过快导致内温下降，大量固体析出  

主归类：组成轨迹跨越不稳定区  
次归类：设备与转移边界

#### 控制策略

1. 在实验中观察并识别不稳定区域  
2. 采用低沸溶剂萃取 + 较高沸溶剂置换的在线置换主动规划路径  

#### 触发条件（字段/子项缺失型）

| 条件 | 阻断等级 | 依赖字段 |
|---|---|---|
| 混合溶剂体系 **未填写 CEP** 或 CEP.比例漂移描述 缺失/为空 | Soft-block | CEP |
| VRT 中 **挥发顺序** 或 **共沸/共蒸声明** 缺失任一 | Soft-block | VRT |

---

### 3.3 热暴露累积模式

#### 机制描述

放大浓缩通常：

- 温度提高（+10–20°C）
- 时间延长（×3–5）
- 末段浓度升高

可能导致：

- 产物热降解
- 杂质升高
- 杂质或产物二次反应

#### 控制策略

- 小试阶段完成热破坏实验（覆盖放大条件）
- 通过路线1或路线2降低浓缩倍数
- 通过提前溶剂置换减少末段高浓度暴露

#### 触发条件

| 条件 | 阻断等级 | 依赖字段 |
|---|---|---|
| TE.热破坏实验声明 缺失/为空 | Soft-block | TE |
| 热破坏实验未覆盖放大条件（温度×时间×浓度轨迹） | Soft-block | TE；CF |
| 实验显示不稳定仍按原条件放大 | Hard-block | TE（实验结论） |

---

### 3.4 设备与转移边界模式

#### 机制描述

小试可全干燥并原瓶继续操作；  
放大受限于：

- 最小可搅拌体积
- 出料路径
- 固体残渣转移
- 湿品含溶剂对下一步影响

#### 控制策略

- 核算最小可搅拌体积
- 采用“不完全浓缩 + 放料 + 离心”
- 或提前溶剂置换促析

#### 触发条件

| 条件 | 阻断等级 | 依赖字段 |
|---|---|---|
| 未填写 OC 或 OC 任一最小子项缺失/为空 | Soft-block | OC |
| 预计体积 < OC.最小可搅拌体积 且 OC.是否允许全干=是（仍计划全干燥） | Hard-block | OC.最小可搅拌体积；终点体积（计算）；OC.是否允许全干 |
| 残渣为固体但无出料/转移方案 | Hard-block | OC.出料/转移方案 |
| 计划得湿品但 OC.湿品残溶目标与影响依据 缺失/为空 | Soft-block | OC.湿品残溶目标与影响依据 |

---

### 3.5 跨模式硬门：爆炸性评估

任何浓缩步骤前必须完成爆炸性评估。

| 条件 | 阻断等级 | 依赖字段 |
|---|---|---|
| 未提供爆炸性评估报告 | Hard-block | 外部安全评估结论 |

---

## 4 三条设计路线（优先级顺序）

机器审查顺序：

> 路线1 > 路线2 > 路线3

### 路线1（最优）：产品先脱离体系

- 是否评估产品可提前脱离反应体系？
- 是否存在可转移路径？

未评估 → Soft-block

### 路线2：减少浓缩倍数

- 萃取溶剂 ≤ 2–3 倍（经验值）
- CF ≤ 5（经验值）
- CF > 10 → Hard-block

> 注：**CF>10 原则上 Hard-block**。  
> 仅当提供“无法降低 CF 的强制性理由”并形成独立评审留痕（#Audit 引用）时，允许以“Hard-block-with-override（可审计豁免）”放行。

### 路线3：浓缩 + 置换

- 不全干燥
- 提前加入下一步溶剂
- 若需分离产品，选择难溶置换溶剂促析

存在高风险特征但未采用提前置换 → Soft-block

---

## 5 审计留痕

```text
#Audit: WRKUP-003
- CF:
- NV完整:
- VRT子项完整(挥发顺序/共沸共蒸):
- CEP子项完整(比例漂移/不稳定区/形态点):
- TE子项完整(Tmax/时间/热破坏声明):
- OC子项完整(最小搅拌体积/全干/转移/湿品残溶依据):
- 采用路线:
- Hard-block触发:
- Soft-block触发:
- Override(如有):
```

## 6 Vocabulary Evolution

|概念|定义|
|---|---|
|浓缩控制权|通过移除挥发组分迫使体系沿不可逆路径前进|
|非挥发物富集|NV 随溶剂移除而倍增|
|组成演化轨迹（CEP）|混合溶剂比例随时间/体积变化的路径描述|
|热暴露（TE）|温度×时间×浓度轨迹|
|最小可搅拌体积|放大设备搅拌失效临界体积|
|三路线|本章定义的降风险设计优先级|

---

## Appendix A — Representative Structured Cases (Machine-Readable)
 
> **CaseID / Scene / Mode / Fields / Trigger / Outcome / Block / Audit**

### CaseID: W3-01

- Scene: EtOAc/乙酸乙酯萃取后有机相含水；上游水相可能含盐（盐水/无机盐）
    
- Mode: NV富集（盐） + 组成轨迹跨越不稳定区（脱水后盐显形）
    
- Fields: CF; VRT(共沸带水); NV(盐负载); CEP(脱水路径)
    
- Trigger: 有盐负载且计划共沸脱水/浓缩；NV.富集/析出风险声明缺失/为空
    
- Outcome: 共沸带走水后盐析出；造成后续操作异常/损失
    
- Block: 先水洗去盐（在可承受损失前提下）→再共沸脱水；避免干燥剂+过滤作为放大依赖
    
- Audit: NV是否列盐？VRT是否包含挥发顺序/共沸声明？是否给出水洗可行性依据？
    

### CaseID: W3-02

- Scene: 小试旋蒸≈30min；放大釜内真空保守+蒸发面积小→2–4h且T更高
    
- Mode: 热暴露累积
    
- Fields: TE(Tmax/时间窗口/热破坏声明); CF
    
- Trigger: TE.热破坏实验声明缺失/为空，或未覆盖放大条件
    
- Outcome: 产物热降解/杂质谱劣化/新杂质生成；去除策略与小试不一致
    
- Block: 热破坏实验覆盖“温度×时间×浓度轨迹”并记录杂质谱；优先降低CF或提前置换稀释末段
    
- Audit: TE子项是否完整？覆盖范围是否匹配放大预期？
    

### CaseID: W3-03

- Scene: 放大浓缩终点体积可能低于搅拌可维持下限；小试可全干燥
    
- Mode: 设备与转移边界
    
- Fields: OC(最小可搅拌体积/是否允许全干/终点体积计算); CF
    
- Trigger: 终点体积 < OC.最小可搅拌体积且仍计划全干燥
    
- Outcome: 搅拌失效→挂壁/局部异常/残留带入下一步
    
- Block: 分段浓缩/转更小釜/接受不完全浓缩并评估影响；避免把“全干燥”作为硬目标
    
- Audit: 终点体积计算是否给出？OC子项是否齐全？
    

### CaseID: W3-04

- Scene: 放大需釜底出料/转釜；residue为固体或高黏油状，转移成为约束
    
- Mode: 设备与转移边界
    
- Fields: OC(出料路径/固体转移方案/湿品目标); CEP(浆化/溶剂选择)
    
- Trigger: residue为固体但OC.出料/转移方案缺失/为空
    
- Outcome: 难放料/难转移，被迫返溶→流程回退、时间拉长、热暴露加重
    
- Block: 不完全浓缩+放料+离心/过滤；或提前溶剂置换促析并保证可浆化可转移
    
- Audit: 是否给出“固体如何出料/浆化口径/转釜方式”？
    

### CaseID: W3-05

- Scene: 为出料/离心保留少量残溶（不完全浓缩）；但产物对残溶溶解度较大
    
- Mode: 组成轨迹（溶解度窗口） + 设备边界
    
- Fields: CEP(残溶路径); OC(湿品残溶目标与影响依据); CF
    
- Trigger: 计划得湿品但OC.湿品残溶目标与影响依据缺失/为空
    
- Outcome: 母液溶解损失高；析出时机不对导致夹杂/油化
    
- Block: 用数据定义允许残溶范围；必要时溶剂置换到难溶溶剂促析并离心收集
    
- Audit: 是否有残溶-收率依据？置换溶剂选择依据是否写明？
    

### CaseID: W3-06

- Scene: 反应溶剂+萃取溶剂混合体系；放大时低沸溶剂先走且浓缩时间更长，小试油状→放大变固体
    
- Mode: 组成轨迹跨越不稳定区
    
- Fields: VRT(挥发顺序/共沸声明); CEP(不稳定区/形态点); TE(时间拉长)
    
- Trigger: CEP.形态变化关键点缺失/为空（或标注未知但无最小观察记录）
    
- Outcome: 油→固突变影响搅拌/传热；也可能是浓缩诱导结晶机会点
    
- Block: 小试记录形态窗口（体积/时间/温度）；可将浓缩与结晶耦合，避免“全干燥后返溶重结晶”
    
- Audit: 是否记录固体出现窗口点？是否解释耦合/不耦合决策？
    

### CaseID: W3-07

- Scene: 萃取溶剂与下一步反应溶剂不一致；希望不出料直接进入下一步
    
- Mode: 组成轨迹（主动规划） + 热暴露控制
    
- Fields: VRT(低沸溶剂先走); CEP(在线置换路径); CF; TE
    
- Trigger: CF偏高或热敏风险显著，但未采用提前溶剂置换保持稀释
    
- Outcome: 末段高浓度+加热导致降解/杂质放大；且可能受设备边界限制难全干燥
    
- Block: 浓缩到一定程度加入反应溶剂继续浓缩，带走残留的萃取溶剂；保持体系较稀降低末段暴露
    
- Audit: 是否明确置换加入时点（体积/温度）？是否说明与下一步溶剂兼容？
    

### CaseID: W3-08

- Scene: 反应溶剂为DCM（下层）；为实现后续萃取相行为，需先浓缩/置换到低密度溶剂
    
- Mode: 组成轨迹（为相行为服务）
    
- Fields: VRT(去除DCM程度); CEP(置换路径); OC(分相/出料可行性)
    
- Trigger: 需要低密度萃取但未设计“DCM→低密度溶剂”的置换路径（CEP缺失/为空）
    
- Outcome: 分相不友好/操作冲突；WRKUP-002的相间分配难稳定
    
- Block: 淬灭后先去除部分DCM，再置换到低密度萃取溶剂后萃取/洗涤
    
- Audit: 是否声明置换前后相位/密度预期？是否评估溶解损失？
    

### CaseID: W3-09

- Scene: THF/醇/DMF/DMSO等与水互溶或高水溶性，导致液液萃取不友好
    
- Mode: 组成轨迹（互溶窗口管理）
    
- Fields: CEP(互溶性路径); VRT(预浓缩去除量); CF
    
- Trigger: 计划萃取但未给出“预浓缩/置换到萃取友好溶剂”的方案（CEP/VRT子项缺失）
    
- Outcome: 难分相/分配失控；WRKUP-002的Kd逻辑无法稳定应用
    
- Block: 先预浓缩去除互溶溶剂的一部分，再置换为萃取友好溶剂后进行水洗/萃取
    
- Audit: 是否明确预浓缩程度？置换后相行为预期是否记录？
    

### CaseID: W3-10

- Scene: 小试常全干燥；放大终点往往为湿品（残溶较高），直接进入结晶/下一步反应会产生差异
    
- Mode: 设备边界 + 组成轨迹（残溶改变体系）
    
- Fields: OC(湿品残溶目标与影响依据); CEP(残溶影响下一步); CF
    
- Trigger: 计划得湿品但OC.湿品残溶目标与影响依据缺失/为空
    
- Outcome: 结晶/反应表现与小试显著不同；若强行烘干则效率大幅下降
    
- Block: 小试按放大现实定义湿品状态；用溶剂置换对齐下一步溶剂需求，减少对烘干依赖
    
- Audit: 湿品残溶目标与测定方法是否写明？影响依据是否存在？
    

### CaseID: W3-11

 - **Scene**: 前序操作使用酸/碱洗涤，残留酸/碱负载随浓缩富集（CF 倍数放大）；产物对酸/碱敏感
    
- **Mode**: NV富集（酸碱）
    
- **Fields**: NV（酸碱负载清单与初始浓度）；CF；TE（若加热）；OC（是否全干）
    
- **Trigger**:
  
 - 场景A（水洗可行）：存在酸碱负载，CF > 3，但未评估析出/富集风险 → Soft-block
      
  - 场景B（水洗不可行）：酸碱敏感 + 酸碱负载存在 + 计划高CF（>5）末段加热，但未设计提前置换规避 → Soft-block
     
  - 场景C（最严重）：酸碱敏感 + 酸碱负载 + CF > 5 + 计划加热至全干 → Hard-block
     
- **Outcome**: 末段酸/碱浓度跃迁导致产物降解、副反应或杂质谱劣化
    
- **Block**:
 
  - 优先通过水洗降低酸碱负载
      
  - 若水洗不可行，采用提前溶剂置换保持稀释，缩短末段高浓度暴露
      
 - 避免高CF（>5）与长时间加热至干组合
     
- **Audit**: 是否声明酸碱负载来源与初始浓度？是否评估水洗可行性？若不可行，是否设计提前置换方案？是否约束CF×加热组合？
    

### CaseID: W3-12

- Scene: 任意需要加热/减压浓缩或可能富集不稳定物的体系
    
- Mode: 安全硬门（Safety Gate）
    
- Fields: 外部安全评估结论（爆炸性/热危害/分解风险）
    
- Trigger: 未提供爆炸性评估/安全评估结论
    
- Outcome: 末段富集与加热/减压可能触发爆炸性风险（来源可为产物/副产物/杂质）
    
- Block: 未提供评估结论→Hard-block；先完成安全评估再谈工艺优化
    
- Audit: 是否引用评估结论编号/日期？是否覆盖“浓缩末段高浓度条件”？
    

### CaseID: W3-13

- Scene: 浓缩被判断为高风险/强不友好（高CF/热敏/杂质多等），应优先评估“产品先脱离体系”（路线1）
    
- Mode: 路线优先级（Route 1）
    
- Fields: 路线1评估要点（产品主要去向/可转移路径/对收率纯度安全影响）
    
- Trigger: 未评估路线1即直接进入萃取→浓缩路径
    
- Outcome: 容易被迫进入高CF+高热暴露末段窗口；浓缩风险留在产品体系中
    
- Block: 机器审查要求先完成路线1最小评估；若可行，优先采用产品先脱离策略
    
- Audit: 若不可行，是否给出证据链（而非习惯性选择萃取浓缩）？

### CaseID: W3-14
    
- Scene: 使用醚类溶剂（THF, 2-MeTHF, Diisopropyl ether）且计划浓缩倍数较高。
    
- Mode: 安全硬门 (Safety Gate) + NV 富集（过氧化物）。
    
- Fields: NV（过氧化物检测值）；CF；OC（是否全干）。
    
- Trigger: 计划全干燥且使用易产生过氧化物溶剂，但未提供过氧化物定量检测记录。
    
- Outcome: 浓缩末段过氧化物浓度超过安全限值，引发热失控或爆炸。
    
- Block: 强制要求在 CF > 5 前进行过氧化物检测；严禁此类体系浓缩至全干。
    
- Audit: 是否附带过氧化物检测试纸照片或分析报告？
---

## 7. Machine Annotation

```yaml
schema_version: "risk_annotation_schema_v0.2"
annotation_scope: "chapter_level"
canonical_id: "WRKUP-003-SOLVENT-REMOVAL-DRIVEN-ACCUMULATION-AND-THERMAL-EXPOSURE-CONTROL"
process_stage: "workup_concentration_solvent_exchange"

transition_model: "liquid_phase_workup_to_forced_composition_path_under_solvent_removal"

control_window: >
  Concentration and solvent exchange still occur in the liquid-phase domain, but solvent removal forces the system along an increasingly constrained composition path. Control authority is mainly exercised by avoiding concentration, reducing CF, selecting the extraction or reaction solvent appropriately, and introducing early solvent exchange before late-stage high-concentration risk windows form.

core_judgment: >
  The central machine-review task is to detect whether a proposed workup treats concentration as neutral solvent evaporation instead of an irreversible accumulation trajectory that may amplify nonvolatile inventory, thermal exposure, phase-behavior drift, and equipment or transfer-boundary constraints.

review_gates:
  hard_gate:
    - "CF > 10 without explicit audit override"
    - "acid/base sensitive system + CF > 5 + heating to complete dryness"
    - "known thermal or concentration instability ignored"
    - "final volume below minimum stirrable volume while dryness is planned"
    - "solid residue expected without transfer plan"
    - "no explosion hazard assessment before concentration"
  soft_gate:
    - "NV exists and CF > 3 but NV accumulation risk is not declared"
    - "CEP missing for a mixed-solvent system"
    - "VRT volatility order missing"
    - "TE degradation study missing for heated concentration"
    - "thermal study does not cover scale-up temperature, time, or concentration conditions"
    - "OC missing for scale-up concentration"

route_priority:
  - "Route 1: product disengagement before concentration"
  - "Route 2: concentration reduction, preferably CF <= 5"
  - "Route 3: concentration plus early solvent exchange, avoiding complete dryness when possible"

risk_signals:
  - "CF > 3 with nonvolatile inventory present and undeclared"
  - "CF > 5 in acid/base sensitive system with heating to complete dryness"
  - "CF > 10 without explicit override"
  - "nonvolatile salts, acids, bases, high-boiling residues, or modifiers remain during concentration"
  - "mixed-solvent system without VRT volatility order"
  - "mixed-solvent system without CEP composition-drift assessment"
  - "lower-boiling solvent removal may cross instability zone"
  - "oiling out during concentration"
  - "salt-out during concentration"
  - "unexpected crystallization during concentration"
  - "phase inversion during concentration"
  - "heated concentration without scale-relevant degradation study"
  - "thermal study does not cover higher temperature, longer duration, and higher concentration expected on scale-up"
  - "planned complete dryness"
  - "final volume below minimum stirrable volume"
  - "solid residue without transfer plan"
  - "wet-product solvent target not defined"
  - "explosion hazard assessment missing before concentration"

reasoning_anchors:
  - "control_authority_decay"
  - "misallocated_control_authority"
  - "forced_composition_path"
  - "nonvolatile_accumulation"
  - "composition_evolution_path"
  - "volatile_removal_trajectory"
  - "thermal_exposure_accumulation"
  - "early_solvent_exchange"
  - "equipment_transfer_boundary"
  - "upstream_solvent_selection_coupling"
  - "route_priority_review"

expert_judgment:
  - "Solvent removal should be reviewed as a forced composition trajectory, not as a neutral housekeeping operation."
  - "If nonvolatile inventory remains during concentration, its effective local level may scale approximately with CF and may create precipitation, acid/base shift, viscosity increase, or secondary reaction risk."
  - "If lower-boiling components leave first, solvent ratio drift may rewrite phase behavior even when the initial mixture appears acceptable."
  - "If thermal exposure data do not cover scale-up Tmax, duration, and concentration, small-scale stability evidence should not be treated as sufficient."
  - "If complete dryness is planned, review must distinguish laboratory convenience from scale-up feasibility, especially minimum stirrable volume, discharge path, and solid transfer."
  - "If concentration risk is high, the preferred review direction is upstream redesign, product disengagement, or CF reduction before accepting concentration plus solvent exchange."

uncertainty_and_exceptions:
  - "CF thresholds are initial engineering guidelines and may be tuned by product properties, company standards, and acceptable risk tolerance."
  - "Missing fields trigger review rather than automatic process rejection unless a defined hard-gate condition is met."
  - "Early precipitation during solvent exchange may be beneficial if intentionally designed, experimentally understood, and compatible with downstream handling."
  - "CF > 10 may be overridden only with explicit audit trace and a justified risk-control basis."
  - "The annotation should not infer degradation, oiling out, or phase inversion unless supported by observed data, known instability, or missing required review fields."

quantitative_triggers:
  cf_nv_soft_review: "NV exists and CF > 3 with undeclared accumulation risk"
  cf_acid_base_dryness_hard_block: "acid/base sensitive system + CF > 5 + heating to complete dryness"
  cf_hard_block: "CF > 10 unless explicit audit override"
  preferred_cf_target: "CF <= 5"
  thermal_study_required_when: "heated concentration"
  explosion_assessment_required_when: "before concentration"

required_review_fields:
  - "CF"
  - "VRT"
  - "NV"
  - "CEP"
  - "TE"
  - "OC"
  - "explosion_hazard_assessment"
  - "selected_route"
  - "override_trace_if_any"

machine_use: >
  Review whether a proposed concentration or solvent-exchange design has avoided unnecessary concentration, justified CF, declared nonvolatile inventory, mapped volatile-removal and composition-evolution trajectories, covered scale-relevant thermal exposure, and checked equipment or transfer-boundary constraints before accepting the workup route.