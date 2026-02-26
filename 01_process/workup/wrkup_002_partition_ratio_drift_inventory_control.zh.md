---
snapshot_id: "WRKUP-002-PARTITION-RATIO-DRIFT-INVENTORY-CONTROL"
status: "draft"
domain: "Process"
process: "Workup"
topic: "萃取分配比漂移：相环境漂移 / 物种漂移 / 工业路径风险标签（Soft Gate）"
level: "001"
dependencies:
  - "WRKUP-001-WORKUP-CONTROL-AUTHORITY"
  - "MIX-001-MIXING-TIME-SCALE-FAILURE"
  - "THR-001-THERMAL-CONTROL-AUTHORITY"
note:
  - "面向 machine-review：以 1→2 次洗涤/萃取的 Δkd 为早期信号，触发追因与软阻断，抑制库存损失与返工放大。"
---

# wrkup-002｜phase redistribution & inventory control

## partition ratio drift (kd drift) as soft gate

## 1. 定位（positioning）

本章将萃取/洗涤定义为库存再分配（inventory redistribution），关注三类库存：

- target inventory：目标物留在哪一相
- waste inventory：水溶性/活性杂质是否被稳定丢弃
- carryover inventory：盐/金属/络合态/共溶剂/含水是否被带入下一步

本章为 soft gate：不当场否决，但对高损失/高返工路径触发追因与阻断提示。

输出等级：
- flag：必须补充证据/追因后再推进或放大复制
- soft block：未完成追因则禁止按原方案继续扩展/复制

## 2. 基本判据（foundational criteria）

### 2.1 分配比定义与一致性判据（kd consistency）

**定义（总量口径）**  
kd = 有机相中目标物总量 / 水相中目标物总量

采用“浓度 × 质量（称重）”计算（不使用体积）：
- kd = (c_org × m_org) / (c_aq × m_aq)

其中：
- m_org, m_aq：两相质量（称重）
- c_org, c_aq：两相浓度（单位自洽即可）

**一致性检查（只盯 1→2）**
- Δkd(1→2) = |kd_2 − kd_1| / kd_1
- 若 Δkd(1→2) > 15%：触发 soft block（必须完成追因后方可继续按原方案扩展洗涤）

阈值为工程初值：可版本化修订，或按产品价值/容错包络分级。

### 2.2 相环境漂移判据（phase-environment drift）

相环境指每次洗涤当下两相的实际环境组成（离子强度、共溶剂、含水、温度、界面状态等）。相环境改变即默认 kd 不等价。

**主要漂移来源（按可审查要素列举）**

1) 纯水被“加载”为盐水窗口（loading drift）
- wash#1 名义为纯水/酸水/碱水，但接触体系后形成高离子强度水相：
  - loading-1：体系自带盐/金属盐/离子型副产物溶入水相
  - loading-2：酸水/碱水中和生成盐（中和盐水相）
- wash#2 通常回到真纯水（低离子强度）→ 1→2 水相环境显著不同 → kd 漂移风险上升

2) 共溶/互溶溶剂残留与“组分加载漂移”（mutual solubility & loading drift）
- THF、MeCN、IPA 等与水互溶/部分互溶
- 回收/套用溶剂导致共溶剂与含水累积 → 有机相极性上升 → 携盐能力与 kd 改变
- 新鲜溶剂的 kd 不等价于回收溶剂的 kd

3) 有机相带水（hidden water content）
- 有机相自带数 % 水 → 极性与携盐能力改变 → kd 与带盐风险漂移
- 该问题属于相环境因素，不等价于“干燥不足”

4) 温度窗口切换（temperature window shift）
- 热洗/冷洗切换改变溶解度与分配窗口 → kd(T) 不可外推

5) 界面层/第三相（rag layer）
- 放大静置/分相时间延长、微量固体/金属盐/副产物在界面累积形成 rag layer
- 出现 rag layer 时系统从“两相分配”转为“三相库存再分配”，界面层可成为独立库存通道
- 开发早期应主动暴露 rag layer 风险（延长静置/重复洗涤/切换盐强度与温度窗口），以确认其可见性与可重复性

乳化（emulsion）与 rag layer 作为界面现象，统一按 rule w2-3 执行记录与审计。

### 2.3 物种漂移判据（species drift）

物种漂移指目标物/关键组分在不同洗次以不同化学形态参与分配，导致 kd 非等价，典型包括：
- 游离态 vs 盐态（酸/碱产物在 pH 变化下部分成盐）
- 络合态/离子对 vs 非络合态

常规 TLC/HPLC 通常难以区分络合物/有机盐/离子对，因此物种漂移易被误归因为相环境漂移。

