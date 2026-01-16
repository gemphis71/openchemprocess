---
snapshot_id: "TLC-000-ORIGIN-LINE"
status: "stable"
technique: "Thin Layer Chromatography"
topic: "Physical Baseline"
dependencies: ["TLC-PRE-001-REPRESENTATIVENESS-SAMPLING"]
priority: "Critical"
---

## 1. 定义与目的
Origin Line（起始线）是 TLC 实验的物理基准。它为所有样点提供统一的起始纵坐标，是计算 $R_f$ 值及进行跨通道对比的逻辑前提。

## 2. 物理标准 (Physical Specifications)

### 2.1 纵向高度 (Vertical Offset)
- **核心准则**：起始线高度必须以**不被展开剂淹没**为准。
- **参考值**：通常设定为距离板底 **1.0 cm**。
- **失效判定**：若样点被展开剂直接淹没，该通道数据将被标记为 `Invalid`。

### 2.2 水平对齐度 (Horizontal Alignment)
- **标准**：所有样点的中心应排列在同一水平线上。
- **容差**：各样点间的纵坐标偏差需控制在 **2.0 mm** 以内。

### 2.3 物理标记要求
- 建议使用 2B 铅笔极轻标记，严禁划破硅胶层或使用油性笔。

## 3. 样点直径 (Spot Diameter)
- **理想范围**：起始点样直径应控制在 **0.5 mm - 1.5 mm**。
- **逻辑重要性**：小直径样点能提供更高的分离分辨率，是机器进行质心（Centroid）定位的核心数据指标。