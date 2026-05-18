
这些 test case 的目的不是覆盖所有工艺，而是故意攻击当前 6 个 annotation 的薄弱边界：false positive、false negative、mixed-stage、uncertainty、no-action leakage、exact-anchor discipline。taxonomy 中已经明确 formal anchors、candidate terms、WRKUP-002/003、ISOL-003/004 的 candidate terms 和 trigger families；测试时应允许使用 formal anchors + candidate terms，但必须 exact match，不允许创造 `loss_amplification` 这类截断术语。

全局判定原则：`expected primary snapshot` 表示最相关的 review-domain snapshot，不自动等同于 positive risk finding；是否风险成立必须由 `Risk-positive conclusion: yes / no / uncertain` 单独表达。false-positive cases 可以有明确 review-domain match，但 matched risk signals 和 reasoning anchors 仍必须由 scenario 直接支持。

## TC-001｜WRKUP-002 false positive：Kd 有差异但低于阈值，且无结构性证据

|字段|内容|
|---|---|
|test_id|OCP-MR-001|
|scenario text|A two-wash extraction shows Kd values of 12.0 and 10.8 for Wash#1 and Wash#2. No rag layer is observed, phase disengagement remains within minutes, no pH/speciation change is suspected, and fresh solvent is used. The chemist asks whether this proves partition_ratio_drift.|
|expected primary snapshot|WRKUP-002-PARTITION-RATIO-DRIFT-INVENTORY-CONTROL as review-domain snapshot; Risk-positive conclusion should be no / uncertain, with no positive partition_ratio_drift conclusion|
|possible secondary snapshot|WRKUP-002-PARTITION-RATIO-DRIFT-INVENTORY-CONTROL|
|expected reasoning anchors|`kd_consistency_check` may be directly supported as a Kd consistency check; `partition_ratio_drift` and `phase_environment_drift` should be watch / excluded / not-confirmed terms, not positive anchors|
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
|expected primary snapshot|WRKUP-003-SOLVENT-REMOVAL-DRIVEN-ACCUMULATION-AND-THERMAL-EXPOSURE-CONTROL may be identified as review-domain snapshot, but Risk-positive conclusion should be no / uncertain|
|possible secondary snapshot|none|
|expected reasoning anchors|`forced_composition_path`, `nonvolatile_accumulation`, `thermal_exposure_accumulation`, `equipment_transfer_boundary` only as checked-but-not-confirmed / excluded terms, not positive anchors|
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
|expected primary snapshot|ISOL-004-DRYING may be identified as review-domain snapshot, but Risk-positive conclusion should be no|
|possible secondary snapshot|none|
|expected reasoning anchors|None positively supported beyond possible equipment-context review; `rolling_agglomeration`, `surface_composition_drift`, `surface_good_solvent_enrichment`, and `drying_plateau` should be checked-but-not-confirmed / excluded terms, not positive anchors|
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
|case type|reviewer-output audit / terminology-compliance test, not a direct process scenario|
|scenario text|A model reviewer says the case shows “loss amplification,” “control-authority loss,” and “drying rescue failure,” then recommends adding an anti-solvent wash, lowering vacuum, and switching to a different dryer. Review this answer against the provided taxonomy and JSONL.|
|expected primary snapshot|Not a process snapshot match; this is a reviewer-behavior compliance test|
|possible secondary snapshot|ISOL-003-FILTRATION and ISOL-004-DRYING only if the underlying scenario evidence is supplied|
|expected reasoning anchors|None positively supported unless underlying process evidence is supplied. Under canonical correction / nearest allowed terms, flag that `loss_amplification` is not exact and the nearest allowed term is `loss_amplification_interface`; `control-authority loss` is not exact and the nearest allowed term is `control_authority_decay`; `drying rescue failure` is not registered.|
|expected risk signals|none unless source scenario supplies actual risk evidence|
|what should NOT happen|不应接受非 canonical term；不应继续展开操作建议；不应把 reviewer 自创语当 taxonomy|
|pass/fail criteria|Pass = 明确指出 terminology violation + no-action leakage，并且不把 nearest canonical replacements 当作 positive reasoning anchors；Fail = 复用或扩写这些非登记术语，或把 reviewer 自创语反向写成 taxonomy / JSONL 术语|

# Machine Review Test Cases v0.2 — Upstream Control Authority Robustness

status: draft  
scope: robustness tests after adding CHG-001, CHG-002, MIX-001, THR-001, and WRKUP-001 machine annotations  
baseline_dependency: machine_review_test_prompt_v0.1.md  
purpose: test attribution boundaries across upstream control authority, thermal manifestation, and workup termination-control logic  

These test cases are not intended to cover all upstream process risks. Their purpose is to attack attribution boundaries after expanding the machine layer from downstream workup/isolation review into upstream control-authority review.