## 3. 失效模式（failure modes）

### Ⅰ｜kd 漂移未阻断（kd drift unchecked）
- 触发条件：Δkd(1→2) > 15% 但未追因，仍按“次数”推进
- 风险结果：target loss、乳化/分相失败、返工与下游负担放大

### Ⅱ｜物种漂移被漏判（species drift missed）
- 误判路径：将物种差异解释为“水相更咸/更稀/溶剂带水/温度不同”等相环境因素
- 控制要求：触发漂移后优先进行物种一致性校验（rule w2-2），再进入相环境追因

### Ⅲ｜工业不友好路径标签（industrial-unfriendly workflow tag）
- 指溶剂/工作流在放大中引入系统性不友好因素（VOCs、三废、转移损失、带水堵塞等）
- 作为路径级 risk tag 输出，不与 kd 漂移机理混写

## 4. 代表性案例（case headers + 判定要点/控制结论）

### case 1｜high-ionic-strength window → desalting window：窗口切换导致 kd(1→2) 漂移（phase-environment drift）

**case header**
- system：目标对离子强度敏感；体系含盐/金属盐/离子型副产物；可能乳化
- plan：先进入高离子强度窗口以完成“锁定/转移”，再进入低离子强度窗口（纯水）执行去盐
- key drift：高→低离子强度窗口切换 + wash#1 水相被加载成“非纯水” → kd(1→2) 可能显著漂移

**subtype 1a｜lock-in**
- intent：在高离子强度窗口锁住目标留有机相，同时将水溶性副产物迁移至水相（代价：有机相含盐）
- risk：转入去盐窗口后，若两窗口 kd 不等价，目标进入水相/乳化/损失放大

**subtype 1b｜transfer-out / salt-out**
- intent：降低目标在水相的有效溶解度或改变分配，驱动其从水相转移至有机相，提高首次转移效率
- risk：转入去盐窗口后同样可能触发 kd(1→2) 漂移与损失

**判定要点**
- wash#1 的“高离子强度窗口”来源必须明确（loading-1 / loading-2 / addition）。
- 该类流程的目标通常合理；风险点在于：窗口切换前未验证两窗口 kd 的等价性。

**控制结论**
- Δkd(1→2) > 15%：必须解释“wash#1 窗口形成机制 + wash#2 是否切换到真纯水窗口”，否则 soft block。

#audit：窗口切换不是错误；未验证窗口下 kd 等价性才是错误。

### case 2｜互溶/互相加载导致的 kd 漂移（mutual solubility & loading drift；phase-environment drift）

**case header**
- system：有机溶剂与水存在互溶/部分互溶（water↔org 双向渗入）
- plan：wash#1 后两相组成发生改变；wash#2 在“已改变组成的有机相/水相”上继续洗涤
- key drift：洗次之间相组成（含水量、共溶剂比例、极性）变化 → kd(1→2) 不可假设等价

**判定要点**
- wash#1 同时发生：
  - water → organic：有机相含水上升、极性改变
  - organic → aqueous：水相带入有机溶剂/共溶剂，改变水相性质
- wash#2 发生在“被 wash#1 重新配方后的两相”上，因此 kd(1→2) 可能显著偏离。

**控制结论**
- 互溶体系中应将 kd(1→2) 视为必须核对对象；触发 Δkd(1→2) > 15% 时按 rule w2-1 进入 soft block 与追因。

#audit：互溶体系中，洗涤改变相组成本身；重复洗涤不等价于重复同一环境。

### case 3｜rag layer（third phase）作为“未审计库存通道”（phase-environment drift: physical manifestation）

**case header**
- system：放大静置/分相时间延长，微量固体/金属盐/副产物在界面累积形成 rag layer（絮状层/第三相）
- plan：分相过程中出现稳定界面层，导致分相困难并可能夹带目标物流向废液
- key drift：两相模型失效 → 三相库存再分配；rag layer 成为独立库存通道

**判定要点**
- rag layer 视作第三相；此时 kd 仅覆盖两相，不描述界面库存去向。
- rag layer 的消除策略高度经验性；本章仅要求其库存风险被显式审计。

**控制结论**
- 出现 rag layer 时：
  - 必须记录：发生洗次、静置时间、温度、盐/酸碱条件（作为追因输入）
  - 必须评估：rag layer 中目标物含量（粗定量亦可），否则视为“未审计库存流失通道”
- rag layer 可见且未完成库存审计 → soft block（不得按稳定两相分配流程继续放大复制）

#audit：rag layer 的关键不是“能否快速消除”，而是“是否造成未审计的库存流失”。

