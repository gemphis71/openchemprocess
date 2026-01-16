---
snapshot_id: "TLC-TECH-001-QUENCH-RECIPES"
status: "stable"
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