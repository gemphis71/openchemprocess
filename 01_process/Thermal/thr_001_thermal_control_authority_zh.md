snapshot_id: "THR-001-THERMAL-CONTROL-AUTHORITY"
status: "draft"
domain: "Process"
process: "Thermal"
topic: "温度作为反应路径与阶段控制权的风险结构"
level: "001"
note:  本文件用于识别在放大条件下， 温度是否从“速率调制参数”升级为“控制权来源”。不讨论设备传热能力或控温工程，仅讨论温度在反应逻辑层面对路径与阶段可达性的决定作用。
dependencies:
  - "CHG-001-CHARGING-SEQUENCE"
  - "CHG-002-ADDITION-MODE-AND-RATE"
  - "MIX-001-MIXING-TIME-SCALE-FAILURE"
---
## 1. 定位（Positioning）

在投料顺序（CHG-001）、  投料方式与名义速率（CHG-002）、  以及混合逻辑（MIX-001）在结构上均成立的前提下，

**温度在少数反应体系中成为第一控制权来源。**

在此类体系中：

- 温度不再只是反应“快慢”的调节参数；
    
- 温度的选择直接决定：
    
    - 哪一条反应路径占据主导；
        
    - 或反应是否能够跨越阶段 / 中间体边界；
        
- 一旦温度策略错误，  
    上游 CHG / MIX 控制手段无法等价补救。
    

---

## 2. 核心区分（Core Distinction）

### A｜并行反应路径分配

**Thermal as Competing Pathway Authority**

反应体系中存在两条或多条可达反应路径。  
温度通过改变这些路径的相对速率，  
对路径主导权进行分配。

**判定特征：**

- 改变温度即改变产物构成或选择性；
    
- 延长时间或调整加料速率无效；
    
- 控制权不可转移至 CHG / MIX 层。
    

---

### B｜反应阶段可达性

**Thermal as Stage-Gating Authority**

反应经由中间体或多阶段推进。  
温度决定反应是否、以及何时进入下一阶段。

**判定特征：**

- 特定温度区间内反应停滞或中间体积累；
    
- 升温后反应恢复或阶段跃迁；
    
- 温度决定阶段边界，而非仅影响速率。
    

---

## 3. A 类案例｜并行路径分配型

---

### Case A1｜Diol 选择性酰化中的路径占比转移（DLL）

#### System Conditions

- 底物：同时含 primary / secondary alcohol 的 diol
    
- 反应：pivaloyl chloride 酰化
    
- 本征速率比：~1:20（secondary : primary）
    

#### Logic Conflict

低温通常被用于“提高选择性”；  
但在该体系中，选择性变化并非线性随温度改善。

#### Observed Behavior

- 低温（~0 °C）：
    
    - primary alcohol 路径占主导；
        
    - secondary alcohol 路径被抑制；
        
    - 目标转化窗口内选择性稳定。
        
- 升温：
    
    - secondary alcohol 路径占比持续上升；
        
    - 选择性随反应推进塌缩。
        

#### Decision Trace

**Hypothesis Space**

- H1：选择性变化仅由整体反应速率变化引起
    
- H2：温度改变两条反应路径的相对速率
    
- H3：选择性塌缩源于后期底物比例变化
    

**Elimination Path**

- 不同温度下低转化区间已出现产物比例差异 → 排除 H1
    
- 底物比例变化无法解释早期差异 → 限定 H3
    

**Decision Pivot**  
温度通过改变 competing alcohol sites 的相对速率，  
对反应路径进行速率分配。  
路径主导权仅由温度决定，  
CHG / MIX 调整无法等价替代。

#### Explicit Labels

- Case_Type: Core
    
- Authority_Level: Primary
    
- Control_Mode: Competing_Pathway
    
- Substitutable_By: None
    

---

### Case A2｜CBS 不对称还原中的催化路径失权

#### System Conditions

- 并行路径：
    
    - CBS 催化循环（高 ee）
        
    - borane 直接还原（消旋）
        

#### Logic Conflict

