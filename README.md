# AI 学习路线：应用构建者 × 管理者

[![Link Check](https://github.com/luckliu2007/ai-ml-data-roadmap/actions/workflows/link-check.yml/badge.svg)](https://github.com/luckliu2007/ai-ml-data-roadmap/actions/workflows/link-check.yml)
[![License: CC0-1.0](https://img.shields.io/badge/License-CC0_1.0-lightgrey.svg)](./LICENSE)

一套**以产出为驱动**的 AI 学习框架，面向两类人：

- **AI 应用 / 产品构建者**：不必从数学推导学起，但要把大模型真正用进产品和工作流，并能证明它“有效”。
- **管理者 / 高管**：要判断 AI 在自己行业的价值在哪里、怎么选用例、怎么组织落地、怎么管住风险。

> 想走算法 / 模型工程师路线（从数学、PyTorch 到从零实现 LLM），见姊妹仓库 [github-learning-resources 的 AI 分类](https://github.com/luckliu2007/github-learning-resources/blob/main/categories/06-ai-ml-data.md)。

## 为什么是这套框架

市面上的 AI 资料不缺，缺的是**顺序、取舍和检验**。这里的做法：

1. **一手资料优先**：模型厂商官方指南、标准组织原文、权威年度报告，二手解读只作补充。
2. **每个模块都有产出**：读完不算学完，交出一份能用的东西才算。
3. **评估先行**：无论做产品还是做决策，先定义“怎样算好”，再动手。
4. **区分事实与推断**：引用数据标注来源和日期，AI 领域的数字半年就会过时。

## 目录

| 文件 | 内容 |
| --- | --- |
| [best-practices-2026.md](best-practices-2026.md) | **2026 AI 最佳实践**：今年的 9 项技术与监管变化、构建者 13 条、管理者 11 条、90 天行动计划 |
| [tech-radar-2026.md](tech-radar-2026.md) | **AI 技术雷达**：依据 Thoughtworks 技术雷达第 34 期，把 AI 方法、工具、平台、框架分为采用 / 试用 / 评估 / 谨慎四档，附 7 个反模式 |
| [ai-regulation-tracker.md](ai-regulation-tracker.md) | **AI 合规时间线**：中国、欧盟、国际标准的关键日期与企业合规最小清单 |
| [framework.md](framework.md) | **能力模型**：两条路线共用的 8 个核心概念 + L1–L4 四级能力标准 |
| [tracks/app-builder.md](tracks/app-builder.md) | **应用构建者路线**：12 周、6 个模块、1 个毕业项目 |
| [tracks/leader.md](tracks/leader.md) | **管理者路线**：8 周、6 个模块、1 份 AI 战略备忘录 |
| [self-assessment.md](self-assessment.md) | 按等级自测清单，开始前测一次、每个模块后再测 |
| [resources.md](resources.md) | 全部资源总表（类型、语言、费用、核实日期） |
| [templates/](templates/) | 用例画布、评估计划、模型选型评分卡、AI 试点立项书、AI 战略备忘录、智能体授权与管控清单、员工 AI 使用规范、AI 事故响应手册、每周学习记录 |

## 怎么开始

1. 用 [self-assessment.md](self-assessment.md) 给自己定级（大多数人起点是 L1）。
2. 选一条路线；两条都想学，先走管理者路线（8 周）建立判断力，再走应用路线。
3. 每周固定节奏：**3 小时学习 + 2 小时动手 + 30 分钟复盘**，用 [每周记录模板](templates/weekly-log.md)。
4. 每个模块结束交付该模块“产出”，再进入下一个。

## 两条路线一览

| 模块 | 应用构建者（12 周） | 管理者（8 周） |
| --- | --- | --- |
| 1 | 模型认知与选型 | AI 能力与局限的真实图景 |
| 2 | 提示与上下文工程 | 产业影响与价值池 |
| 3 | AI 编程智能体 | 用例发现与优先级 |
| 4 | 知识库与 RAG | 从试点到规模化：组织与人才 |
| 5 | 智能体、工具与工作流（MCP / Skills） | 风险、治理与合规（中 / 欧 / 美） |
| 6 | 评估驱动的产品化 | 投资、度量与 AI 战略 |
| 毕业 | 上线一个有评估集的 AI 应用 | 一份 AI 战略备忘录 + 用例组合 |

## 路线图

下一步的补强方向和维护机制见 [ROADMAP.md](ROADMAP.md)。

## 维护

- 链接由 [Link Check](.github/workflows/link-check.yml) 每周一自动检查。
- 资源每季度复核一次：是否仍在维护、是否有新版本、是否有更好的替代。变更记在 [CHANGELOG.md](CHANGELOG.md)。

## License

[CC0 1.0](LICENSE)。本仓库只做整理和学习设计，所链接的第三方内容遵循其各自版权。
