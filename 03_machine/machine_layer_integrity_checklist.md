# Machine Layer Integrity Checklist

status: working checklist  
scope: lightweight manual consistency check for OpenChemProcess machine layer  
version: v0.1  

schema 已经规定 JSONL 机器导出文件必须一行一个完整 JSON object，维护态 `.jsonl.md` 可以含 Markdown，但 machine-use export `.jsonl` 不应含 headings、comments、code fences；同时 JSONL structured field content 应使用 English-only，zh/en 文件通过 `languages` 和 `source_paths` 记录。

## 3.1 每次新增或修改 annotation 后的人工检查

|检查项|最小通过标准|
|---|---|
|JSONL 合法性|导出的 `openchemprocess_index.jsonl` 每行可被 JSON parser 读取；`.jsonl.md` 维护文件可以有 Markdown，但导出文件不能有 heading、comment、code fence|
|canonical_id 唯一性|每个 `canonical_id` 只出现一次；中英文版本不能各自生成一条 JSONL|
|registry 覆盖|`annotation_registry.md` 中每个 completed / added 的 canonical_id 都必须在 JSONL 中出现；JSONL 中每个 canonical_id 也必须在 registry 中有一行|
|source_paths 完整性|每条 JSONL 必须有 `source_paths.zh` 和 `source_paths.en`；路径后缀应分别为 `.zh.md` 和 `.en.md`|
|languages 一致性|`languages` 应包含 `["zh","en"]`，除非该 snapshot 明确只有单语言且在 registry notes 中说明|
|schema_version 一致性|当前 6 个条目应为 `risk_annotation_schema_v0.2`；若出现不同版本，必须在 `machine_change_log.md` 说明原因|
|structured fields 英文|`core_judgment`、`risk_signals`、`reasoning_anchors`、`machine_use`、`process_stage`、`transition_model` 应为英文机器字段；中文解释留在 source snapshot 或说明文件|
|reasoning_anchors 来源| 每个 JSONL reasoning_anchor 必须能在 `minimum_risk_taxonomy.md` 的 Formal Reasoning Anchors、Candidate Terms、或 Taxonomy Delta introduced / reused terms 中 exact match 找到；JSONL 本身不能作为 anchor 合法性的自证来源。|
|non-canonical term 扫描|检查是否出现未登记、截断或非 exact 的术语表达，例如 `loss_amplification`、standalone `control_authority`、`control-authority loss`、`drying rescue failure` 等；合法 exact anchors 如 `control_authority_decay`、`misallocated_control_authority` 不应被误判。若确需新增术语，先进入 taxonomy delta，不直接混入 JSONL。|
|code fence 闭合|原始 snapshot 末尾 Machine Annotation 区块如果使用 fenced code block，必须首尾闭合；不得吞掉后续正文|
|candidate term 来源|新增 candidate term 必须能追溯到具体 source snapshot 和 change log 记录；不能只因模型测试输出而进入 taxonomy|
|risk signal exactness|JSONL 中 risk signal 尽量复用 taxonomy delta 或 source annotation 原句；同义改写要避免，例如不要把 `residual solvent curve reaches plateau` 改成 `solvent plateau problem`|
|QA 输出污染边界|robustness test 输出中的 inferred / partially supported signals、nearest canonical replacements、conceptual alignments、review-domain matches 不得反向写入 JSONL risk_signals 或 reasoning_anchors；除非 source snapshot 明确支持且 change log 记录，否则不能进入 taxonomy delta|
|review-domain 与 risk-positive 分离|测试结果和 reviewer 输出必须区分“属于哪个 snapshot 的审核范围”与“风险是否正向成立”；false-positive case 可以有 review-domain match，但 `Risk-positive conclusion` 应独立为 no / uncertain|
|section placement discipline|matched risk signals、inferred / partially supported signals、reasoning anchors、canonical correction / nearest allowed terms 必须分区；reasoning anchor 不能作为 risk signal，nearest canonical replacement 不能作为 positive anchor|
|reviewer-output audit handling|当输入是另一个 reviewer 的回答而非 process scenario 时，只做术语合规、evidence sufficiency 和 no-action leakage 审核；不得在没有底层过程证据时列出 positive risk signals 或 positive reasoning anchors|
|threshold 语义|soft review、hard block、watch zone、candidate trigger 不得混写；特别是 CF、WMR、ΔKd 不应全部变成 deterministic rejection|
|registry 状态同步|`annotation_status`、`jsonl_status`、`taxonomy_status`、`last_change_type`、`last_updated` 必须与实际修改一致|
|change log 同步|新增 annotation、taxonomy term、schema_version 变化、JSONL 结构变化都必须有一条简短 change log|
|no-action language|Machine Annotation 与 JSONL 的 `machine_use` 应保持 review 语言，不写 SOP-like 操作建议|

## 3.2 当前已暴露的重点污染词

先列为 watchlist，不必建复杂系统：

```
loss_amplification          -> 非 exact；当前 exact candidate term 是 loss_amplification_interface
control_authority           -> 非 exact standalone anchor；当前 formal anchor 是 control_authority_decay，另有 misallocated_control_authority
control-authority loss      -> 非登记表达
drying rescue failure       -> 非登记表达
near_dryness_risk           -> 非登记表达
WMR_failure                 -> 非登记表达
third_phase_loss            -> 非登记表达
interface_loss              -> 非登记表达
composition_drift_risk      -> 非登记表达
bound_solvent_plateau       -> 非登记表达
rolling_risk                -> 非登记表达
```

## 3.3 最小执行节奏

1️⃣ 每新增 1 个 snapshot annotation：先更新 source snapshot 末尾 Machine Annotation，再更新 JSONL，再更新 taxonomy delta/registry/change log；最后用 checklist 做一次人工检查。  
2️⃣ 每完成 3–5 个 annotation：运行一次 10–12 个 robustness test 的子集，重点看 non-canonical term、action leakage、threshold misuse。  
3️⃣ 每发现模型反复创造同一术语：不要立刻收录，先写入 change log 或 Vocabulary watchlist；只有当它确实对应稳定概念且有 source snapshot 支撑，再进入 taxonomy delta。