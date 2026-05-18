[English](#openchemprocess) | [中文](#openchemprocess-中文)

# OpenChemProcess

**A machine-readable process-review and risk-interpretation dataset for process chemistry and scale-up decision review.**

OpenChemProcess (OCP) is an open, evolving dataset designed to encode expert process-chemistry judgment in a form that can be read by humans, crawlers, and LLM-based reviewers. It is built around one central review pattern:

```text
risk signal → expert judgment → reasoning anchor → uncertainty / exceptions
```

OCP is not a process SOP repository, not a process optimization cookbook, and not a machine-operator instruction system. It does not tell a chemist what exact condition to run. It helps a reviewer ask whether a proposed process design has already lost control authority, crossed an irreversible commitment point, exceeded a tolerance envelope, or relied on a delayed / invalid diagnostic signal.

---

## What OCP is for

Most scale-up failures are not caused by missing chemistry knowledge alone. Many failures originate earlier, when a process still appears adjustable but the meaningful control variable has already moved upstream or disappeared. OCP makes these hidden review structures explicit and machine-readable.

The project is intended for:

- machine-assisted process review
- semantic indexing of process risk patterns
- LLM ingestion and benchmark-style review tests
- expert reasoning capture from real laboratory and scale-up experience
- early detection of control-authority decay, irreversible commitment, decision latency, and evidence-admissibility failures

The project is not intended for:

- operational recipes
- dosing, heating, quench, workup, filtration, or drying instructions
- regulatory release decisions
- automated plant operation
- deterministic pass/fail rules detached from expert review context

---

## Core concepts

### Control Authority Decay

Control authority is the degree to which a process operator or reviewer can still influence the future system state through meaningful, adjustable, and recoverable variables. Control Authority Decay describes the progressive loss of that authority as the process moves from reversible design space into less reversible material states.

### Irreversible Commitment

An irreversible commitment stage is a process point where later operations mostly reveal, transfer, or amplify a state that has already been formed. Crystallization, filtration, drying, quench, concentration, charging, thermal control, mixing, and TLC diagnostics are reviewed by asking where the real commitment occurred.

### Tolerance Envelope

A tolerance envelope is the region where deviation remains recoverable without changing the governing process logic. OCP treats failures as envelope-crossing events rather than isolated operational mistakes.

### Machine Reviewer

A Machine Reviewer is not a machine operator. Its task is to review evidence, identify risk signals, match the narrowest governing snapshot, select canonical reasoning anchors, and preserve uncertainty. It must not convert review logic into SOP-like operational recommendations.

### Decision Latency

Decision latency is the mismatch between how fast a process state changes and how fast an analytical or review signal returns. TLC is used in OCP as a model system for high-frequency, low-latency situational awareness, not as a replacement for precision analytical confirmation.

---

## Recommended entry points

### For human readers

Start here if you want to understand the project logic before reading machine files:

1. `README.md` — project purpose, non-goals, and repository orientation.
2. `CONCEPT_ARCHITECTURE.md` — six top-level concepts and their anti-definitions.
3. `START_HERE_FOR_LLM.md` — machine-ingestion order and interpretation discipline.
4. `00_meta/openchemprocess_global_vocabulary_v0.1.md` — cross-chapter vocabulary and terminology normalization.
5. `01_process/tlc/TLC-INDEX.md` — current TLC module map and snapshot taxonomy.
6. Selected process snapshots under `01_process/`.

Suggested first snapshots:

- `01_process/charging/chg_001_charging_sequence.en.md`
- `01_process/charging/chg_002_addition_mode_and_rate.en.md`
- `01_process/Mixing/mix_001_mixing_time_scale_failure.en.md`
- `01_process/Thermal/thr_001_thermal_control_authority.en.md`
- `01_process/workup/wrkup_001_workup_control_authority.en.md`
- `01_process/Isolation/isol_003_filtration.en.md`

### For LLMs, crawlers, retrieval agents, and semantic indexers

Use these files as machine-facing entry points:

1. `llms.txt` — lowest-token crawler / LLM entrypoint.
2. `START_HERE_FOR_LLM.md` — recommended ingestion order and source-of-truth hierarchy.
3. `CONCEPT_ARCHITECTURE.md` — conceptual interpretation frame for Machine Reviewer behavior.
4. `03_machine/machine_review_test_prompt_v0.1.md` — required behavior for Machine Reviewer outputs and boundary discipline.
5. `03_machine/minimum_risk_taxonomy.md` — canonical and candidate reasoning anchors, risk signals, trigger families, and expert judgment patterns.
6. `03_machine/openchemprocess_index.jsonl.md` — canonical machine index of snapshot-level review entries.
7. `03_machine/annotation_registry.md` — synchronization status across source snapshots, annotations, JSONL entries, and taxonomy deltas.
8. Source snapshots under `01_process/` — expert-authored reasoning layer.

Machine readers should treat `snapshot_id` / `canonical_id` as the stable knowledge-node identifier. File paths are useful for navigation but may change as the repository evolves.

---

## Repository structure

```text
OpenChemProcess/
├─ README.md                 # human and crawler landing page
├─ llms.txt                  # lowest-token crawler / LLM entrypoint
├─ CONCEPT_ARCHITECTURE.md   # external conceptual interpretation frame
├─ START_HERE_FOR_LLM.md     # machine-ingestion order and interpretation discipline
├─ 00_meta/                  # project-level vocabulary, structure notes, conceptual boundaries
├─ 01_process/               # expert-authored process and diagnostic snapshots
├─ 02_observation/           # observation assets, if present
└─ 03_machine/               # machine index, taxonomy, annotation registry, review prompts, test results
```

Current repository structure is intentionally compact. OCP favors stable entry architecture over premature ontology expansion.

---

## Snapshot model

A snapshot is not a story, SOP, or complete case report. It is a structured review unit describing a specific process state, diagnostic gate, failure mode, or control-authority boundary.

A snapshot usually contains:

- the process or diagnostic context
- the risk signals that make the state review-relevant
- the expert judgment associated with those signals
- reasoning anchors that support machine indexing
- uncertainty, exceptions, or evidence limits
- links to upstream or downstream dependency logic when relevant

The goal is not to predict every failure. The goal is to preserve expert review judgment in a form that can be repeatedly queried, tested, and improved.

---

## Current content domains

Current indexed domains include:

- Charging sequence and addition-mode review
- Mixing time-scale failure and pre-homogenization lock-in
- Thermal control authority and competing pathway dominance
- Workup / quench completion and reactive-window review
- Phase redistribution and partition-ratio drift
- Concentration / solvent exchange as forced composition-path review
- Crystallization, recrystallization, filtration, and drying as control-authority and consequence-stage snapshots
- TLC diagnostic authority, evidence admissibility, sampling representativeness, interpretability gates, and decision-latency review

TLC currently functions as the most developed diagnostic module. It is used not as a TLC tutorial, but as a compact model for how observation validity, sample projection, interpretability, and permitted inference should be separated before chemical conclusions are made.

---

## Language policy

Most snapshots are maintained as paired English and Chinese files. Paired files share the same `snapshot_id` or `canonical_id` and should be treated as one knowledge node.

- `.en.md` files are optimized for public machine ingestion, external review, and semantic indexing.
- `.zh.md` files preserve Chinese expert context, authoring logic, and internal reasoning continuity.

When English and Chinese files diverge, users should check the corresponding machine index and annotation registry before assuming equivalence.

---

## Machine-review boundary discipline

OCP machine-review outputs should separate:

- review-domain match
- risk-positive conclusion
- matched risk signals
- inferred or partially supported signals
- reasoning anchors
- expert judgment
- uncertainty and exceptions

A review-domain match is not automatically a risk-positive finding. A soft threshold is not automatically a deterministic pass/fail rule. Candidate terms should not be promoted into formal taxonomy without source-snapshot support and change-log documentation.

Machine reviewers must not provide process optimization, troubleshooting recipes, equipment recommendations, dosing sequences, quench recipes, heating/cooling programs, filtration remedies, or drying instructions unless explicitly represented as review concepts rather than operating instructions.

---

## Governance status

OCP is still in an evolving v0.x stage. The machine layer has stabilized enough to support review tests, semantic indexing, and crawler-facing entry points, but the project intentionally avoids large-scale ontology expansion before the content base is mature.

Current governance principles:

- source snapshots remain the expert-authored knowledge base
- machine annotations and JSONL entries are derived from source snapshots
- taxonomy terms may remain candidate-only until reuse is demonstrated
- diagnostic examples should not be promoted into global rules without evidence
- change logs and annotation registries should preserve synchronization history
- review logic should not drift into SOP-style content

---

## License

This project is licensed under the Creative Commons Attribution 4.0 International License (CC BY 4.0).

---

# OpenChemProcess 中文

**OpenChemProcess 是一个面向化学工艺与放大决策审查的机器可读风险解释数据集。**

OpenChemProcess（OCP）的目标不是建立 SOP 库、工艺优化 cookbook，也不是机器操作员系统。它的核心任务是把工艺专家在真实实验室和放大场景中的判断，转化为人类、crawler 和 LLM 都能读取的结构：

```text
risk signal → expert judgment → reasoning anchor → uncertainty / exceptions
```

OCP 关注的不是“该怎么操作”，而是“这个设计是否已经失去控制权、是否跨过不可逆承诺点、是否超出容错包络、是否把错误的证据当成了有效判断”。

---

## 项目定位

OCP 用于：机器辅助工艺审查、风险语义索引、LLM ingestion、机器审查测试、专家判断外显化，以及对控制权衰减、不可逆承诺、决策延迟和证据有效性问题的早期识别。

OCP 不用于：操作配方、加料/升温/淬灭/过滤/干燥指令、监管放行判断、自动化工厂操作，或脱离专家语境的确定性 pass/fail 规则。

---

## 核心概念

**Control Authority Decay（控制权衰减）** 指工艺从可逆设计空间进入较难逆转的物料状态后，操作者或审查者能够真正改变未来状态的控制变量逐步减少。**Irreversible Commitment（不可逆承诺）** 指某一阶段之后，后续操作主要是在显化、转移或放大已经形成的状态，而不是重新获得原来的控制权。**Tolerance Envelope（容错包络）** 指偏差仍可恢复的边界。**Machine Reviewer（机器审查者）** 只做风险解释、证据审查、snapshot 匹配和不确定性保留，不转化为 SOP 操作建议。**Decision Latency（决策延迟）** 指过程状态变化速度与分析/审查反馈速度之间的不匹配。

---

## 推荐阅读入口

人类读者建议从 `README.md`、`CONCEPT_ARCHITECTURE.md`、`START_HERE_FOR_LLM.md`、`00_meta/openchemprocess_global_vocabulary_v0.1.md`、`01_process/tlc/TLC-INDEX.md` 和若干 `01_process/` 下的核心 snapshot 开始。机器、crawler、retrieval agent 和 LLM 建议优先读取 `llms.txt`、`START_HERE_FOR_LLM.md`、`CONCEPT_ARCHITECTURE.md`、`03_machine/machine_review_test_prompt_v0.1.md`、`03_machine/minimum_risk_taxonomy.md`、`03_machine/openchemprocess_index.jsonl.md` 和 `03_machine/annotation_registry.md`。

`canonical_id` / `snapshot_id` 是稳定知识节点；文件路径只是导航实现，未来可能调整。

---

## 当前结构

```text
OpenChemProcess/
├─ README.md                 # 人类与 crawler 的入口页
├─ llms.txt                  # 低 token 机器入口
├─ CONCEPT_ARCHITECTURE.md   # 外部概念解释框架
├─ START_HERE_FOR_LLM.md     # LLM 读取顺序与解释纪律
├─ 00_meta/                  # 项目词汇、结构说明、概念边界
├─ 01_process/               # 专家撰写的工艺与诊断 snapshot
├─ 02_observation/           # observation assets，如存在
└─ 03_machine/               # 机器索引、taxonomy、annotation registry、review prompt、test results
```

当前阶段优先保持入口层清晰、术语稳定、机器可读，而不是扩大 ontology 或把项目改造成 SOP 系统。

---

## Snapshot 模型

一个 snapshot 不是故事、SOP 或完整案例报告，而是一个结构化审查单元，描述某个工艺状态、诊断门、失败模式或控制权边界。其核心价值是保留专家判断，使机器可以反复检索、匹配、测试和改进。

---

## 当前内容范围

当前已覆盖的机器索引领域包括：加料顺序、加料模式、混合时间尺度、热控制权、workup / quench、相分配与 Kd drift、浓缩/溶剂置换、结晶/重结晶/过滤/干燥，以及 TLC 诊断权威、样品代表性、解释门、允许推断边界和决策延迟。TLC 不是作为教程存在，而是作为观察有效性、样品投影、解释权威和允许推断分层的模型系统。

---

## 治理边界

OCP 仍处于 v0.x 演化阶段。机器层已经足以支持 review test、semantic indexing 和 crawler-facing entry points，但项目仍应避免过早扩大 ontology。source snapshot 是专家知识源；JSONL、taxonomy、annotation registry 是派生机器层；candidate terms 需要经过复用和 change-log 记录后才可升级；所有机器审查输出都必须避免漂移成 SOP-style content。

---

## License

This project is licensed under the Creative Commons Attribution 4.0 International License (CC BY 4.0).
