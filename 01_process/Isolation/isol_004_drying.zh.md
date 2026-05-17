---
snapshot_id: "ISOL-004-DRYING"
status: "draft"
domain: "Process"
process: "Isolation"
topic: "干燥：控制权终结与状态锁定"
level: "001"
language: zh  
canonical_id: ISOL-004-DRYING
dependencies:
  - "ISOL-003-FILTRATION"
note:
  - "面向 machine-review：干燥不是'如何烘干'，而是固液分离之后，溶剂状态与位置如何决定最终失效路径的锁定阶段。其核心任务是在既定固体状态下识别表面组成漂移、结合态溶剂滞留与路径级不可行性。"
---

# ISOL-004：干燥

## 1. 系统角色与控制权边界

干燥位于 ISOL-003（过滤）之后，是**上游固体状态在最终产品中的投影锁定阶段**。

- **控制权定义**：干燥 = 在有限控制权下，对“溶剂状态 × 溶剂位置”的最终锁定。
- **不可逆性**：产品分布、晶型、粒径形貌、孔道结构及初始溶剂结合态在进入本章前已默认锁定，干燥阶段无法逆转。
- **控制权特征**：温度、真空、机械力等变量仅能改变溶剂的迁移路径与释放速率，不能将“结合态”转为“自由态”（除非引入状态转换）。

---

## 2. 继承状态（Inherited State）

本章逻辑核心在于识别由上游（ISOL-001/002/003）移交的固体物理化学特征。

### 2.1 溶剂分布与位置

- **表面态**：附着于颗粒外表面的液膜
- **结构态（孔道）**：由针状/棒状颗粒堆积形成的物理孔道，或晶体内部孔道中的滞留溶剂

### 2.2 表面组成漂移逻辑

- **关键点**：表面溶剂组成 ≠ 母液组成
- **失效诱因**：若良溶剂与固体亲和力更强或不良溶剂更易挥发，干燥初期不良溶剂优先离开，导致表面残留液中良溶剂比例被动上升

### 2.3 形貌与结合能

- **形貌影响**：针状/棒状颗粒易形成孔道，产生空间滞留
- **结合力性质**：盐型体系与可形成氢键的溶剂易形成结合态。常规真空难以去除，残留溶剂将进入平台期

---

## 3. 状态演化与失效路径（State Transition & Failure Modes）

干燥不是溶剂含量的单调下降，而是状态迁移与失效显化的叠加。

### Case 1：表面驱动型团聚（起球）

- **演化路径**：不良溶剂优先挥发 → 表面良溶剂富集 → 跨越溶解阈值 → 表面微观再溶解 → 双锥滚动碰撞 → 粘连放大 → 宏观起球
- **本质变量**：表面组成漂移
- **触发条件**：
  - [表面良溶剂处于高风险状态]
  - [不良溶剂优先挥发]
  - [设备具备滚动阶段]
- **干预路径**：前置不良溶剂漂洗，或引入“先静态真空、后滚动”的阶梯干燥路径

### Case 2：孔道结合态溶剂滞留

- **演化路径**：溶剂进入孔道 → 与产物形成氢键/离子相互作用 → 转为结合态 → 蒸气压降低 → 传质驱动力不足 → 残留溶剂曲线进入平台期
- **本质变量**：溶剂结合状态
- **触发条件**：
  - [针状/棒状形貌]
  - [盐型]
  - [可形成氢键的溶剂]
  - [方案仅依赖真空/温度/时间]
- **干预路径**：溶剂置换。以可替代溶剂置换孔道溶剂。

---

## 4. 放大敏感性与决策逻辑

### 4.1 尺度效应（Scale Sensitivity）

- 实验室静态条件可能掩盖双锥滚动下的起球风险
- 实验室薄层条件可能掩盖生产厚层中的孔道滞留与传质限制

### 4.2 决策逻辑门（Decision Gates）

1. **Gate 1（溯源）**：出现起球或平台期时，优先判定为上游结晶/过滤产生的状态问题，而非干燥参数问题
2. **Gate 2（补偿）**：评估是否可通过“静态预干燥”或“溶剂置换”在干燥阶段完成损失控制
3.  **Gate 3（重构）**  ：若补偿无效，则返回上游重构固体形态、盐型或溶剂体系


