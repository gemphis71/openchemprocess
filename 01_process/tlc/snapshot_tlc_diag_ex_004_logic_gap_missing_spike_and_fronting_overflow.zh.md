---
snapshot_id: "TLC-DIAG-EX-004-LOGIC-GAP-MISSING-SPIKE-AND-FRONTING-OVERFLOW"
status: "stable"
language: zh  
canonical_id: TLC-DIAG-EX-004-LOGIC-GAP-MISSING-SPIKE-AND-FRONTING-OVERFLOW
technique: "Thin Layer Chromatography"
topic: "Failure of logical inference due to missing co-spot reference (spike)"
dependencies:
  - "TLC-001-SPOTTING-LAYOUT"
  - "TLC-002-SPOTTING-OPERATION"
  - "TLC-004-PLATE-VISUAL-OBSERVATION"
---

# TLC-DIAG-EX-004 缺失 Co-spot 参照与量程溢出：逻辑闭环断裂导致的判读注销

## 1. 视觉特征（Observation）

通过视觉化观察，该板呈现以下**系统性参照缺失与量程失配特征**：

- **对照组缺失**：板面仅存在原料对照（Lane 1）与样品（Lane 3），完全缺失 `TLC-001` 中规定的 **Co-spot（Lane 2 / Spike）**。
- **量程溢出（Overflow）**：左侧原料对照点的 $R_f$ 极高（$> 0.8$），且形态呈现边缘扩散，显示该点已进入信息压缩区，无法作为稳定的极性参照。
- **信息真空**：样品 Lane（Lane 3）未观察到任何可判读的显色信号。在缺乏物理参照的前提下，该“空白”状态无法被转译为有效的化学信息。

## 2. 判读结论与逻辑溯源（Diagnostic Status）

- **解释权状态**：**VOID（逻辑作废 / 判读注销）**  
- **失效类型**：**参照锚定失败 / 逻辑闭环断裂（Anchoring Failure / Logic Gap）**

在本案例中，由于 **Co-spot 的缺失**，系统无法建立样品、原料与反应体系之间的最小物理锚点，直接导致以下不可消解的不确定性：

- **因果关系不可分辨性**：无法区分“反应完全且产物不显色”“点样过稀或失败”“基质效应抑制显色”等互斥状态；
- **物理位移陷阱**：缺乏 Co-spot，使得任何可能存在的 $R_f$ 位移均无法被识别或校正；
- **标尺标定失效**：原料对照点已超出有效判读区间，进一步放大了参照缺失带来的逻辑断裂。

因此，该板在逻辑上**不具备进入任何化学判读流程的前提条件**。

## 3. 阻断规则（Mandatory Blocking Rules）

- **Rule-001（Spike 强制性）**：  
  在定性反应监测中，若样品信号缺失且未设置 Co-spot（SM + Reaction Mixture），则判定该板的信息熵为零，禁止做出“原料消失”“反应完成”等结论。
- **Rule-002（有效量程锚定）**：  
  原料对照点的 $R_f$ 必须锚定在 **0.2–0.7** 的有效判读区间内；若参照点冲顶，则全板的相对极性比较逻辑自动失效。
- **Rule-003（优先级原则）**：  
  参照缺失属于**测量设计层失败**，其判定优先级高于显色、展开剂选择或表面相互作用等化学层判定。

## 4. 处置建议（Corrective Actions）

以下措施仅用于**重新获得判读资格**，不构成对当前板面的补救性解释：

1. **重构点样布局**：严格执行 `TLC-001-SPOTTING-LAYOUT` 规定的 **[原料 | 共点 | 样品]** 三联式布局，建立最小物理参照；
2. **重标投影轴**：降低展开剂极性，使原料点回落至中等 $R_f$ 区间，为协同定位提供可用标尺；
3. **禁止逻辑补救**：在缺失 Co-spot 的原始数据上，严禁通过经验猜测、显色强化或图像解释来“挽回”判读权。

## 5. 物理失效证据（Physical Evidence）

- **参照缺失性**：板面不存在用于校准 $R_f$ 位移或确认点身份的共点结构；
- **信息不可逆性**：由于协同定位数据在实验设计阶段未被采集，该次展开在逻辑上不可重建，属于**非法实验输入**。
---

## Machine Annotation Candidate

```yaml
candidate_status: candidate_only_not_indexed
schema_version: risk_annotation_schema_v0.2
canonical_id: TLC-DIAG-EX-004-LOGIC-GAP-MISSING-SPIKE-AND-FRONTING-OVERFLOW
annotation_scope: diagnostic_example_candidate
source_language: zh
candidate_parent: TLC-001-SPOTTING-LAYOUT
candidate_secondary_parent: TLC-DIAG-001-INTERPRETABILITY-GATE
candidate_tertiary_parent: TLC-DIAG-002-INTERPRETATION-PATHWAYS
jsonl_status: not_added
registry_status: not_added
taxonomy_status: example_terms_not_promoted
future_subsnapshot_watch: true

candidate_decision: >
  本诊断例子强烈复用了已建立的 reference-layout 与 logical void 语义。
  缺失 co-spot 参照、样品信号缺乏锚定、原料对照冲顶共同构成测量设计层失败，
  从逻辑上阻断化学判读。虽然本例结构价值较高，未来可能具备 sub-snapshot entry 资格，
  但本批仍保持 candidate-only，避免把单个例子过早转化为新的索引化 taxonomy 对象。

reused_reasoning_anchors:
  - reference_layout_validity
  - co_spot_anchoring
  - matrix_shift_compensation
  - identity_consistency_check
  - logical_void_status
  - interpretability_gate
  - projection_axis_compression
  - prohibited_quantitative_conversion

candidate_example_terms_watchlist:
  - missing_co_spot_reference
  - anchoring_failure
  - logic_gap
  - measurement_design_layer_failure
  - information_vacuum
  - range_overflow
  - non_reconstructible_plate_data

directly_supported_review_signals:
  - co-spot 参照缺失
  - 样品 lane 为空白或缺乏可解释信号
  - 原料参照超出有效判读区间
  - 样品 lane 空白不能解释为反应完成
  - 缺少 co-spot 时无法识别或校正 Rf 位移
  - 当前板状态为逻辑 VOID
  - 原始数据不能通过经验猜测或增强显色修复

machine_review_boundary: >
  本 candidate 作为 missing reference anchoring 导致 logical void status 的高价值 supporting example。
  不应把重构布局或重标投影轴等动作转化为 SOP 建议。
  本轮不加入 JSONL，但应保留 future sub-snapshot watch，
  因为它直接强化 co-spot anchoring、reference-layout validity 和禁止推断反应完成的边界。
```
