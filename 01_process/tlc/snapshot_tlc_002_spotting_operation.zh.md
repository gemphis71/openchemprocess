---
snapshot_id: "TLC-002-SPOTTING-OPERATION"
status: "stable"
language: zh  
canonical_id: TLC-002-SPOTTING-OPERATION
technique: "Thin Layer Chromatography"
topic: "Spotting Methodology"
dependencies: 
- "TLC-001-SPOTTING-LAYOUT"
- "TLC-PRE-002-SAMPLE-PREPARATION-GATE" 
---

## 1. 适用范围
本 Snapshot 定义 **TLC 点板操作**的标准规范。前提是样品已确认稳定性与代表性，且为单相均一溶液。

## 2. 工具与浓度标准

### 2.1 毛细管选择
- **首选内径**：**0.5 mm**（平衡了抗堵塞能力与点样稳定性）。
- **备选**：0.3 mm。

### 2.2 推荐浓度区间
- **目标浓度**：**0.2–0.3 M**（工作区间 0.1–0.5 M）。
- **高浓度处理**：若体系 >0.5 M，建议取样稀释至目标区间，以防点径失控。

## 3. 点样动作与控制 (Spotting Motion)
- **标准动作**：轻触板面 → 极短停留 → 垂直快速离板。依靠毛细作用转移，严禁压点或摩擦。
- **合格点径**：初始点径约 **0.5 mm**，展开后理想点径为 **1–2 mm**。
- **不合格判定**：点径明显 >2 mm 则视为信号失真，不具半定量意义。

--- 
## 3.1 预处理操作衔接 (Integration with TECH)
若根据 `TLC-PRE-002-SAMPLE-PREPARATION-GATE` 判定样品需要进行化学预处理，点样动作需按以下规范调整：

- **板上 (In-situ) 处理**：遵循 `TLC-TECH-001-QUENCH-RECIPES` 规定的配方顺序。操作时必须**先点淬灭试剂**润湿板面，在试剂未干透前，立即使用另一根毛细管在该点位**重叠点样**。 
- **体外 (Ex-situ) 处理**：在采样瓶中完成 `TLC-TECH-001-QUENCH-RECIPES` 定义的化学转化后，将得到的均相溶液视为普通样品，执行本文件定义的标准点样动作。 
---

## 4. 多次点样 (Retouch)
- **原则**：次数 ≤3 次，上限 **5 次**。
- **模式**：
  - **连续触碰**：适用于 $R_f < 0.3$ 且点样溶剂扩散推动力小的情况。
  - **点-干-再点**：适用于溶剂极性大或样品易扩散的情况。

## 5. 干燥判据
- **物理指标**：翻转 TLC 板，玻璃背面点位的**湿痕完全消失**。
- **方式**：优先冷风干燥；热稳定样品可用 50–60 °C 热风；高沸点溶剂（DMSO/DMF）需延长干燥时间。

## 6. 诊断用异常标志 (Diagnostic Flags)
机器或人工判读时需标注：
- **Overload**：点径过大导致的超载。
- **Tailing**：包括上粗下细的长拖尾或倒三角/锥形拖尾。
- **Lateral Drift**：样点非垂直爬升的左右偏移。

> **核心定义**：点板是将化学体系编码成受控、可判读的空间信号的过程。
---

## Machine Annotation Candidate

```yaml
candidate_status: candidate_only_not_indexed
schema_version: risk_annotation_schema_v0.2
canonical_id: TLC-002-SPOTTING-OPERATION
annotation_scope: operation_validity_candidate
source_language: zh
candidate_parent: TLC-PRE-002-SAMPLE-PREPARATION-GATE
candidate_secondary_parent: TLC-004-PLATE-VISUAL-OBSERVATION
jsonl_status: not_added
registry_status: not_added
taxonomy_status: operation_terms_not_promoted

candidate_decision: >
  本 chapter 包含“点板是空间信号编码”的有价值 review 逻辑，
  但当前文本操作性较强，包含毛细管内径、点样动作、点径、多次点样限制和干燥方式等细节。
  在其 review 价值能够从 TLC 操作规范中分离，并被诊断例子复用之前，
  本文件应保持 candidate-only，不进入 JSONL，不提升 taxonomy。

reused_reasoning_anchors:
  - sample_preparation_gate
  - visual_data_object_generation
  - migration_distortion_control

candidate_example_terms_watchlist:
  - spatial_signal_encoding
  - spot_size_distortion
  - spotting_overload
  - repeated_spotting_distortion
  - drying_completeness_check
  - lateral_drift

directly_supported_review_signals:
  - 点样前提是假定样品稳定、具有代表性且为均相溶液
  - 点径过大会导致信号失真
  - 高浓度可能导致点径不可控扩张
  - 多次点样可能扭曲空间信号编码
  - 干燥不完全可能造成迁移失真
  - overload、tailing 和 lateral drift 应作为诊断标志记录

machine_review_boundary: >
  本 candidate 仅作为操作有效性 supporting reference。
  不应将毛细管选择、点样动作、多次点样上限、干燥方式或浓度建议转化为
  Machine Reviewer SOP 指令或全局 taxonomy 规则。
  只有当后续诊断例子反复复用点样相关有效性逻辑时，才考虑未来升级。
```