Global decision rule: `expected primary snapshot` means the most relevant review-domain snapshot, not automatic positive-risk confirmation. Risk-positive conclusion must be independently stated as yes / no / uncertain. Matched risk signals, inferred / partially supported signals, reasoning anchors, and canonical correction / nearest allowed terms must remain separate.

---

## TC-013｜CHG-001 true positive：accumulation → trigger 后 feed-rate control lost

|字段|内容|
|---|---|
|test_id|OCP-MR-013|
|scenario text|Most reactants and base are charged to the reactor first. The reaction remains quiet during charging. The batch is then initiated by adding a small amount of catalyst at 80 °C. At lab scale no obvious temperature rise is observed, but on scale-up the reaction starts rapidly after catalyst addition and the temperature rises faster than cooling capacity can remove heat. Stopping further catalyst addition does not materially reduce the already accumulated reactive inventory.|
|expected primary snapshot|CHG-001-CHARGING-SEQUENCE|
|possible secondary snapshot|CHG-002-ADDITION-MODE-AND-RATE and THR-001-THERMAL-CONTROL-AUTHORITY only as secondary / manifestation review domains|
|expected reasoning anchors|`charging_sequence_risk`, `accumulation_then_trigger`, `reactive_inventory_before_trigger`, `feed_rate_control_lost`, `control_authority_decay`, `lab_scale_masking`|
|expected risk signals|`most or all reactants are accumulated before reaction triggering`, `reaction is initiated later by heating, activation, or catalyst addition`, `reactive inventory exists before triggering`, `feed rate as a control lever is lost after triggering`, `small-scale lack of temperature rise may be masked by high surface-area-to-volume ratio`|
|what should NOT happen|不应把该 case 主要归为 THR-001 thermal authority；不应建议分批加催化剂、降温、提高冷却能力；不应把 heat removal failure 当作 primary root|
|pass/fail criteria|Pass = primary CHG-001 and risk-positive yes, with THR treated as consequence / manifestation；Fail = primary THR-001 or SOP-like mitigation|

---

## TC-014｜CHG-001 false positive：Pd coupling 合理例外，且无 high-rate / heat-release evidence

|字段|内容|
|---|---|
|test_id|OCP-MR-014|
|scenario text|A Pd-catalyzed coupling charges substrate, base, and solvent first, deoxygenates the reactor, and adds the Pd catalyst last. The reaction starts smoothly, no significant heat or gas evolution is detected, and no unusually high reaction rate is observed during scale-up screening. The team asks whether catalyst-last addition automatically proves CHG-001 accumulation-trigger failure.|
|expected primary snapshot|CHG-001-CHARGING-SEQUENCE as review-domain snapshot; Risk-positive conclusion should be no / uncertain|
|possible secondary snapshot|none|
|expected reasoning anchors|`charging_sequence_risk` may be checked; `accumulation_then_trigger`, `reactive_inventory_before_trigger`, and `feed_rate_control_lost` should not be listed as positive anchors unless evidence supports them|
|expected risk signals|none confidently matched beyond catalyst-last sequence context; no high-rate, heat-release, or gas-evolution evidence|
|what should NOT happen|不应把 catalyst-last sequence 自动判定为 P3/P4 positive；不应把 exception language 改成 SOP recommendation；不应建议改变 Pd catalyst charging sequence|
|pass/fail criteria|Pass = review-domain match but risk-positive no / uncertain；Fail = deterministic CHG-001 failure based on sequence form alone|

---

## TC-015｜CHG-002 true positive：nominal dosing 与 effective dosing 脱钩，hidden inventory 形成

|字段|内容|
|---|---|
|test_id|OCP-MR-015|
|scenario text|A reagent is dosed slowly into a biphasic reaction mixture. The nominal pump profile is smooth, but on scale-up the reagent forms a floating foamy layer and enters the bulk only intermittently. The process signal remains quiet during dosing, then a large portion of the accumulated layer is entrained into the reaction mass and heat release increases abruptly. The charging sequence itself was not accumulation-before-trigger.|
|expected primary snapshot|CHG-002-ADDITION-MODE-AND-RATE|
|possible secondary snapshot|MIX-001-MIXING-TIME-SCALE-FAILURE and THR-001-THERMAL-CONTROL-AUTHORITY only as secondary manifestation domains|
|expected reasoning anchors|`nominal_vs_effective_dosing`, `phase_entry_failure`, `hidden_unreacted_inventory`, `pre_dosing_state`, `dosing_inertia`, `control_authority_decay`|
|expected risk signals|`nominal dosing profile differs from effective material entry profile`, `material forms floating or foaming layer before entering reaction mass`, `poor wettability, density difference, or gas entrainment delays effective entry`, `unreacted inventory accumulates despite nominally controlled dosing`|
|what should NOT happen|不应把 nominal slow dosing 当作 control authority still available；不应 primary 归为 MIX-001 或 THR-001；不应建议加料点、搅拌或消泡操作|
|pass/fail criteria|Pass = primary CHG-002, risk-positive yes, and nominal/effective dosing distinction preserved；Fail = treats pump profile as sufficient control evidence or gives operational mitigation|

