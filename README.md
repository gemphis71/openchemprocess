[English](#openchemprocess) | [Chinese](#openchemprocess-chinese)

# OpenChemProcess

## What is this

OpenChemProcess is an open framework for structuring **chemical process knowledge and expert decision-making rules** in a form usable by both humans and machines.

It focuses on:

- Control authority and irreversible decision points
    
- Expert reasoning derived from real laboratory and industrial practice
    
- Machine-readable representations of process judgment
    

---

## Why this matters

Most process failures are not caused by missing knowledge, but by **loss of control authority at earlier stages**.

This project makes these hidden structures explicit and analyzable.

---

## How to read

This repository has three layers:

- `00_meta` → definitions, vocabulary, structural rules
    
- `01_process` → core process snapshots and decision logic
    
- `02_observation` → experimental observations and visual evidence
    

Each file is a **snapshot**, representing:

- a specific process condition or failure mode
    
- its dependencies on upstream decisions
    

---

## Start here

If you are new, start with:

1. CHG-001 – Charging Sequence
    
2. MIX-001 – Mixing Time-Scale Failure
    
3. ISOL-003 – Filtration Control Authority
    

Then follow dependencies to explore related snapshots.

---

## Data Structure

- **Primary format: Markdown (.md)**  
    → authoritative source containing expert reasoning and logic
    
- **Derivative formats: CSV / JSON (planned)**  
    → extracted for machine use
    

Markdown files are the only manually curated source of truth.

---

## Navigation

By process:

- Isolation
    
- Mixing
    
- Thermal
    
- Charging
    
- Workup
    

---

## Language

Each snapshot has two versions:

- English (`.en.md`) – authoritative logic
    
- Chinese (`.zh.md`) – supporting expert context
    

Both share the same `canonical_id`.

---

## License

This project is licensed under the Creative Commons Attribution 4.0 International (CC BY 4.0).

---
# OpenChemProcess-Chinese

## 这是什么

OpenChemProcess 是一个开放框架，旨在将**化学工艺知识与专家决策规则**结构化表达为同时适用于人类与机器的形式。

本项目重点关注：

- 控制权（Control Authority）与不可逆决策节点
    
- 来源于真实实验室与工业实践的专家判断逻辑
    
- 化学工艺判断与推理的机器可读表达
    

---

## 为什么重要

大多数工艺失败并非源于知识缺失，而是由于**早期阶段控制权的丧失**。

本项目的目标是将这些隐性的结构显性化，并使其可分析、可复用。

---

## 如何阅读

本仓库分为三层结构：

- `00_meta` → 定义、术语与结构规则
    
- `01_process` → 核心工艺快照与决策逻辑
    
- `02_observation` → 实验观测与证据
    

每一个文件都是一个 **snapshot（快照）**，表示：

- 一个具体的工艺状态或失败模式
    
- 以及它对上游决策的依赖关系
    

---

## 建议阅读路径

如果是第一次接触，建议从以下内容开始：

1. CHG-001 – 加料顺序
    
2. MIX-001 – 混合时间尺度失效
    
3. ISOL-003 – 过滤中的控制权问题
    

随后可以根据 dependency 继续扩展阅读。

---

## 数据结构

- **主要格式：Markdown (.md)**  
    → 权威数据源，包含完整的专家判断与逻辑
    
- **派生格式：CSV / JSON（规划中）**  
    → 从 Markdown 自动提取，用于机器处理
    

Markdown 文件是唯一人工维护的真实来源。

---

## 导航方式

按工艺模块浏览：

- 分离（Isolation）
    
- 混合（Mixing）
    
- 热过程（Thermal）
    
- 加料（Charging）
    
- 后处理（Workup）
    

---

## 语言说明

每个 snapshot 提供两种版本：

- 英文（`.en.md`）— 权威逻辑版本
    
- 中文（`.zh.md`）— 中文仅作为辅助说明，不作为权威版本
- 
    

两者共享同一 `canonical_id`。

---

## 许可

本项目采用 CC BY 4.0 许可协议。