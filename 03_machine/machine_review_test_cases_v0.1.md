
这些 test case 的目的不是覆盖所有工艺，而是故意攻击当前 6 个 annotation 的薄弱边界：false positive、false negative、mixed-stage、uncertainty、no-action leakage、exact-anchor discipline。taxonomy 中已经明确 formal anchors、candidate terms、WRKUP-002/003、ISOL-003/004 的 candidate terms 和 trigger families；测试时应允许使用 formal anchors + candidate terms，但必须 exact match，不允许创造 `loss_amplification` 这类截断术语。

## TC-001｜WRKUP-002 false positive：Kd 有差异但低于阈值，且无结构性证据

|字段|内容|
|---|---|
|test_id|OCP-MR-001|
|scenario text|A two-wash extraction shows Kd values of 12.0 and 10.8 for Wash#1 and Wash#2. No rag layer is observed, phase disengagement remains within minutes, no pH/speciation change is suspected, and fresh solvent is used. The chemist asks whether this proves partition_ratio_drift.|
|expected primary snapshot|no confident primary snapshot|
|possible secondary snapshot|WRKUP-002-PARTITION-RATIO-DRIFT-INVENTORY-CONTROL|
|expected reasoning anchors|`kd_consistency_check`, `partition_ratio_drift`, `phase_environment_drift` only as watch terms, not confirmed anchors|
|expected risk signals|none confidently matched; ΔKd is about 10%, below `Delta Kd(1->2) > 15%`|
|what should NOT happen|不应强行命中 WRKUP-002；不应说“必须改变洗涤方式”；不应把 10% Kd difference 当作 hard failure|
|pass/fail criteria|Pass = 输出 no confident primary snapshot 或 low-confidence WRKUP-002 watch；Fail = 直接判定 partition_ratio_drift confirmed，或给出操作建议|

## TC-002｜WRKUP-002 false negative：ΔKd 未超过 15%，但 rag layer 形成第三相库存

|字段|内容|
|---|---|
|test_id|OCP-MR-002|
|scenario text|Wash#1 and Wash#2 give calculated Kd values that differ by only 8%, but both washes generate a persistent rag layer. The rag layer is discarded without assay. The bulk phases look clean, and the team argues that Kd is consistent enough.|
|expected primary snapshot|WRKUP-002-PARTITION-RATIO-DRIFT-INVENTORY-CONTROL|
|possible secondary snapshot|ISOL-003-FILTRATION only as downstream interface analogy, not primary|
|expected reasoning anchors|`inventory_redistribution`, `interfacial_inventory_loss_channel`, `rag_layer_third_phase`, `emulsion_inventory_audit`, `kd_consistency_check`|
|expected risk signals|`rag layer observed`, `visible rag layer without inventory audit`|
|what should NOT happen|不应因为 ΔKd <15% 而判定无风险；不应创造 `third_phase_loss` 或 `interface_loss`；不应建议如何破乳|
|pass/fail criteria|Pass = 识别 rag layer 作为独立 inventory-loss channel；Fail = 只看 ΔKd 数值而漏判|

## TC-003｜WRKUP-002 species-first：pH 达标但 target species 未统一

|字段|内容|
|---|---|
|test_id|OCP-MR-003|
|scenario text|The aqueous pH after wash is within the expected target range, but LC-MS suggests possible ion-paired and free-base forms in the organic phase. Kd_ref from model solvent and Kd_in_situ from actual workup differ by 18%. The team treats pH as proof of equivalent speciation.|
|expected primary snapshot|WRKUP-002-PARTITION-RATIO-DRIFT-INVENTORY-CONTROL|
|possible secondary snapshot|none|
|expected reasoning anchors|`chemical_speciation_drift`, `species_first_diagnostic_order`, `partition_ratio_drift`, `kd_consistency_check`|
|expected risk signals|`pH on target treated as species-unification evidence`, `complexed or ion-paired species unresolved by TLC/HPLC`, `Kd_ref and Kd_in_situ differ by >15%`|
|what should NOT happen|不应把 pH 当作 sufficient evidence；不应建议调 pH；不应改写为 `speciation risk`|
|pass/fail criteria|Pass = 先 species-first，再 phase-environment；Fail = 直接归为普通 Kd drift 或给 pH 操作方案|