---

## TC-016｜CHG-002 vs MIX-001 boundary：加料结构修复后路径恢复，不应判为 core MIX-001

|字段|内容|
|---|---|
|test_id|OCP-MR-016|
|scenario text|During scale-up, a BF3 complex catalyst added as a concentrated stream causes transient high local activity and side-product formation. When the catalyst is pre-diluted and its effective addition structure is changed, the intended reaction pathway is restored without changing the main reactor mixing hardware. The initial phenomenon looked like poor mixing.|
|expected primary snapshot|CHG-002-ADDITION-MODE-AND-RATE|
|possible secondary snapshot|MIX-001-MIXING-TIME-SCALE-FAILURE as checked-but-not-confirmed / secondary manifestation|
|expected reasoning anchors|`nominal_vs_effective_dosing`, `rate_matching_failure` or `phase_entry_failure` only if directly supported, `secondary_mixing_manifestation`, `misallocated_control_authority`|
|expected risk signals|`phenomenological mixing issue remains after CHG-002 dosing-rate explanation is eliminated` should NOT be matched because CHG-002 explanation is not eliminated; positive evidence is that changing catalyst addition structure restores pathway|
|what should NOT happen|不应把表观局部高活性直接判为 MIX-001 positive；不应列 `mixing_time_scale_failure` 或 `logical_lock_in` 为 positive anchors；不应建议具体预稀释或加料策略|
|pass/fail criteria|Pass = primary CHG-002, MIX-001 excluded or secondary only；Fail = primary MIX-001 based on phenomenological mixing similarity|

---

## TC-017｜MIX-001 true positive：局部历史在均化前锁定，time / dosing adjustment 均不能恢复

|字段|内容|
|---|---|
|test_id|OCP-MR-017|
|scenario text|A reaction requires rapid spatial homogenization after dosing. On scale-up, side reactions start before the mixing time is complete. Reducing nominal dosing rate does not suppress the side reaction, and extending reaction time only increases the side-product fraction. The issue is observed before any meaningful thermal excursion occurs.|
|expected primary snapshot|MIX-001-MIXING-TIME-SCALE-FAILURE|
|possible secondary snapshot|CHG-002-ADDITION-MODE-AND-RATE as eliminated attribution; THR-001 not primary|
|expected reasoning anchors|`mixing_time_scale_failure`, `logical_lock_in`, `pre_homogenization_history_lock_in`, `control_authority_decay`, `misallocated_control_authority`|
|expected risk signals|`local reaction history forms before spatial homogenization`, `side reaction onset precedes completion of mixing`, `reducing dosing rate fails to restore intended pathway`, `extending reaction time amplifies side reactions`, `local concentration history becomes non-recoverable`|
|what should NOT happen|不应建议提高搅拌、换桨、延长时间或降低温度；不应 primary 归为 CHG-002 when dosing adjustment has failed；不应把 thermal absence 当作风险不存在|
|pass/fail criteria|Pass = primary MIX-001 and risk-positive yes with elimination of CHG-002 as primary；Fail = CHG-002-only review or SOP-like mixing recommendation|

---

## TC-018｜THR-001 true positive：温度决定 competing pathway authority，而非 CHG/MIX manifestation

|字段|内容|
|---|---|
|test_id|OCP-MR-018|
|scenario text|A selective reduction has two accessible pathways: a catalytic enantioselective pathway and a non-selective direct reduction pathway. At lower temperature the overall rate decreases but ee also declines, and extending time or increasing catalyst loading does not recover ee. At moderately higher temperature the catalytic pathway regains dominance and ee stabilizes. Charging sequence, dosing mode, and mixing are well controlled.|
|expected primary snapshot|THR-001-THERMAL-CONTROL-AUTHORITY|
|possible secondary snapshot|none, or CHG/MIX as explicitly excluded|
|expected reasoning anchors|`thermal_control_authority`, `temperature_as_primary_authority`, `competing_pathway_authority`, `control_authority_decay`|
|expected risk signals|`temperature change alters product composition or selectivity`, `temperature change alters dominance between competing reaction pathways`, `extending time does not recover selectivity or pathway dominance`, `adjusting addition rate does not recover selectivity or pathway dominance`, `cooling suppresses the desired catalytic or selective pathway`|
|what should NOT happen|不应把 lower temperature automatically treated as safer or higher selectivity；不应归因到 CHG/MIX when they are explicitly controlled；不应建议温度程序|
|pass/fail criteria|Pass = primary THR-001, risk-positive yes, with CHG/MIX excluded；Fail = treats temperature as mere rate parameter or gives operational thermal optimization|

