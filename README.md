# OpenChemProcess

**OpenChemProcess** is an open project for structuring chemical process knowledge
and expert decision-making rules in a form that is usable by both humans and machines.

## Scope
This project focuses on:
- Chemical process unit operations (e.g. TLC, HPLC, quenching, extraction)
- Expert decision rules derived from real laboratory and industrial practice
- Machine-readable representations of process judgment and reasoning

## Data Formats
- **Primary (authoritative) format: Markdown (.md)**
  - Markdown files contain the complete expert reasoning, spatial logic, and heuristic rules.
- **Derivative format: CSV / JSON**
  - Automatically extracted from Markdown for machine consumption (v0.2+).

Markdown files represent the ground-truth expert rules and are the only manually curated source.

## Languages
- **English**: Primary language for authoritative logic and machine-readable instructions.
- **Chinese**: Expert insights and deep context (supporting documentation).

## Project Status
- **01_process/tlc/**: Baseline logic for Thin Layer Chromatography, including spatial constraints and spotting layout rules.

## License
This project is licensed under the Creative Commons Attribution 4.0 International (CC BY 4.0).

---

# OpenChemProcess（中文说明）

**OpenChemProcess** 是一个开放项目，旨在将化学工艺知识与专家判断经验
系统化整理为**人类可理解、机器可读取**的结构化形式。

## 项目范围
本项目主要关注：
- 化学工艺中的单元操作（如 TLC、HPLC、淬灭、萃取等）
- 来源于真实实验室与工业实践的专家判断规则
- 化学工艺判断与决策逻辑的机器可读表示

## 数据格式说明
- **主要（权威）格式：Markdown (.md)** - Markdown 文件包含完整的专家推导逻辑、空间逻辑和启发式规则。
- **派生格式：CSV / JSON** - 从 Markdown 中自动提取，供机器读取 (v0.2+)。

## 语言说明
- 项目主语言：**英文**
- 中文仅作为辅助说明，不作为权威版本

## 项目状态
- **01_process/tlc/**: 薄层色谱（TLC）的基础逻辑，包括空间约束和点样布局规则。

## 许可证
本项目采用 Creative Commons Attribution 4.0 International（CC BY 4.0）许可协议。
