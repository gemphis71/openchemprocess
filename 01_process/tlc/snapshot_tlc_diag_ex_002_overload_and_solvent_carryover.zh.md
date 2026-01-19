---
snapshot_id: "TLC-DIAG-EX-002-OVERLOAD-AND-SOLVENT-CARRYOVER"
status: "stable"
technique: "Thin Layer Chromatography"
topic: "Non-interpretable plate due to spotting overload / high-boiling solvent carryover"
dependencies:
  - "TLC-PRE-002-SAMPLE-PREPARATION-GATE"
  - "TLC-002-SPOTTING-OPERATION"
  - "TLC-004-PLATE-VISUAL-OBSERVATION"
---

# TLC-DIAG-EX-002 点样过载与强极性溶剂残留：条带化导致的系统性失效

## 1. 视觉特征（Observation）

通过视觉化观察，该板呈现明显的物理失效形态：

- **纵向条带化（Streak / Smear）**：多个通道（Lane）呈现从基线向上连续拉长的宽大柱状信号，完全丧失收敛的“点形”结构。
- **边界湮灭**：信号边缘模糊且相互重叠，无法区分不同组分或杂质，板面缺乏可识别的迁移结构。
- **物理痕迹**：基线区域可见异常湿润或形变痕迹，提示点样区域存在未充分挥发的溶剂残留。

## 2. 判读结论与逻辑溯源（Diagnostic Status）

- **解释权状态**：**REVOKED（撤销） / 无法判读**  
- **失效类型**：**点样混杂干扰（Spotting Confounder）**

在本案例中，该失效可归因于以下点样相关因素的叠加：

- **高沸点强极性溶剂残留**：点样溶剂未充分干燥，在展开过程中显著扰动局部迁移行为，导致信号整体被拉伸为连续条带。
- **上样量过载**：单位面积内样品负载过高，超出硅胶表面可提供的有效吸附与分离能力，迁移过程中形成物理性涂抹。

## 3. 阻断规则（Mandatory Blocking Rules）

- **Rule-001（形貌阻断）**：若信号呈现“全程条带化”且缺乏任何可收敛的点形结构，判定为物理失效，禁止进行任何极性、纯度或组分数的推断。
- **Rule-002（溶剂溯源）**：若观察到点样区域存在溶剂未干或异常扩散痕迹，应直接回溯 `TLC-PRE-002-SAMPLE-PREPARATION-GATE`，撤销该板的判读权。
- **Rule-003（分辨能力失效）**：当条带宽度显著大于原始点样尺度时，判定该方法在当前条件下无法提供有效分辨率。

## 4. 操作性处置与策略（Corrective Actions）

以下处置仅用于**恢复可观测性**，不构成对当前板面信息的延伸解释或补充诊断：

1. **稀释与溶剂置换**：使用低沸点、低粘度且溶解性良好的溶剂对样品进行显著稀释，以降低单位面积载量与溶剂残留影响。
2. **强制干燥**：点样后通过热风、真空或延长静置时间，确保高沸点溶剂完全挥发后再进行展开。
3. **技术转移评估**：若在合理稀释与干燥条件下仍持续出现条带化失效，应判定 TLC 在该体系下信息密度不足，考虑转向 HPLC、LC-MS 等替代分析手段。

## 5. 物理失效证据（Physical Evidence）

- **局部迁移畸变**：点样区域的溶剂残留显著改变了初始迁移环境，使本应受硅胶吸附控制的迁移行为被整体拖拽，导致板面失去层析判读意义。
