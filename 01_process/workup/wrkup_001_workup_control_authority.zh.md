snapshot_id: "WRKUP-001-WORKUP-CONTROL-AUTHORITY"
status: "draft"
domain: "Process"
process: "Workup"
topic: "后处理阶段的控制权、淬灭反应及放大不重现性的工程判据"
level: "001"
language: zh  
canonical_id: WRKUP-001-WORKUP-CONTROL-AUTHORITY
dependencies:
  - "CHG-001-CHARGING-SEQUENCE"
  - "CHG-002-ADDITION-MODE-AND-RATE"
  - "MIX-001-MIXING-TIME-SCALE-FAILURE"
  - "THR-001-THERMAL-CONTROL-AUTHORITY"
---
# WRKUP-001｜Workup Control Authority

## 后处理阶段的控制权与淬灭反应判据

---

## 1. 定位（Positioning）

在多数工艺中，workup 仅用于处理已经完成的反应结果。  
在以下条件同时满足时，workup 升级为**控制权来源**：

- 主反应在名义上已停止；
    
- 反应结束态中仍存在可反应物种；
    
- 稳定终态并非由主反应直接生成；
    
- 稳定终态只能通过淬灭（quench）反应获得。
    

在此类体系中：

> **反应是否真正结束，由淬灭反应是否完成决定，而非由主反应停止决定。**

---

## 2. 基本判据（Foundational Criteria）

### 判据 2.1｜反应结束态判据

若反应结束时体系中存在以下任一状态：

- 活性中间体；
    
- 金属或有机金属络合态；
    
- 可逆催化体系；
    
- 等待被转化的反应结束态物种；
    

则该状态不构成化学稳定终态。

---

### 判据 2.2｜淬灭反应判据

若体系满足以下任一条件：

- 淬灭过程具有可观动力学时间尺度；
    
- 淬灭路径不唯一，存在竞争反应；
    
- 淬灭依赖于温度、酸碱性或相态条件；
    

则淬灭必须被视为**需要显式设计与验证的化学反应**。

---

## 3. WRKUP 中的三类淬灭控制失效模式

### Ⅰ 类｜慢化学淬灭未完成型

**Chemically Incomplete Quench**

**定义**  
已加入淬灭剂，但在给定时间、温度或条件下，  
淬灭反应未完成，体系仍保持化学活性。

**必要条件**

- 淬灭为化学反应而非瞬时过程；
    
- 反应速率与放大尺度相关；
    
- 小试中易被忽略。
    

**机器判定要点**

- “已加淬灭剂”不能作为终止判据；
    
- 必须评估淬灭反应是否在设计条件下完成。
    

---

### Ⅱ 类｜核心时间窗口失控型

**Partial Quench / Pathway Competition**

**定义**  
淬灭初期存在反应性窗口，  
在放大条件下该窗口被拉长，导致反应路径主导权发生改变。

**关键特征**

- 初期淬灭条件 ≠ 后期淬灭条件；
    
- 放大导致加料时间显著增加；
    
- 副反应在淬灭初期被放大。
    

**机器判定要点**

- 评估 t = 0 至完全失活期间是否存在反应性窗口；
    
- 不以最终状态（如最终 pH）作为唯一判据。
    

---

### Ⅲ 类｜物理不可达导致的表观淬灭

**Physically Inaccessible Quench**

**定义**  
淬灭试剂表观加入体系，但由于相变或界面问题，  
未能实际进入反应相参与淬灭反应。

**说明**

- 物理原因（结冰、相分离）；
    
- 化学后果（淬灭未完成）；
    
- 放大条件下显著。
    

---

## 4. 代表性案例（保持不变，仅语言校准）

### Case 1｜DCC 缩合反应中的慢化学淬灭（Ⅰ 类）

**判定要点**

- DCC 衍生活性中间体水解为慢反应；
    
- 中性条件下动力学不足；
    
- “加水”不构成淬灭完成判据。
    

**控制结论**

- 必须提供酸性条件与足够停留时间；
    
- 仅在活性中间体完全失活后进入分相。
    

`#Audit: 淬灭完成的判据是活性中间体消失，而非淬灭剂加入。`

---

### Case 2｜酶催化体系中物理去除不等于化学淬灭（Ⅰ 类）

**判定要点**

- 过滤仅为物理操作；
    
- 残留可溶性酶仍保持催化活性。
    

**控制结论**

- 必须引入化学或热失活步骤；
    
- 否则反应逻辑在 workup 中持续存在。
    

---

### Case 3｜碱性体系逐步加酸引发的核心窗口失控（Ⅱ 类）

**判定要点**

- 淬灭初期体系整体仍为碱性；
    
- 放大导致该窗口显著拉长；
    
- 碱敏感物种发生副反应。
    

**控制结论**

- 必须保证任意时刻无反应性窗口；
    
- 推荐反转物流：反应液 → 过量酸性体系。
    

`#Audit: 淬灭控制的判据不是最终 pH，而是从 t = 0 起无活性窗口。`