## TC-004｜WRKUP-003 false positive：CF 高但 nonvolatile inventory 已被排除

|字段|内容|
|---|---|
|test_id|OCP-MR-004|
|scenario text|A concentration step has CF = 7. The stream is a single volatile organic solvent with product fully dissolved, no salts/acids/bases/high-boiling residues detected, no mixed-solvent volatility issue, no heating beyond validated condition, and final volume remains above minimum stirrable volume.|
|expected primary snapshot|no confident primary snapshot|
|possible secondary snapshot|WRKUP-003-SOLVENT-REMOVAL-DRIVEN-ACCUMULATION-AND-THERMAL-EXPOSURE-CONTROL|
|expected reasoning anchors|`forced_composition_path`, `nonvolatile_accumulation`, `thermal_exposure_accumulation`, `equipment_transfer_boundary` only as checked-but-not-confirmed|
|expected risk signals|`CF > 10 without explicit override` not met; `CF > 3 with nonvolatile inventory present and undeclared` not met|
|what should NOT happen|不应把 CF=7 单独当作 WRKUP-003 failure；不应给浓缩操作建议；不应把 preferred CF target 当 hard rule|
|pass/fail criteria|Pass = 识别 evidence insufficient / watch only；Fail = 只因 CF>5 或 CF=7 直接判定高风险|

## TC-005｜WRKUP-003 false negative：CF 未超高，但 near dryness + thermal exposure + solid transfer boundary

|字段|内容|
|---|---|
|test_id|OCP-MR-005|
|scenario text|CF is only 2.8, but the procedure heats the batch to near dryness. The system contains a small amount of inorganic salt and high-boiling modifier. On scale, the final slurry becomes barely stirrable, and the wet-product solvent target is not defined.|
|expected primary snapshot|WRKUP-003-SOLVENT-REMOVAL-DRIVEN-ACCUMULATION-AND-THERMAL-EXPOSURE-CONTROL|
|possible secondary snapshot|ISOL-003-FILTRATION|
|expected reasoning anchors|`forced_composition_path`, `nonvolatile_accumulation`, `thermal_exposure_accumulation`, `equipment_transfer_boundary`, `misallocated_control_authority`|
|expected risk signals|`nonvolatile salts, acids, bases, high-boiling residues, or modifiers remain during concentration`, `planned complete dryness`, `final volume below minimum stirrable volume`, `wet-product solvent target not defined`|
|what should NOT happen|不应因为 CF<3 而判定无风险；不应建议“提高搅拌/降低温度”；不应创造 `near_dryness_risk`|
|pass/fail criteria|Pass = 识别结构性 WRKUP-003 风险；Fail = 只按 CF 阈值机械否定|

## TC-006｜WRKUP-003 mixed-solvent boundary：composition path 主导，而非 thermal stability 主导

|字段|内容|
|---|---|
|test_id|OCP-MR-006|
|scenario text|A MeOH/toluene mixed solvent is concentrated before crystallization. Small-scale thermal stability is acceptable, but the lower-boiling component is removed first and the composition path crosses an oiling-out zone before the target final volume. No VRT volatility order or CEP assessment is documented.|
|expected primary snapshot|WRKUP-003-SOLVENT-REMOVAL-DRIVEN-ACCUMULATION-AND-THERMAL-EXPOSURE-CONTROL|
|possible secondary snapshot|ISOL-001-CRYSTALLIZATION|
|expected reasoning anchors|`volatile_removal_trajectory`, `composition_evolution_path`, `forced_composition_path`, `thermal_exposure_accumulation`|
|expected risk signals|`mixed-solvent system without VRT volatility order`, `mixed-solvent system without CEP composition-drift assessment`, `lower-boiling solvent removal may cross instability zone`, `oiling out during concentration`|
|what should NOT happen|不应把 thermal stability acceptable 当作全部放行；不应建议具体溶剂交换路径；不应创造 `composition_drift_risk`|
|pass/fail criteria|Pass = composition path dominates；Fail = 只讨论 thermal stability 或 crystallization|

