---
snapshot_id: "TLC-TECH-001-QUENCH-RECIPES"
status: "stable"
language: zh  
canonical_id: TLC-TECH-001-QUENCH-RECIPES
layer: "TECH"
technique: "Thin Layer Chromatography"
topic: "Standardized Quench Recipes for TLC"
dependencies:
  - "TLC-PRE-002-SAMPLE-PREPARATION-GATE"
used_by:
  - "TLC-002-SPOTTING-OPERATION"
priority: "High"
---

# TLC-TECH-001 淬灭配方库 (Quench Recipes for TLC)

## 0. 技术定位 (Scope)

本文件定义一组**可复用、可预测的 TLC 淬灭技术配方**。本文件属于**工具箱 (TECH)** 属性，其调用逻辑由 PRE 判定决策，物理执行由 PROCESS 操作规范定义。

---

## 1. 核心化学逻辑：淬灭即衍生化

TLC 淬灭不仅是为了“终止反应”，更是为了**“主动调节 $R_f$”**：
- **减小极性 ($R_f$ 增加)**：通过醇类将活性亲电体转化为酯。
- **增加极性 ($R_f$ 减小)**：通过氨/胺类将活性亲电体转化为酰胺或脲。

---

## 2. 醇类与胺类配方库 (亲电体捕获)

### 2.1 醇类库 (Alcohol-based)
- **适用对象**：酰氯、酸酐、异氰酸酯等。
- **配方**：无水 MeOH (首选) 或 无水 EtOH。
- **逻辑**：生成热力学稳定的酯或氨基甲酸酯，点形通常圆润且迁移率适中。

### 2.2 氨/胺类库 (Amine-based)
- **适用对象**：强亲电中间体。
- **配方**：氨水 ($NH_3$ 饱和溶液) 或低分子量伯胺/仲胺。
- **逻辑**：生成酰胺或脲。由于氢键作用，产物极性通常显著高于对应的酯，用于防止组分跑在溶剂前端。

---

## 3. 弱酸与还原体系处理

### 3.1 弱酸库 (Weak Acid/Protonation)
- **适用对象**：格氏试剂、有机锂、强碱性体系。
- **配方**：**冰醋酸 (AcOH)** 或 10% AcOH/MeOH。
- **操作规范 (In-situ)**：必须遵循**“先点酸，再点样”**的顺序。先用酸湿润硅胶点位，确保样品进入时立即质子化。

### 3.2 强还原剂体系 (Hydride Quench)
- **适用对象**：$NaBH_4$, $DIBAL-H$, $LiAlH_4$。
- **配方**：10% AcOH/MeOH。
- **安全警告**：高浓度时**严禁 In-situ（板上）淬灭**。剧烈的产氢过程 ($H_2$) 会物理破坏硅胶层形成“弹坑”，彻底摧毁迁移行为的完整性。

---

## 4. 浓度与操作边界 (与 TLC-PRE-002-SAMPLE-PREPARATION-GATE 联动)

- **等效浓度 < 0.5 M**：允许执行 In-situ（板上）淬灭，但必须执行“试剂预湿”动作。
- **等效浓度 > 0.5 M**：强烈建议执行 Ex-situ（体外）淬灭，即在取样瓶中预混后再点样。
- **等效浓度 ≥ 1.0 M**：**强制**执行 Ex-situ 淬灭，以确保淬灭完全且点样量受控。

---

## 5. 模块关联

- **TLC-PRE-002-SAMPLE-PREPARATION-GATE**：裁定“是否”必须淬灭。
- **TLC-002-SPOTTING-OPERATION**：裁定物理点样动作（如毛细管使用）。
- **TLC-TECH-001-QUENCH-RECIPES**：提供具体化学配方。

---

> **TECH 箴言**：淬灭的目的不是“把反应做完”，而是“把体系变成 TLC 能解释的样子”。


## Machine Annotation Candidate

```yaml
candidate_status: candidate_only_not_indexed
schema_version: risk_annotation_schema_v0.2
canonical_id: TLC-TECH-001-QUENCH-RECIPES
annotation_scope: technical_recipe_candidate
source_language: zh
candidate_parent: TLC-PRE-002-SAMPLE-PREPARATION-GATE
candidate_secondary_parent: TLC-002-SPOTTING-OPERATION
jsonl_status: not_added
registry_status: not_added
taxonomy_status: recipe_terms_not_promoted

candidate_decision: >
  本 TECH 模块是在 TLC-PRE-002 已经判定需要淬灭或衍生化之后，
  提供可复用 TLC 样品预处理配方的工具箱。它通过把活性样品或难以投影的样品
  转化为更适合 TLC 判读的输入，支持 TLC 证据准入；但它不证明原始反应完成、
  workup 淬灭完成或工艺终止。由于源文件是 recipe / toolbox 属性，
  且包含具体试剂与操作程序，本文件应保持 candidate-only，
  不作为 Machine Reviewer 规则源进入索引。

reused_reasoning_anchors:
  - sample_preparation_gate
  - quench_requirement_check
  - sample_state_projection
  - migration_distortion_control
  - observation_validity_gate

candidate_example_terms_watchlist:
  - tlc_quench_recipe
  - derivatization_for_tlc_projection
  - electrophile_capture
  - alcohol_based_quench
  - amine_based_quench
  - weak_acid_protonation
  - hydride_quench_boundary
  - in_situ_quench_boundary
  - ex_situ_quench_boundary
  - recipe_not_completion_evidence

directly_supported_review_signals:
  - TLC 淬灭配方仅在 PRE gate 判定需要淬灭后被调用
  - TLC 淬灭可将活性物种转化为更适合 TLC 投影的衍生物
  - 试剂选择可通过改变极性主动调整 Rf
  - 高浓度板上淬灭可能物理破坏板面或使迁移行为失效
  - 配方执行不证明原始工艺的化学完成
  - 配方模块支持样品预处理，但不定义工艺终止控制权

machine_review_boundary: >
  本 candidate 仅作为 TLC 样品预处理的技术支持参考。
  不应将 MeOH、EtOH、氨水、胺、AcOH、AcOH/MeOH 或还原剂淬灭示例
  转化为 Machine Reviewer 的 SOP 建议。
  不应将 TLC 淬灭配方选择视为反应完成、workup 淬灭完成或工艺终止完成的证据。
  除非后续 review 证明 recipe 相关术语具有超出配方执行本身的跨 snapshot 价值，
  否则不应将其加入 taxonomy。