---

### Case 4｜金属/有机金属体系的化学淬灭完成问题（Ⅰ 类）

**判定要点**

- 反应结束态为金属络合中间体；
    
- 稳定产物仅在淬灭后生成。
    

**控制结论**

- 必须显式设计金属失活路径；
    
- 未完成失活不得进入后续操作。
    

---

### Case 5｜低温条件下的物理不可达淬灭（Ⅲ 类）

**判定要点**

- 淬灭试剂在放大条件下发生冻结或界面隔离；
    
- 表观加入但未参与反应。
    

**控制结论**

- 必须在小试阶段验证放大物理可达性；
    
- 否则该淬灭策略不可放大。
    

`#Audit: 表观加入不等于实际参与；物理可达性是淬灭完成的前置条件。`

---

## 5. 阻断规则（Blocking Rules）

### Rule W-1｜慢化学淬灭阻断

若淬灭反应在设计条件下无法完成，则禁止进入后续步骤。

### Rule W-2｜核心窗口阻断

若淬灭过程中存在反应性窗口，且该窗口在放大时被拉长，则该方案不可接受。

### Rule W-3｜物理可达性阻断

若淬灭试剂在放大条件下存在结冰、相分离或界面隔离风险，则禁止放大。

---

## 6. 方法论总结（Machine-Oriented）

> **反应是否真正结束，是一个可判定的工程问题。  
> 判定依据不是操作是否完成，而是淬灭反应是否完成。**

WRKUP-001 的目标，是为机器提供以下能力：

- 在设计阶段识别不可放大的淬灭策略；
    
- 在异常出现时正确回溯至 workup 层；
    
- 从设计根源上消除放大的不重现性。
    

---

## #Audit

本文件用于判定 workup 是否构成反应终止控制层。  
核心判据：

**淬灭是否被设计并验证为一个可完成的化学反应。**

---

## Machine Annotation

```yaml
schema_version: "risk_annotation_schema_v0.2"
annotation_scope: "chapter_level"
canonical_id: "WRKUP-001-WORKUP-CONTROL-AUTHORITY"
process_stage: "workup_quench_control_authority"
transition_model: "nominal_reaction_stop_to_chemical_final_state_by_quench_completion"

control_window: >
  WRKUP-001 applies when the primary reaction has nominally stopped but the reaction end state is not yet a chemically stable final state. In such systems, workup becomes a reaction-termination control layer because the true end of reaction is determined by quench completion rather than by primary reaction cessation.

core_judgment: >
  Workup should be treated as a source of control authority only when reactive species remain after nominal reaction stop and a quench reaction is required to reach the chemically stable final state. The machine-review task is to detect chemically incomplete quench, critical quench-window loss, or physically inaccessible quench before downstream workup is mistaken for reaction termination.

risk_signals:
  - "primary reaction has nominally stopped but reactive species remain"
  - "reaction end state is not chemically stable final state"
  - "stable final state requires a quench reaction"
  - "quench agent added is treated as termination criterion"
  - "quench reaction has non-negligible kinetic time scale"
  - "quench pathway is not unique or involves competing reactions"
  - "quench depends on temperature, pH, or phase conditions"
  - "early quench-stage conditions differ from late quench-stage conditions"
  - "reactive window exists from t = 0 until complete deactivation"
  - "final pH is used as sole quench criterion"
  - "quench reagent is physically inaccessible due to freezing, phase separation, or interfacial isolation"
  - "apparent quench-agent addition does not imply actual participation"

expert_judgment:
  - "If reactive species remain after nominal primary reaction stop, the reaction should not be considered ended until quench completion is evidenced."
  - "If quench is a chemical reaction with time, temperature, pH, phase, or pathway dependence, it should be reviewed as a designed and validated reaction rather than an instantaneous workup operation."
  - "If a reactive window exists during quench and is elongated on scale-up, the case should be reviewed as loss of control in the critical quench window."
  - "If the quench reagent is physically isolated from the reaction phase, apparent addition should be treated as insufficient evidence of quench completion."

reasoning_anchors:
  - "control_authority_decay"
  - "misallocated_control_authority"
  - "workup_as_termination_control"
  - "reaction_end_state_not_final_state"
  - "quench_reaction_completion"
  - "chemically_incomplete_quench"
  - "critical_quench_window"
  - "physically_inaccessible_quench"
  - "apparent_addition_not_participation"

uncertainty: "medium"

exceptions:
  - "Most workup steps remain result-processing operations unless reactive species remain and a quench reaction is required to reach chemical stability."
  - "Physical removal, phase separation, filtration, or final pH alone may be insufficient if chemical deactivation has not been demonstrated."
  - "Blocking-language cases should be interpreted as design-review blocks, not as operational instructions."

machine_use: >
  Use this annotation to review whether workup constitutes a reaction-termination control layer and whether quench completion has been evidenced. Keep output in review language. Do not provide quench recipes, addition modes, pH targets, residence times, or downstream operating instructions.
```