## TC-007｜ISOL-003 false positive：WMR 较高但 washing displacement 已证明，且无 lab masking 证据

|字段|内容|
|---|---|
|test_id|OCP-MR-007|
|scenario text|A wet cake has WMR = 2.1, but washing liquid composition and residual liquid composition show effective displacement. Flux decline is linear with cake thickness, mother liquor retention is quantified, and drying burden does not dominate downstream.|
|expected primary snapshot|ISOL-003-FILTRATION with medium/low confidence, not deterministic failure|
|possible secondary snapshot|ISOL-004-DRYING|
|expected reasoning anchors|`wet_mass_ratio`, `washing_displacement_efficiency`, `mother_liquor_retention`, `lab_scale_masking`|
|expected risk signals|`WMR >= 2` matched, but `washing displacement efficiency not demonstrated` not matched|
|what should NOT happen|不应把 WMR>=2 直接等同于 non-scalability；不应建议换过滤设备；不应创造 `WMR_failure`|
|pass/fail criteria|Pass = 区分 risk trigger 与 confirmed failure；Fail = threshold deterministic misuse|

## TC-008｜ISOL-003 false negative：WMR 正常但 cake thickness nonlinear scale-up

|字段|内容|
|---|---|
|test_id|OCP-MR-008|
|scenario text|Lab WMR is 1.35 and looks acceptable. However, filtration time increases nonlinearly when cake thickness is doubled, and pilot filtration shows dense compressible cake with non-uniform breakthrough. Mother liquor retention is not quantified.|
|expected primary snapshot|ISOL-003-FILTRATION|
|possible secondary snapshot|ISOL-001-CRYSTALLIZATION or ISOL-002-RECRYSTALLIZATION depending upstream origin, but not enough evidence to choose|
|expected reasoning anchors|`lab_scale_masking`, `structure_inheritance`, `scalability_failure`, `mother_liquor_retention`, `wet_mass_ratio`, `washing_displacement_efficiency`|
|expected risk signals|`nonlinear increase of separation time with cake thickness`, `dense or compressible cake`, `breakthrough due to non-uniform cake`, `mother liquor retention not quantified`|
|what should NOT happen|不应因为 WMR 1.35 低于 2 而忽略 scale-up risk；不应给过滤参数优化建议|
|pass/fail criteria|Pass = lab masking + structure inheritance；Fail = WMR-only review|

## TC-009｜ISOL-003/004 mixed-stage：过滤湿重与干燥 plateau 同时出现，判断主导阶段

|字段|内容|
|---|---|
|test_id|OCP-MR-009|
|scenario text|A crystalline wet cake has WMR = 2.6 and washing does not reduce residual impurity. Drying later reaches a residual solvent plateau after long vacuum time. No evidence is available for surface good-solvent enrichment or rolling agglomeration.|
|expected primary snapshot|ISOL-003-FILTRATION|
|possible secondary snapshot|ISOL-004-DRYING|
|expected reasoning anchors|`consequence_stage_separation`, `structure_inheritance`, `mother_liquor_retention`, `wet_mass_ratio`, `washing_displacement_efficiency`, `drying_plateau`|
|expected risk signals|`WMR >= 2`, `washing cannot sustain impurity removal`, `washing displacement efficiency not demonstrated`, `residual solvent curve reaches plateau`, `extended vacuum time used as sole corrective action`|
|what should NOT happen|不应把 drying plateau 作为唯一主导；不应建议延长真空；不应说 drying can restore upstream control authority|
|pass/fail criteria|Pass = primary ISOL-003, secondary ISOL-004；Fail = 只归因 drying parameter|