### case 4｜温度窗口作为 kd 杠杆：升温/降温改变两相溶解度差（temperature window shift；phase-environment drift）

**case header**
- system：室温窗口下 kd 不理想（目标在有机相溶解度不足，或两相溶解度差过小）
- plan：开发早期对温度窗口进行探索（升温与降温两端），以改变目标在有机相/水相的相对溶解度与分配
- key drift：温度改变两相溶解度差 → kd 随温度显著变化；温度窗口切换即分配模型变更

**判定要点**
- kd 不可从室温外推到其它温度窗口；升温/降温均可能成为有效杠杆。
- 温度窗口策略需要两类证据：
  1) 目标温度窗口下的 kd 数据（至少覆盖 1→2 洗次窗口）
  2) 该温度窗口内的化学稳定性时窗论证（避免热/冷诱导分解或析出造成误读）

**控制结论**
- 缺少 kd(T) 数据或稳定性论证 → flag 或 soft block（按风险等级输出）。
- 若温度窗口可显著改善 kd，则将其作为 workup 设计变量管理（窗口迁移），而非操作技巧。

#audit：当室温 kd 不理想时，应系统评估温度窗口；避免在错误窗口重复洗涤。

### case 5｜pH 平衡下的部分成盐导致 kd 跳变（species drift）

**case header**
- system：目标为有机酸/有机碱；给定 pH 下游离态与离子态（盐态）共存；常规 TLC/HPLC 难以区分形态
- plan：wash#1 与 wash#2 的 pH/盐环境不同，或在同一 pH 下存在“形态未统一”的平衡残余
- key drift：kd 实测值反映“形态混合物”的有效分配，而非单一物种 kd

**判定要点**
- pH 控制对应形态平衡，不等价于“物种完成”。残余离子态比例由 pH–pKa 决定（每 1 pH 单位约 10×形态比变化）。
- 当 kd_free 与 kd_salt/ion 差异较大时，少量离子态即可显著拉动 kd_in_situ 偏离 kd_ref。
- “pH 达标”不构成“物种已统一”的证据；按 rule w2-2 优先触发 species-first 校验。

**控制结论**
- 若 (kd_ref − kd_in_situ) / kd_ref > 15%：优先按物种漂移处理；在排除前不进入相环境细项追因。
- 若确认存在显著形态混合且 kd 对形态高度敏感，则将“形态统一到目标比例”作为 workup 设计变量（与稳定性时窗联立）。

#audit：pH 是平衡变量，不是完成判据；少量离子态可在 kd 高敏体系中放大为明显漂移。

### case 6｜二氯甲烷（DCM）等工业不友好溶剂（Ⅲ类：路径级风险标签）

**case header**
- system：工业放大约束下，部分溶剂存在路径级风险（VOCs/三废/转移损失/带水堵塞等）
- plan：多次转移/回釜/浓缩链路放大风险暴露
- key drift：不以 kd 机理解释；输出为 industrial compatibility risk tag

**判定要点**
- 二氯甲烷在特定萃取场合可能有优势，但工业不友好风险往往系统性存在。

**控制结论**
- 输出 risk tag + path-rethink（可替代/不可替代/需约束论证），不混写为 kd 漂移原因。

#audit：这是放大可持续性问题，不应被误写为 kd 漂移机理。

### case 6b｜回收/套用溶剂导致加载漂移（phase-environment drift + 工业标签）

**case header**
- system：回收溶剂中共溶剂/含水累积改变有机相极性与携盐能力
- plan：以新鲜溶剂假设设计的窗口在回收溶剂下失效
- key drift：回收批次 ≠ 新鲜批次 → kd 漂移

**判定要点**
- “溶剂名称相同”不等价于“相环境相同”。

**控制结论**
- 回收溶剂用于萃取前需以同来源回收批次测 kd（覆盖 1→2 窗口），否则 flag。

#audit：回收溶剂会引入相环境隐性漂移；未测 kd 则属于未验证窗口运行。

### case 7｜浓度依赖 kd：非线性等温线导致的浓度窗口漂移（concentration-dependent kd）

**case header**
- system：目标物在高浓度下发生自缔合（self-association）或接近溶解度/活度边界；kd 随浓度变化而非线性
- plan：小试在低浓度窗口测得 kd，放大在更高浓度窗口运行（或洗次稀释导致浓度窗口在过程内移动）
- key drift：kd 随浓度上升显著下降（或发生曲线性变化），低浓度数据不可外推至高浓度窗口

