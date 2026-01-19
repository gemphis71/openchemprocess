---
snapshot_id: "TLC-DIAG-EX-005-STARTING-MATERIAL-STAGNATION-AND-POLARITY-GAP"
status: "stable"
technique: "Thin Layer Chromatography"
topic: "Interpretability revoked due to absence of starting material migration"
dependencies:
  - "TLC-001-SPOTTING-LAYOUT"
  - "TLC-003-ELUENT-SELECTION"
  - "TLC-004-PLATE-VISUAL-OBSERVATION"
related:
  - "TLC-DIAG-EX-001-FRONTING-BAND-AND-BASELINE-COMPRESSION"
  - "TLC-DIAG-EX-003-LOW-RF-TRIANGULAR-TAILING-SURFACE-INTERACTION"
---

# TLC-DIAG-EX-005 原料未迁移：起点投影缺失导致的判读撤销

## 1. 视觉特征（Observation）

通过视觉化观察，该板呈现以下**决定性的起点失效特征**，并伴随高端形貌异常：

- **原料端起点滞留（Starting Material Stagnation）**：  
  Lane 1（SM）中，绝大部分信号停留在点样原点，仅有极少量拖尾上行。未形成可定义的迁移中心，$R_f \approx 0$。
- **样品端伴随形貌异常（Secondary Feature）**：  
  Co-spot 与 Sample Lane 中的信号迁移至极高 $R_f$ 区（$> 0.8$），点形呈现火焰状或前沿压缩趋势，前端浓度明显升高，存在多组分重叠的高度可能性。
- **有效区间缺失**：  
  板面在 0.2–0.7 的高分辨率投影区间内，未能形成同时关联原料与样品的稳定参照。

其中，**原料端未形成有效迁移**构成该板不可判读的首要且充分条件。

## 2. 判读结论与逻辑溯源（Diagnostic Status）

- **解释权状态**：**REVOKED（撤销）**  
- **失效类型**：**起点投影缺失（Starting Material Projection Failure）**

在本案例中，由于原料未能离开起点，反应监测所依赖的最小物理投影未被生成，直接导致：

- 无法确认原料是否真实参与反应，或仅因溶解度/表面相互作用因素而滞留；
- 无法将样品端的任何迁移信号与原料建立可比关系；
- 任何关于“反应发生 / 未发生 / 已完成”的推断均缺乏物理基础。

即使样品端存在可见迁移信号，该板在逻辑上仍**不具备进入判读流程的资格**。

## 3. 与相关模式的关系（Relation to EX-001）

- **EX-001（投影轴压缩）**：  
  原料与样品均可迁移，但同时落入信息压缩区，导致分辨失败。
- **EX-005（起点投影缺失）**：  
  原料端未形成任何可用迁移投影，反应监测逻辑在起点即告终止。

因此，EX-005 可视为 **EX-001 的更早期、更严格失效形态**：  
在尚未进入“投影轴压缩”讨论之前，判读权已被直接撤销。

## 4. 阻断规则（Mandatory Blocking Rules）

- **Rule-001（原料迁移前置）**：  
  若原料对照点未形成可重复、可定义的迁移（即绝大部分信号滞留在基线），整板解释权直接撤销。
- **Rule-002（样品信号不可补救）**：  
  在原料迁移失败的前提下，样品或 co-spot 中出现的任何迁移信号均不得用于补偿或推断反应状态。
- **Rule-003（优先级原则）**：  
  起点投影缺失属于反应监测的前置失败，其阻断优先级高于展开剂选择、显色方式或表面相互作用调整。

## 5. 操作性处置与策略（Corrective Actions）

以下措施仅用于**重新获得判读资格**，不构成对当前板面的解释：

1. **优先恢复原料迁移**：  
   通过调整展开体系或表面相互作用条件，使原料点能够形成稳定迁移。
2. **拆分观察轴而非折中**：  
   将原料与样品的观察拆分到不同极性体系中，避免试图用单一折中条件同时覆盖两端。
3. **重新生成数据**：  
   在原料迁移条件满足前，当前板面数据在逻辑上不可复用。

## 6. 物理失效证据（Physical Evidence）

- **起点锚定失败**：原料未离开起点，导致反应监测的物理参照在最底层即缺失。
- **信息不可恢复性**：由于起点投影未生成，该次展开无法通过任何视觉后处理或经验补救获得判读价值。