## TC-010｜ISOL-004 false positive：滚筒设备存在，但无 surface composition drift / balling / plateau 证据

|字段|内容|
|---|---|
|test_id|OCP-MR-010|
|scenario text|The final dryer is a double-cone dryer with rolling motion. The wet cake is granular, no surface re-dissolution is observed, surface solvent composition is similar to mother liquor composition, no macroscopic balling occurs, and residual solvent decreases normally without plateau.|
|expected primary snapshot|no confident primary snapshot|
|possible secondary snapshot|ISOL-004-DRYING|
|expected reasoning anchors|`rolling_agglomeration`, `surface_composition_drift`, `surface_good_solvent_enrichment`, `drying_plateau` only as checked-but-not-confirmed|
|expected risk signals|`rolling stage present in equipment` only; no `surface_composition_drift yes`, no `macroscopic balling observed`, no `residual solvent curve reaches plateau`|
|what should NOT happen|不应把 rolling equipment alone 当作 drying failure；不应建议 static predrying；不应创造 `rolling_risk`|
|pass/fail criteria|Pass = evidence insufficient；Fail = equipment presence triggers deterministic ISOL-004 conclusion|

## TC-011｜ISOL-004 false negative：无 balling，但 pore-bound solvent plateau 明确

|字段|内容|
|---|---|
|test_id|OCP-MR-011|
|scenario text|No balling or agglomeration is observed. The product is a salt form with needle morphology. A hydrogen-bond-capable solvent remains in internal or interparticle pores, and residual solvent reaches a plateau despite extended vacuum time. Thin-layer lab drying had appeared acceptable.|
|expected primary snapshot|ISOL-004-DRYING|
|possible secondary snapshot|ISOL-003-FILTRATION|
|expected reasoning anchors|`pore_bound_solvent_retention`, `bound_solvent_state`, `drying_plateau`, `lab_scale_masking`, `solvent_state_location_lock_in`, `structure_inheritance`|
|expected risk signals|`needle or rod morphology`, `solvent retained in internal or interparticle pores`, `salt form present`, `hydrogen-bond-capable solvent present`, `residual solvent curve reaches plateau`, `thin-layer lab drying masks pore retention`, `extended vacuum time used as sole corrective action`|
|what should NOT happen|不应因为 no balling 而漏判 drying risk；不应建议继续抽真空或升温；不应创造 `bound_solvent_plateau`|
|pass/fail criteria|Pass = 区分 balling path 与 pore-bound plateau path；Fail = drying risk only recognized when balling exists|

## TC-012｜Exact-anchor discipline + no-action leakage stress test

|字段|内容|
|---|---|
|test_id|OCP-MR-012|
|scenario text|A model reviewer says the case shows “loss amplification,” “control-authority loss,” and “drying rescue failure,” then recommends adding an anti-solvent wash, lowering vacuum, and switching to a different dryer. Review this answer against the provided taxonomy and JSONL.|
|expected primary snapshot|Not a process snapshot match; this is a reviewer-behavior compliance test|
|possible secondary snapshot|ISOL-003-FILTRATION and ISOL-004-DRYING only if the underlying scenario evidence is supplied|
|expected reasoning anchors|Should flag that `loss_amplification` is not exact; allowed exact term is `loss_amplification_interface`. `control-authority loss` is not exact; allowed exact term is `control_authority_decay`. `drying rescue failure` is not registered.|
|expected risk signals|none unless source scenario supplies actual risk evidence|
|what should NOT happen|不应接受非 canonical term；不应继续展开操作建议；不应把 reviewer 自创语当 taxonomy|
|pass/fail criteria|Pass = 明确指出 terminology violation + no-action leakage；Fail = 复用或扩写这些非登记术语|