**判定要点**
- 当体系存在自缔合/聚集、接近饱和、或显著活度系数变化时，kd 不再是常数。
- 低浓度窗口（如 2%）下的 kd 不能线性外推到高浓度窗口（如 15%）；洗次导致的稀释也可能引入“过程内 kd 漂移”。

**控制结论**
- kd 必须在最高设计浓度（worst-case concentration）下验证；高浓度窗口的 kd 不可由低浓度数据线性外推。
- 若 Δkd(1→2) > 15% 且浓度窗口同时发生显著变化，应将“浓度依赖 kd”纳入优先追因集合。

#audit：kd 的非线性可能被误判为相环境漂移；应先确认浓度窗口是否发生跨越。

### case 8｜反应-分配耦合：化学清除型洗涤中的 kd 漂移（reactive extraction drift）

**case header**
- system：洗涤同时包含化学反应（例如亚硫酸氢钠清除醛、酸洗清除碱性杂质、或其它“化学清除”型 wash）
- plan：以“洗涤=分配”为假设推进，但实际存在反应完成度差异（洗次/停留时间/当量变化）
- key drift：kd 波动来自“反应进程改变物种/库存”，而非单纯相环境变化

**判定要点**
- reactive wash 不是 partition-only；它将“反应完成度”引入 kd 的可变性。
- 反应未完成或反应窗口在洗次间不等价时，可表现为 kd 的剧烈波动或不可重复。

**控制结论**
- 一旦识别为 reactive wash，追因优先级固定为：先物种一致性校验（rule w2-2），再讨论相环境漂移。
- 未提供反应完成度论证（当量/时间/窗口）即按高返工风险 flag 处理（即使未观察到显著乳化）。

#audit：reactive wash 的核心风险是“把反应当分配”；kd 漂移常对应反应完成度问题。

## 5. 阻断规则（blocking rules）

### rule w2-1｜kd 漂移软阻断（15%）
- Δkd(1→2) > 15% 且未解释原因：soft block（禁止按原方案扩展洗涤次数）。

### rule w2-2｜物种一致性优先校验（species-first check; 15%）

**适用前提**
- 酸/碱目标体系默认存在“游离态 ↔ 离子态（盐态）”形态混合；常规 TLC/HPLC 通常不可区分。
- 触发 w2-1 后，追因顺序固定为：先物种，后相环境。

**校验定义（以 reference 为基准）**
- kd_ref：游离态/非络合态（或通过条件强制统一形态后）测得
- kd_in_situ：实际反应体系测得

若：
- (kd_ref − kd_in_situ) / kd_ref > 15%

则：
- species drift likely；在排除物种漂移前，不进入相环境漂移细项追因

补充：
- 若 kd_in_situ ≥ kd_ref，则该式不触发 species-first；转入相环境漂移追因。

### rule w2-3｜界面现象审计规则（emulsion / rag layer）
- 乳化与 rag layer 必须记录（出现洗次、静置时间、温度、盐/酸碱条件）。
- 默认按相环境漂移症状追因（离子强度/密度/界面条件/共溶剂/含水/温度）。
- 必须评估界面层 target 含量（粗定量亦可）；否则界面层视为“未审计库存流失通道”。
- 补充（自乳化倾向）：若目标物/中间体具两亲性（表面活性特征），随转化率上升可能出现自乳化增强。可将“分相时间”作为 kd 的影子指标；若分相时间随洗次呈系统性放大趋势（例如从分钟级上升到小时级或出现明显非线性增长），触发界面库存审计，并可升级为 soft block。

### rule w2-4｜工业不友好路径标签
- 二氯甲烷等路径级风险输出为 risk tag + path-rethink，不与 kd 漂移机理混写。

### rule w2-5｜回收/套用溶剂加载漂移规则（recycled solvent loading drift）
- 使用回收/套用溶剂：必须用同来源回收批次测 kd（至少覆盖 1→2）。
- 若回收溶剂与新鲜溶剂 kd 偏差 > 15%：按相环境漂移处理并追因。
- 未做该测试：flag（高返工风险）。

## 6. 方法论总结（machine-oriented）

- 控制变量：kd；关键监控点：Δkd(1→2)
- 追因顺序：rule w2-2（species-first）→ phase-environment drift
- 界面现象：rule w2-3（记录 + 目标物审计）
- 回收溶剂/工业不友好溶剂：路径级标签管理（rule w2-4 / w2-5）

## #audit

1→2 Δkd 用作早期软阻断信号；以 kd_ref vs kd_in_situ 优先识别物种漂移；对乳化与 rag layer 执行界面库存审计；对回收溶剂与二氯甲烷等路径级风险输出 risk tag 并触发 path-rethink。