# OpenChemProcess — Chapter 判定与写作元原则（v0.2）

> **Status:** active constitution
> 
> **Scope:** This document defines the _structural constitution_ of OpenChemProcess.  
> It constrains how Chapters are defined, how snapshots are organized, and how revisions are allowed.

---

## 0. 写作目标与边界

OpenChemProcess 不是知识分类项目，也不是工艺手册。

它的目标是：

> **以工程可验证的方式，记录真实工艺在放大过程中反复出现的结构性失败模式。**

因此：

- Chapter 不是“主题集合”，而是**失败高密度的工艺阶段（stage）**
    
- Snapshot 不是案例合集，而是**失败坐标轴（failure coordinates）**
    
- 项目整体必须防止退化为 SOP、HAZOP 或“最佳实践大全”
    

---

## 1. Chapter 的主轴：不可逆承诺（Irreversible Commitment）

Chapter 的一级划分以**不可逆承诺发生的工艺阶段**为主轴。

所谓不可逆承诺，是指在真实放大或生产条件下：

- 系统从“可逆试错”进入“下注状态”
    
- 后续调节即使存在，也已无法改变最终结局
    

典型示例：

- Early diagnostics（如 TLC）：尚未投料，但已形成错误信心与决策路径
    
- Charging：第一次不可逆承诺（加料顺序、方式或速率导致失去控制杠杆）
    
- Quench / Workup：第二次不可逆承诺（以为结束，实为再次下注）
    

---

## 2. 两条全局元轴（Meta-axes）

以下两条轴**不是 Chapter，也不是独立内容对象**，而是所有 Chapter 与 snapshot **必须显式回应的判断维度**。

### 2.1 T-axis：容错包络（Tolerance Envelope）

用于回答：

- 在该工艺阶段，系统允许多大的偏差仍可 survive？
    
- 偏差如何从“可修复”跨越到“不可修复”？
    

容错包络必须以**条件区间与失效边界**的形式出现，而不是模糊经验判断。

---

### 2.2 S-axis：放大敏感性（Scale Sensitivity）

用于回答：

- 放大后，容错包络是线性缩小、非线性塌缩，还是直接消失？
    
- 哪些控制杠杆在小试存在，但在放大后变成“名义存在、实质无效”？
    

S-axis 的核心不是“规模效应存在与否”，而是**包络形态在 scale-up 中的系统性变化**。

---

## 3. Chapter 判定的三条硬标准

一个概念是否可以上升为**独立 Chapter**，必须**同时满足**以下三条：

1. **Stage 标准**  
    是否对应一个独立、可反复触发失败的工艺阶段（而非单一变量或条件）？
    
2. **包络标准**  
    是否存在该阶段独有的容错包络，可清晰描述 survive 条件与失效边界？
    
3. **放大标准**  
    该容错包络是否在 scale-up 中系统性塌缩或变形，形成结构性劣势？
    

> 若任一标准不满足，该概念通常应作为 Chapter 内的风险维度、判据或子结构，而非独立 Chapter。

---

## 4. 不独立成 Chapter 的常见要素（默认规则）

以下要素通常**非常重要**，但默认不独立成章，应嵌入各 Chapter 的风险结构中：

### 4.1 Thermal / Safety（TMP / SAF）

- 属性：结果变量
    
- 正确位置：
    
    - 各 Chapter 的失效边界
        
    - 不可逆节点之后的“是否仍有回旋空间”判据
        
- 允许使用的结构化工具：
    
    - Q_exo vs Q_cooling
        
    - ΔT_ad
        
    - 条件空间 → 结果空间的响应面（response surface）
        

---

### 4.2 MAT / RAW（物料与规格）

- 属性：条件变量
    
- 正确位置：
    
    - survive 条件
        
    - 失效边界
        
    - 002-level 的具体案例
        

原料本身不制造失败，**使用方式 + 工艺阶段**才制造失败。

---

### 4.3 ATM（气氛 / 压力等状态条件）

- 属性：状态约束
    
- 正确位置：
    
    - 特定 Chapter 内的边界条件
        
    - 不可逆节点描述
        

不应泛化为“环境条件章节”。

---

## 5. Chapter 内部写作规则

所有 Chapter 与 snapshot 需遵循以下一致规则：

- **001 层级**：结构性风险 / risk envelope（非 yes–no gate）
    
- **002 层级**：具体失败模式、经验案例、可复现实例
    
- failure-first：从放大失败的结构风险出发，而非最佳实践
    
- 允许 survive，但必须写清成立条件
    
- 文件保持 open / appendable，不封闭
    

---

## 6. 版本化修订规则（强约束）

本原则允许修订，但必须遵守以下约束：

1. 修订前必须调出旧版本全文及当时的思考背景
    
2. 所有修改需形成新版本号（vX.Y）
    
3. 必须记录：
    
    - 修改动机
        
    - 新增证据或反例
        
    - 对既有 Chapter 判定的影响
        

> 禁止未经回溯原思考过程而“随意调整结构或偷换定义”。

---

## 7. 运行时提醒机制（项目级约定）

在写作与扩展过程中，需反复自检：

- 当前内容是否越过既定 Chapter 边界？
    
- 是否显式回应了 T-axis 与 S-axis？
    
- 是否试图用“重要性”替代“阶段性”来申请独立 Chapter？
    

本文件用于**约束作者与未来协作者（包括 AI）**，而非教学用途。

---

**End of Constitution (v0.2)**