---

## 5. #Audit：影子指标与审计要求

| 指标字段 | 阈值/标志 | 审计意义 |
|---|---|---|
| `surface_good_solvent_state` | 高 / 中 / 低 | 预测再溶解/起球风险 |
| `surface_composition_drift` | 有 / 无 | 识别起球前提是否存在 |
| `morphology_tag` | needle / rod / other | 孔道滞留预警 |
| `is_salt_form` | true / false | 结合态风险必要条件 |
| `solvent_hbond_capability` | true / false | 结合态风险必要条件 |
| `plateau_check` | 是 / 否 | 判定常规干燥动力学失效 |
| `static_drying_ratio` | 高 / 中 / 低 | 评估针对起球的工艺鲁棒性 |

**#Audit：干燥方案若仅有“延长真空时间”作为变量，不足以应对结构性滞留。**  
**#Audit：表面组成漂移 × 滚动 = 起球；孔道结构 × 结合态溶剂 = 平台期。**

## 6. Machine Annotation

```yaml
schema_version: "risk_annotation_schema_v0.2"
annotation_scope: "chapter_level"
canonical_id: "ISOL-004-DRYING"
process_stage: "isolation_drying"

transition_model: "filtered_wet_solid_to_final_solvent_state_and_location_lock_in"

control_window: >
  Drying occurs after filtration and represents the final lock-in of solvent state and solvent location within the solid inventory. Product/impurity distribution, polymorph, morphology, pore structure, and initial solvent-binding state are inherited from upstream. Drying variables such as temperature, vacuum, and mechanical action mainly alter solvent migration pathways and release rates; they do not restore upstream composition or solid-state control authority.

core_judgment: >
  The central machine-review task is to detect whether a drying problem is being misattributed to drying parameters when it is more likely caused by inherited surface solvent state, pore-bound solvent retention, morphology, salt form, or solvent-binding behavior. Extended vacuum time alone should not be treated as a sufficient strategy for structural solvent-retention problems.

review_gates:
  attribution_gate:
    - "balling or agglomeration occurs"
    - "residual solvent curve reaches plateau"
    - "surface re-dissolution suspected"
    - "drying failure appears only under rolling or thick-bed scale conditions"
  compensation_gate:
    - "assess whether static pre-drying can reduce rolling-induced balling"
    - "assess whether solvent displacement can convert pore-bound or strongly retained solvent into a more removable solvent state"
    - "assess whether pre-wash with anti-solvent can reduce surface good-solvent enrichment"
  reconstruction_gate:
    - "if static pre-drying or solvent displacement fails, return upstream to redesign morphology, salt form, or solvent system"
    - "if drying relies only on vacuum, temperature, and time despite bound-solvent plateau, upstream reconstruction is required"

risk_signals:
  - "surface_good_solvent_state high"
  - "surface_composition_drift yes"
  - "surface solvent composition differs from mother liquor composition"
  - "anti-solvent preferential evaporation"
  - "good solvent enriched at particle surface"
  - "surface re-dissolution during early drying"
  - "rolling stage present in equipment"
  - "double-cone rolling collision after surface good-solvent enrichment"
  - "macroscopic balling observed"
  - "agglomeration during drying"
  - "needle or rod morphology"
  - "pore structure likely from particle packing"
  - "solvent retained in internal or interparticle pores"
  - "salt form present"
  - "hydrogen-bond-capable solvent present"
  - "ionic or hydrogen-bond interaction between solvent and product suspected"
  - "process relies only on vacuum, temperature, and time"
  - "residual solvent curve reaches plateau"
  - "plateau_check yes"
  - "static lab drying masks rolling-induced balling"
  - "thin-layer lab drying masks pore retention"
  - "thick-bed mass-transfer limitation suspected"
  - "extended vacuum time used as sole corrective action"

reasoning_anchors:
  - "control_authority_decay"
  - "solid_state_commitment"
  - "misallocated_control_authority"
  - "consequence_stage_separation"
  - "structure_inheritance"
  - "upstream_failure_exposure"
  - "lab_scale_masking"
  - "scalability_failure"
  - "drying_state_lock_in"
  - "solvent_state_location_lock_in"
  - "surface_composition_drift"
  - "surface_good_solvent_enrichment"
  - "surface_redissolution"
  - "rolling_agglomeration"
  - "pore_bound_solvent_retention"
  - "bound_solvent_state"
  - "drying_plateau"
  - "static_predrying"
  - "solvent_displacement"
  - "drying_compensation_boundary"

taxonomy_role:
  reused_formal_anchors:
    - "control_authority_decay"
    - "solid_state_commitment"
    - "misallocated_control_authority"
  reused_candidate_terms:
    - "consequence_stage_separation"
    - "structure_inheritance"
    - "upstream_failure_exposure"
    - "lab_scale_masking"
    - "scalability_failure"
  candidate_anchors:
    - "drying_state_lock_in"
    - "solvent_state_location_lock_in"
    - "surface_composition_drift"
    - "surface_good_solvent_enrichment"
    - "surface_redissolution"
    - "rolling_agglomeration"
    - "pore_bound_solvent_retention"
    - "bound_solvent_state"
    - "drying_plateau"
    - "static_predrying"
    - "solvent_displacement"
    - "drying_compensation_boundary"

expert_judgment:
  - "Drying should be reviewed as final solvent-state and solvent-location lock-in, not as a neutral solvent-removal operation."
  - "Balling should first be reviewed as surface composition drift plus mechanical rolling amplification, not simply as excessive drying temperature or insufficient vacuum."
  - "Residual solvent plateau should first be reviewed as possible pore-bound or chemically bound solvent retention, not simply as insufficient drying time."
  - "Static laboratory drying may underpredict balling risk in rolling equipment, and thin-layer laboratory drying may underpredict pore-retention risk in thick beds."
  - "Drying-stage interventions such as static pre-drying, pre-wash, or solvent displacement are compensatory controls; if they fail, upstream morphology, salt form, or solvent system must be reconsidered."
  - "A drying strategy relying solely on extended vacuum time is insufficient for structural retention or bound-solvent problems."

uncertainty_and_exceptions:
  - "Balling should not be inferred from solvent composition alone unless rolling, adhesion, or surface re-dissolution risk is also present."
  - "Bound-solvent retention should not be inferred from salt form alone unless solvent-binding capability, pore retention, or plateau behavior is observed or expected."
  - "Solvent displacement may be valid when it changes the solvent state inside pores, but it should not be described as recovery of upstream solid-state control authority."
  - "Extended drying time may be acceptable for free solvent removal, but not as the only response to plateau behavior caused by bound or pore-retained solvent."
  - "Surface composition drift may differ from bulk mother liquor composition; machine review should avoid assuming bulk liquid composition represents the drying surface state."

quantitative_or_flag_triggers:
  surface_good_solvent_state: "high / medium / low"
  surface_composition_drift: "yes / no"
  morphology_tag: "needle / rod / other"
  is_salt_form: "true / false"
  solvent_hbond_capability: "true / false"
  plateau_check: "yes / no"
  static_drying_ratio: "high / medium / low"
  rolling_equipment_present: "yes / no"
  process_relies_only_on_vacuum_temperature_time: "yes / no"

required_review_fields:
  - "surface_good_solvent_state"
  - "surface_composition_drift"
  - "surface_solvent_composition_basis"
  - "morphology_tag"
  - "pore_structure_assessment"
  - "is_salt_form"
  - "solvent_hbond_capability"
  - "solvent_binding_state"
  - "plateau_check"
  - "rolling_equipment_present"
  - "static_drying_ratio"
  - "solvent_displacement_option"
  - "upstream_reconstruction_option_if_any"

machine_use: >
  Review whether a drying failure is caused by inherited solvent state and solvent location rather than drying parameters alone; distinguish surface-composition-drift-driven balling from pore-bound solvent plateau; check whether static pre-drying, anti-solvent pre-wash, or solvent displacement are valid compensatory controls; and identify when upstream morphology, salt form, or solvent-system reconstruction is required.
```