“降温以提高选择性”的常规策略在该体系中发生反转。

#### Observed Behavior

- 降温：
    
    - 反应速率下降；
        
    - ee 持续降低；
        
    - 延长时间 / 增加催化剂载量无效。
        
- 升温：
    
    - 催化路径重新占主导；
        
    - ee 恢复并稳定。
        

#### Decision Trace

**Hypothesis Space**

- H1：ee 下降源于反应未完成
    
- H2：ee 下降源于路径占比变化
    
- H3：ee 变化来自后处理或时间效应
    

**Elimination Path**

- 延长时间 / 增加载量无效 → 排除 H1
    
- ee 变化早期即出现 → 排除 H3
    

**Decision Pivot**  
降温优先抑制 CBS 催化循环，  
非选择性路径占比上升。  
控制权位于温度层，  
无法由 CHG / MIX 转移。

#### Explicit Labels

- Case_Type: Core
    
- Authority_Level: Primary
    
- Control_Mode: Competing_Pathway
    
- Substitutable_By: None
    

---

## 4. B 类案例｜阶段可达性型（含中间体）

---

### Case B1｜稳定中间体导致阶段死锁

#### System Conditions

- 路径：S → I → P
    
- I 稳定；I → P 需更高温度
    

#### Logic Conflict

反应在低温下可启动，但无法完成。

#### Observed Behavior

- 低温：
    
    - 状态：I-Accumulated；
        
    - S 停止消耗；
        
    - 反应停滞。
        
- 升温：
    
    - I → P 转换启用；
        
    - 反应恢复推进。
        

#### Decision Pivot

温度决定阶段可达性。  
若 I → P 被禁用，反应在阶段边界被结构性阻断。

#### Explicit Labels

- Case_Type: Core
    
- Authority_Level: Primary
    
- Control_Mode: Stage_Gate
    
- Substitutable_By: None
    

---

### Case B2｜稳定中间体 + 不稳定产物

#### System Conditions

- I 稳定
    
- P 在高温下降解
    

#### Logic Conflict

恒定高温同时促进生成与降解。

#### Observed Behavior

- 恒定高温：P 快速降解；
    
- 分阶段温度：
    
    - 低温完成 S → I；
        
    - 短时升温完成 I → P；
        
    - P 高温停留时间显著缩短。
        

#### Decision Pivot

温度用于阶段解耦与停留时间管理，  
而非单纯速率提升。

#### Explicit Labels

- Case_Type: Core
    
- Authority_Level: Primary
    
- Control_Mode: Stage_Gate
    
- Substitutable_By: None
    

---

### Case B3｜不稳定中间体的生成–消耗错配（Boundary Case）

#### System Conditions

- 升温加快 S → I；
    
- I → P 相对缓慢；
    
- I 不稳定。
    

#### Logic Conflict

升温既放大风险，又可能是修复手段。

#### Observed Behavior

- 单纯升温：I 积聚、副反应放大；
    
- 两种修复路径成立：
    
    - 限制生成通量（CHG）；
        
    - 进一步升温加快 I → P。
        

#### Decision Pivot

thermal 与 charging 构成**可替代控制权层**，  
温度不再是唯一控制权来源。

#### Explicit Labels

- Case_Type: Boundary
    
- Authority_Level: Shared
    
- Control_Mode: Stage_Gate
    
- Substitutable_By: CHG
    

---

## 5. 使用提示（Usage Notes）

- 若温度异常仅在加料完成后显化，  
    且控制权在触发前已因库存积累丢失，  
    该风险应归属 CHG 层，而非 THR。
    
- 因 mixing time-scale failure 触发的热失控，  
    thermal 为表观变量而非控制权来源（参见 MIX-001）。
    
- Case B3 为跨层边界案例，不应作为 THR 核心正例。
    

---

## #Audit

本文件描述温度作为**第一控制权来源**的风险结构。  
其判定基于以下条件：

> 路径或阶段主导权是否**只能**通过温度选择来决定，  
> 且无法由 CHG / MIX 等价恢复。