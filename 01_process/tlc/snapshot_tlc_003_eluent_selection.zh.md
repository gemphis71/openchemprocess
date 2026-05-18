---
snapshot_id: "TLC-003-ELUENT-SELECTION"
status: "stable"
language: zh  
canonical_id: TLC-003-ELUENT-SELECTION
technique: "Thin Layer Chromatography"
topic: "Eluent Selection Logic"
dependencies:
  - "TLC-PRE-002-SAMPLE-PREPARATION-GATE"
  - "TLC-002-SPOTTING-OPERATION"
  - "TLC-000-ORIGIN-LINE"
  - "TLC-001-SPOTTING-LAYOUT"
---

# TLC-003 展开剂选择逻辑 (Eluent Selection)

## 1. 核心定义
展开剂并非中性介质，而是决定 **物质迁移行为如何被投影到板面坐标系** 的核心变量。选择展开剂本质上是选择一个合适的 **“信息投影轴”**，使化合物间的极性差异以可判读的方式显现。

## 2. 展开剂作为“极性投影轴”
在常规硅胶体系中，展开剂由大极性组分（主导洗脱能力）和小极性组分（拉伸分辨区间）构成。在稳定区间内，展开剂比例与 $R_f$ 呈稳定相关，构成一条可预测的极性标尺。

## 3. 常规非水体系：可预测的极性标尺

### 3.1 酯 / 烷烃体系（EtOAc / Heptane）
规律性极强的投影轴，用于建立 **化合物相对极性顺序**。
- **失效判定**：低比例仍留基线（超量程）；高比例全部冲顶（信息压缩）。
- **适用边界**：该比例–$R_f$ 的相关性仅在点形正常、未发生拖尾或表面强吸附时成立；若点形异常，该相关性自动失效，不得用于极性推断。

### 3.2 酯 / 卤代烃体系（EtOAc / DCM）
更紧凑的中高极性投影轴。用于在较短比例扫描范围内快速覆盖常规有机极性区。

## 4. 高极性水参与体系：有机 / 无机判别轴

### 4.1 DCM / MeOH / H₂O (三相混合体系)
极端高极性轴，价值在于 **物质类型（有机 vs 无机）** 的快速判别。
- **稳定均相窗口的典型比例**：**DCM / MeOH / $H_2O$ = 3 / 2 / 0.5 (v/v)**。
- **风险提示**：偏离该窗口易发生分相（非均相），使判读失效。
- **判读逻辑**：有机物集体上移，无机盐/强离子物质留驻基线。
- **禁止逻辑**：禁止用于有机物间的精细分离或转化率推导。

## 5. 展开剂酸碱修正：表面相互作用解耦

### 5.1 微酸性环境（添加 AcOH）
削弱酸性官能团与硅胶 Si-OH 的强氢键作用。点形收敛即证明存在强极性酸性特征。

### 5.2 微碱性环境（添加 $NH_3$）
屏蔽硅胶表面酸性位点，减少碱性点拖尾。若氨水导致分相或 $R_f$ 漂移，则判定为不稳定判读条件。

### 5.3 逻辑约束
酸碱添加仅用于解除板面相互作用导致的投影畸变，不等同于对样品进行实质性化学处理，其结果仅在 TLC 判读语境中有效。

## 6. 信息有效区与失效区 (Resolution & Non-inferable Zones)

### 6.1 高分辨率投影区 (High Resolution Zone)
- **有效 $R_f$ 区间**：优先信任落在 **0.2 – 0.7** 之间的信息。
- **理由**：靠近基线（< 0.2）或溶剂前沿（> 0.7）的区域，分辨率显著下降，不建议用于精细的反应进度（转化率）推断。

### 6.2 失效判定 (Failure Criteria)
以下情况禁止进入后续 DIAGNOSTIC 逻辑：
- 极点压缩（全部点 < 0.2 或全部点 > 0.8）。
- 物理性漂移（分相或含水量过高导致 $R_f$ 失去规律）。
- 严重拖尾且未进行酸碱解耦修正。

## 7. 边界声明
本文件仅定义展开剂作为投影工具的逻辑，不提供具体配方，不解释反应机理。
---

## Machine Annotation

```yaml
schema_version: risk_annotation_schema_v0.2
canonical_id: TLC-003-ELUENT-SELECTION
annotation_scope: chapter_level
process_stage: tlc_projection_axis_selection
source_language: zh
machine_review_role: projection_axis_validity_gate

transition_model: eluent_selection_to_information_projection_axis

core_judgment: >
  在 TLC 中，展开剂选择定义的是信息投影轴，而不是中性溶剂选择。
  只有当展开剂体系能把化合物差异投影到可用 Rf 区间，且不发生信息压缩、
  分相失稳、未解耦的表面相互作用或 Rf 规律丧失时，TLC 板才具备可解释性。

risk_signals:
  - 展开剂体系无法将关键组分投影到有效 Rf 区间
  - 所有关键点位停留在基线附近
  - 所有关键点位运行到溶剂前沿附近
  - 点形异常时仍使用比例-Rf 相关性进行推断
  - 拖尾或强表面吸附使极性推断失效
  - 含水或高极性展开体系发生分相
  - 有机/无机判别轴被用于有机物精细分离
  - 展开剂酸碱修饰被当作样品实质化学处理
  - 严重拖尾未经过表面相互作用解耦
  - 投影轴失效仍被用于转化率或机理推断

reasoning_anchors:
  - interpretability_gate
  - projection_axis_validity
  - information_projection_axis
  - projection_axis_compression
  - rf_regular_projection
  - surface_interaction_decoupling
  - non_inferable_zone

tlc_specific_review_triggers:
  effective_rf_range: "优先信任 Rf 0.2-0.7 区间内的信息"
  baseline_compression: "关键点位低于 Rf 0.2"
  front_compression: "关键点位高于 Rf 0.8"
  phase_instability: "高极性含水体系偏离稳定均相窗口并发生分相"
  dcm_meoh_water_reference_window: "DCM / MeOH / H2O = 3 / 2 / 0.5 作为 TLC 特异性均相窗口参考"
  acid_base_modification_boundary: "酸碱添加仅用于解耦表面相互作用，不构成样品结构证明"

expert_judgment_patterns:
  - 在使用 Rf 进行推断前，先把展开剂选择视为投影轴选择。
  - 将基线压缩、前沿压缩和分相失稳视为投影轴失效。
  - 点形异常或强表面相互作用占主导时，不应推断极性顺序。
  - 酸碱修饰只能作为 TLC 表面相互作用解耦证据，不是确定性结构证明。
  - 不应将有机/无机判别轴用于有机物精细分离或转化率推断。

uncertainty_and_exceptions:
  - 比例-Rf 相关性只有在点形稳定且投影行为规律时才成立。
  - 高极性含水体系可用于有机/无机判别，但不适用于有机组分精细判读。
  - TLC 特异性展开剂比例和 Rf 区间是 review trigger，不是通用层析规则。

machine_use: >
  本 annotation 用于在 TLC 判读前，审查展开剂体系是否形成有效信息投影轴。
  如果展开剂导致信息压缩、分相失稳、表面相互作用未解耦或 Rf 规律丧失，
  应限制或拒绝后续极性、组分数、转化率或机理推断。
```