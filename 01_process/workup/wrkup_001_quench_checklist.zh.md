derived_from: WRKUP-001-WORKUP-CONTROL-AUTHORITY
role: derived-decision-gate
scope: workup / quench only
status: draft
note: This file introduces no new process knowledge. It is a rejection checklist only.

---

# WRKUP-001｜Quench Control  
## Machine-Review Checklist（One Page）

> **Purpose**  
> 用于判定：  
> **当前工艺在 workup / quench 阶段是否允许进入后续步骤（放大、萃取、纯化等）**  
>
> **Rule**  
> 任一条触发否决条件 → **REJECT**  
> 本清单不提供任何优化或补救建议。

---

## A｜淬灭是否被设计为“可完成的化学反应”
（Chemically Incomplete Quench）

- A1. 反应结束时，体系是否仍处于以下任一状态？  
  ☐ 活性中间体  
  ☐ 金属 / 有机金属络合态  
  ☐ 可逆催化体系  
  ☐ 非稳定终态（需经转化才能成为最终产物）

- A2. 若 A1 为 YES，是否**明确设计并验证**了淬灭反应所需的：  
  ☐ 时间  
  ☐ 温度  
  ☐ 化学条件（如酸碱性、氧化还原环境）

- A3. “淬灭完成”的判据是否基于：  
  ☐ 活性物种被化学失活或转化  
  ☐ 稳定终态已形成  
  而非仅基于：  
  ☐ 淬灭试剂已加入  
  ☐ 操作步骤已完成

**否决条件**  
- A1 = YES 且 A2 任一为 NO  
- 或 A3 不满足  

→ **REJECT（淬灭未完成）**

---

## B｜淬灭过程中是否存在“反应性窗口”
（Partial Quench / Core Time Window）

- B1. 从淬灭开始到完全失活之前，体系是否存在任一反应性窗口？  
  ☐ 碱性窗口  
  ☐ 酸性窗口  
  ☐ 活性金属 / 高反应性络合态窗口

- B2. 在放大条件下，该窗口是否因以下原因被显著拉长？  
  ☐ 加料速度变慢  
  ☐ 混合 / 传质效率下降  
  ☐ 初期与后期淬灭条件不等价

- B3. 当前方案是否仅以以下作为淬灭成功判据？  
  ☐ 最终 pH 达标  
  ☐ 最终分析结果合格  
  而**未保证**从 t = 0 起无反应性窗口

**否决条件**  
- B1 = YES 且 B2 = YES  
- 或 B3 = YES  

→ **REJECT（核心时间窗口失控）**

---

## C｜淬灭试剂在放大条件下是否“物理可达”
（Physically Inaccessible Quench）

- C1. 在目标放大温度与加料方式下，是否存在以下风险？  
  ☐ 淬灭试剂冻结或部分冻结  
  ☐ 明显相分离或界面隔离  
  ☐ 淬灭试剂无法进入反应相

- C2. 是否在小试阶段**显式验证**了放大条件下的物理可达性  
（不依赖快速倒入或理想混合假设）？

**否决条件**  
- C1 = YES 且 C2 = NO  

→ **REJECT（物理不可达）**

---

## Final Decision

- ☐ **PASS** — 允许进入后续步骤  
- ☐ **REJECT** — 必须回退至 workup / quench 设计阶段

---

## #Audit

> 本清单的唯一功能，是防止在  
> **淬灭尚未被完整设计为可完成的化学反应时，  
> 进入任何后续工艺步骤。**
---

## Machine Annotation

```yaml
schema_version: risk_annotation_schema_v0.2
canonical_id: WRKUP-001-QUENCH-CHECKLIST
annotation_scope: derived_decision_gate
derived_from: WRKUP-001-WORKUP-CONTROL-AUTHORITY
process_stage: workup_quench_decision_gate
source_language: zh
machine_review_role: rejection_checklist_gate

transition_model: nominal_reaction_end_to_quench_completion_authority

core_judgment: >
  如果淬灭尚未被设计并验证为可完成的化学反应，工艺不得越过 workup / quench 阶段进入后续步骤。
  在活性物种、反应性窗口或物理不可达风险仍可能存在时，淬灭试剂已加入、最终 pH 达标、
  或操作步骤完成，都不足以证明化学终止已经成立。

risk_signals:
  - 名义反应结束时仍有活性物种
  - 淬灭未被明确设计为可完成的化学反应
  - 以淬灭试剂加入作为淬灭完成判据
  - 以操作步骤完成作为稳定终态形成判据
  - 淬灭开始至完全失活之间存在反应性窗口
  - 放大条件拉长反应性淬灭窗口
  - 最终 pH 被用作唯一淬灭成功证据
  - 最终分析结果合格但未排除早期反应性窗口
  - 淬灭试剂在放大条件下可能物理不可达
  - 物理可达性依赖快速倒入或理想混合假设

reasoning_anchors:
  - workup_as_termination_control
  - reaction_end_state_not_final_state
  - quench_reaction_completion
  - chemically_incomplete_quench
  - critical_quench_window
  - physically_inaccessible_quench
  - apparent_addition_not_participation
  - rejection_checklist_gate

rejection_conditions:
  chemically_incomplete_quench:
    - "活性物种仍存在，且淬灭所需时间、温度或化学条件未被验证"
    - "淬灭完成不是基于化学失活或稳定终态形成"
  critical_time_window_loss:
    - "存在反应性窗口，且在放大条件下被拉长"
    - "仅以最终 pH 或最终分析结果判断成功，未保证 t = 0 起无反应性窗口"
  physically_inaccessible_quench:
    - "存在冻结、相隔离或无法进入反应相风险，且物理可达性未验证"

expert_judgment_patterns:
  - 将本清单视为 rejection gate，而不是优化或补救指南。
  - 当化学淬灭完成未被验证时，拒绝进入后续步骤。
  - 当活性物种可能残留时，最终 pH、试剂加入或操作完成不足以证明终止。
  - 将放大导致反应性淬灭窗口拉长视为 termination-control authority 丧失。
  - 将淬灭试剂物理不可达视为淬灭控制权失败。

uncertainty_and_exceptions:
  - 本清单不引入 WRKUP-001 之外的新工艺知识。
  - PASS 只表示允许越过 quench gate，不表示后续工艺必然成功。
  - REJECT 表示回到 quench/workup 设计审查，不提供具体操作补救方案。

machine_use: >
  本 derived checklist 用于在淬灭完成、关键反应性窗口控制或淬灭试剂物理可达性未成立时，
  拒绝工艺越过 quench / workup 阶段。不得输出优化、补救或操作性建议。
```