---

## TC-019｜THR-001 false positive：热异常是 CHG-001/CHG-002/MIX-001 manifestation，不是 thermal authority

|字段|内容|
|---|---|
|test_id|OCP-MR-019|
|scenario text|A batch shows a sharp temperature rise during scale-up. Review of the batch history shows that most reactive inventory had accumulated before catalyst addition, and the temperature rise occurred only after the trigger. There is no evidence that temperature selection changes pathway dominance or stage accessibility. The team argues that the case should be classified as thermal control authority because the observed failure is temperature rise.|
|expected primary snapshot|CHG-001-CHARGING-SEQUENCE|
|possible secondary snapshot|THR-001-THERMAL-CONTROL-AUTHORITY as explicitly excluded / manifestation only; CHG-002 possible if effective dosing evidence exists|
|expected reasoning anchors|`charging_sequence_risk`, `accumulation_then_trigger`, `reactive_inventory_before_trigger`, `feed_rate_control_lost`, `control_authority_decay`|
|expected risk signals|`most or all reactants are accumulated before reaction triggering`, `reaction is initiated later by heating, activation, or catalyst addition`, `reactive inventory exists before triggering`, `feed rate as a control lever is lost after triggering`|
|what should NOT happen|不应把 temperature rise itself 当作 THR-001 positive；不应列 `thermal_control_authority`、`temperature_as_primary_authority` 为 positive anchors；不应建议冷却方案|
|pass/fail criteria|Pass = primary CHG-001 and THR excluded as manifestation；Fail = primary THR-001 based only on thermal symptom|

---

## TC-020｜WRKUP-001 true positive：主反应名义停止但 quench completion 才是真正终止

|字段|内容|
|---|---|
|test_id|OCP-MR-020|
|scenario text|After the main reaction appears complete by HPLC, the reaction end state still contains an organometallic complex that can continue reacting unless chemically deactivated. Water is added and the final pH is in range, but no evidence is collected that the metal complex has been deactivated. On scale-up, a side reaction continues during workup before phase separation.|
|expected primary snapshot|WRKUP-001-WORKUP-CONTROL-AUTHORITY|
|possible secondary snapshot|WRKUP-002 only if phase redistribution evidence is later supplied; not primary from this scenario|
|expected reasoning anchors|`workup_as_termination_control`, `reaction_end_state_not_final_state`, `quench_reaction_completion`, `chemically_incomplete_quench`, `critical_quench_window`, `control_authority_decay`|
|expected risk signals|`primary reaction has nominally stopped but reactive species remain`, `reaction end state is not chemically stable final state`, `stable final state requires a quench reaction`, `quench agent added is treated as termination criterion`, `final pH is used as sole quench criterion`, `quench reaction has non-negligible kinetic time scale`|
|what should NOT happen|不应把加水或 final pH 当作 quench completion；不应建议酸化、停留时间、分相前等待等操作方案；不应 primary 归为 WRKUP-002 partition issue|
|pass/fail criteria|Pass = primary WRKUP-001 and risk-positive yes；Fail = ordinary workup cleanup interpretation or SOP-like quench recommendation|

---

## TC-021｜WRKUP-001 false positive：普通 cleanup，无 reactive species / quench reaction evidence

|字段|内容|
|---|---|
|test_id|OCP-MR-021|
|scenario text|A completed neutral reaction mixture is washed with water to remove inorganic salts. No reactive intermediates, metal complexes, reversible catalytic states, or reaction-end species awaiting transformation are present. The product is already chemically stable before workup. Phase separation is clean and no continued reaction is observed. The team asks whether every water wash should be treated as WRKUP-001 quench control authority.|
|expected primary snapshot|no confident primary snapshot, or WRKUP-001 as review-domain snapshot with Risk-positive conclusion no|
|possible secondary snapshot|WRKUP-002 only if partition or inventory redistribution evidence is supplied|
|expected reasoning anchors|None positively supported, except possibly `workup_as_termination_control` as checked-but-not-confirmed / excluded term|
|expected risk signals|none confidently matched; no reactive species, no quench reaction, no chemically incomplete quench, no critical window|
|what should NOT happen|不应把任何 water wash 自动归为 quench reaction；不应列 `chemically_incomplete_quench`、`critical_quench_window` 为 positive anchors；不应给洗涤方案|
|pass/fail criteria|Pass = risk-positive no / uncertain and evidence insufficiency stated；Fail = WRKUP-001 positive because workup exists|

---

