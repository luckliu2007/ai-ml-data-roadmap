# AI 技术雷达（2026）

**核实日期：2026-10-27。** 依据 Thoughtworks 技术雷达[第 34 期](https://www.thoughtworks.com/content/dam/thoughtworks/documents/radar/2026/04/tr_technology_radar_vol_34_en.pdf)（2026-04，共 118 个条目）原文，只挑出与本仓库两条路线有关的 AI 条目。“分档”是 Thoughtworks 交付团队的判断；“怎么用”一列是本仓库的建议，并指向对应模块。Thoughtworks 每年春秋各发一期，第 35 期发布后按新版更新本文。

> 雷达是一家咨询公司的一线经验，不是标准。和你自己的评估结果冲突时，以你的评估集为准（见 [评估计划模板](templates/eval-plan.md)）。

## 四个分档

| 分档 | Thoughtworks 的定义 | 你该怎么做 |
| --- | --- | --- |
| **采用**（Adopt） | 业界应当采用，他们在合适的项目里都在用 | 作为默认选项 |
| **试用**（Trial） | 值得投入，要学会构建这项能力；可以在能承受风险的项目上试 | 选一个非关键项目用起来 |
| **评估**（Assess） | 值得探索，目的是弄清它会怎样影响你的企业 | 小范围实验，不进关键系统 |
| **谨慎**（Caution） | 小心推进，存在需要结合自身情况仔细评估的重大问题 | 当成反模式清单逐条自查 |

---

## 一、方法与实践

| 条目 | 分档 | 一句话 | 怎么用 |
| --- | --- | --- | --- |
| [上下文工程](https://www.thoughtworks.com/radar/techniques/context-engineering) | 采用 | 把上下文窗口当作设计对象，而不只是改提示词措辞；原始数据一股脑塞进去会导致“上下文腐化” | [应用路线模块 2](tracks/app-builder.md#模块-2--提示与上下文工程第-23-周) |
| [团队共享的智能体说明](https://www.thoughtworks.com/radar/techniques/curated-shared-instructions-for-software-teams) | 采用 | 不再靠每个人自己写提示，把 AGENTS.md、CLAUDE.md 等说明文件放进新项目的脚手架模板，团队统一维护 | 模块 3：每个仓库一份 AGENTS.md，由团队评审 |
| [结构化输出](https://www.thoughtworks.com/radar/techniques/structured-output-from-llms) | 采用 | 程序要消费模型输出时，约束模型按 JSON Schema 等固定格式返回；用 Instructor、Pydantic AI 这类库屏蔽各家差异，并自动校验和重试 | 模块 5、6 |
| [DORA 指标](https://www.thoughtworks.com/radar/techniques/dora-metrics) | 采用 | 变更前置时间、部署频率、恢复时间、变更失败率，加上新的第五个指标“返工率”。AI 写代码更快，如果这些指标没改善，就没有带来更好的结果 | [管理者路线模块 4](tracks/leader.md#模块-4--从试点到规模化组织与人才第-5-周)；[最佳实践](best-practices-2026.md)管理者第 9 条 |
| 零信任架构 | 采用 | 构建和运行智能体的默认安全架构：“从不信任、始终验证”、基于身份的安全、最小权限，并持续监控智能体的行为 | 模块 6 安全实践；[智能体授权与管控清单](templates/agent-governance-checklist.md) |
| [Agent Skills](https://agentskills.io/) | 试用 | 把指令、脚本和资料打包，按需加载，减少 token 消耗和指令膨胀；**不要未经审查就复用第三方 Skill**，有供应链风险 | 模块 5 |
| [编程智能体的反馈传感器](https://www.thoughtworks.com/radar/techniques/feedback-sensors-for-coding-agents) | 试用 | 把编译器、lint、类型检查、测试接进智能体工作流，失败时让它自己先改，再交给人审 | 模块 3；最佳实践构建者第 10 条 |
| [渐进式上下文披露](https://www.thoughtworks.com/radar/techniques/progressive-context-disclosure) | 试用 | 先给智能体一份“目录”，由它挑出这一步需要的内容再加载，而不是一开始塞满各种“必须 / 禁止”规则 | 模块 2、5 |
| [编程智能体沙盒执行](https://www.thoughtworks.com/radar/techniques/sandboxed-execution-for-coding-agents) | 试用 | 限制文件系统、网络和资源。Thoughtworks 认为沙盒应是默认配置，而不是可选增强 | 模块 3；最佳实践构建者第 7 条 |
| 语义层 | 试用 | 在数据和使用方（BI、AI 智能体、API）之间统一指标口径、关联关系和访问规则；问数类智能体（text-to-SQL）尤其需要 | 模块 4 进阶 |
| 变异测试 | 试用 | 故意往代码里注入错误，看测试能不能发现。用来识破 AI 生成的“覆盖率很高、其实什么都没断言”的测试 | 模块 3 |
| [小语言模型](https://www.thoughtworks.com/radar/techniques/small-language-models) | 评估 | 某些任务上，小模型每花一块钱得到的效果开始优于大模型；适合摘要、基础编码和对延迟敏感的智能体步骤 | [应用路线模块 1](tracks/app-builder.md#模块-1--模型认知与选型第-1-周) |
| 编程智能体小队 | 评估 | 少量分工明确的智能体（实现、评审等）由一个编排者协调；与“蜂群”不同，后者见下方“谨慎” | 模块 3 进阶 |
| [有毒数据流分析](https://www.thoughtworks.com/radar/techniques/toxic-flow-analysis-for-ai) | 评估 | 找出“能读私密数据 + 会接触不可信内容 + 能对外发送”三者同时具备的路径（Simon Willison 所说的[“致命三要素”](https://simonwillison.net/2025/Jun/16/the-lethal-trifecta/)），在被利用前切断 | 模块 6 安全实践 |
| [MITRE ATLAS](https://atlas.mitre.org/) | 评估 | 针对 AI 系统的攻击战术与技术知识库 | 模块 6 安全实践 |
| RAG 中按角色隔离上下文 | 评估 | 建索引时给每个文本块打上权限标签，检索时按用户身份过滤，模型根本拿不到无权查看的内容 | [应用路线模块 4](tracks/app-builder.md#模块-4--知识库与-rag第-67-周) |
| 用视觉语言模型端到端解析文档 | 评估 | 用专门训练的视觉语言模型直接把文档图像转成结构化内容，替代“版面检测 + OCR + 后处理”多段流水线 | 模块 4 |
| 衡量与编程智能体的协作质量 | 评估 | 别掉进“速度陷阱”：看一次通过率、每个任务的来回次数、合并后的返工、构建失败和评审负担；按团队而不是按个人统计，并和 DORA 指标一起看 | 管理者路线模块 4 |
| Skills 作为可执行的入职文档 | 评估 | 用一个 `/_setup` 之类的 Skill 代替“README + 安装脚本”，让新人（和智能体）按当前环境一步步完成初始化 | 模块 5 |

### 谨慎：七个反模式

这一组最值得管理者和构建者一起读，可以直接当作自查清单：

| 反模式 | 问题是什么 | 对策 |
| --- | --- | --- |
| [智能体指令膨胀](https://www.thoughtworks.com/radar/techniques/agent-instruction-bloat) | AGENTS.md 越写越长、互相矛盾，埋在长上下文中间的规则容易被忽略；研究显示手写的说明往往比让模型生成的更有效 | 只写必要的规则，持续精简；其余做成按需加载的 Skill |
| [AI 加速的影子 IT](https://www.thoughtworks.com/radar/techniques/ai-accelerated-shadow-it) | 非技术人员用 AI 工具搭出没人管的智能体流程，带来安全风险和大量重复建设 | 提供有监控的内部沙盒供人试验；分清一次性流程和需要正式上线的关键流程 |
| [代码库认知债](https://www.thoughtworks.com/radar/techniques/codebase-cognitive-debt) | AI 改代码越来越快，团队对系统“为什么这样设计”的理解跟不上，最终小改动引发连锁故障 | 反馈传感器、关注团队认知负荷、用架构适应度函数持续守住关键约束 |
| [编程智能体蜂群](https://www.thoughtworks.com/radar/techniques/coding-agent-swarms) | 由 AI 动态决定规模的几十到上百个智能体并行开发。最受关注的两个实验（Anthropic 用并行智能体写 C 编译器、Cursor 用一周时间做出浏览器）都选了已有详细规格说明的场景 | 先用小队；没有详细规格和自动化验证，就不要上蜂群 |
| [用代码产出量衡量生产率](https://www.thoughtworks.com/radar/techniques/coding-throughput-as-a-measure-of-productivity) | 用代码行数、PR 数衡量 AI 提效，会催生大量对不上架构、审不过来的代码，评审周期反而变长 | 看 DORA 指标和“一次通过率”（AI 产出不用大改就能用的比例） |
| [忽视智能体工作流的持久性](https://www.thoughtworks.com/radar/techniques/ignoring-durability-in-agent-workflows) | 模型或工具调用一失败，跑了几小时甚至几天的任务就得重来；在开发环境能跑，到生产环境就垮 | 先用智能体框架自带的持久化执行（如 LangGraph、Pydantic AI），关键流程再上 Temporal 等持久化执行平台 |
| [默认使用 MCP](https://www.thoughtworks.com/radar/techniques/mcp-by-default) | 把 MCP 当成接任何系统的默认方式。每多一层协议就多一层信息损耗 | 先问是否真需要协议级互通。一个有完善 `--help`、返回 JSON、报错清楚的命令行工具往往就够了；需要结构化契约、OAuth 授权边界、多租户管控时再用 MCP |

---

## 二、工具

| 条目 | 分档 | 一句话 | 怎么用 |
| --- | --- | --- | --- |
| [Claude Code](https://github.com/anthropics/claude-code) | 采用 | 被 Thoughtworks 内外团队日常用于生产交付，常被当作能力和易用性的参照 | [应用路线模块 3](tracks/app-builder.md#模块-3--ai-编程智能体第-45-周) |
| Cursor | 采用 | 与 Claude Code 一起是交付团队的默认选择；在 IDE 里审核计划再执行的体验更好 | 模块 3 |
| [OpenAI Codex](https://github.com/openai/codex) | 试用 | 适合新项目和重复性的实现工作；容易给出逻辑正确但已过时的库用法，必须配自动化测试和人工评审 | 模块 3 |
| Claude Code 插件市场 | 试用 | 用插件给团队分发 Skills、命令等配置 | 模块 3、5 |
| Dev Containers | 试用 | 用容器给编程智能体提供隔离环境 | 模块 3 |
| [OpenSpec](https://github.com/Fission-AI/OpenSpec) | 评估 | 规格驱动开发框架：先对齐“做什么”，再让智能体写代码 | 模块 3（已收录） |
| [PageIndex](https://github.com/VectifyAI/PageIndex) | 评估 | 无向量、基于推理的长文档检索 | 模块 4（已收录） |
| [Agent Scan](https://www.thoughtworks.com/radar/tools/agent-scan)（[GitHub](https://github.com/snyk/agent-scan)） | 评估 | 扫描本机的 MCP 服务器和 Skills，发现提示注入、工具投毒、有毒数据流、硬编码密钥等风险；扫描时要把组件元数据发给 Snyk，误报率需在自己环境中验证 | 模块 6 安全实践 |
| Bloom | 评估 | Anthropic 推出的行为评估工具：按设定的目标行为自动生成大量测试对话，检测模型的谄媚、自保等倾向 | 模块 6 进阶 |
| OpenCode | 评估 | 开源终端编程智能体，可接云端、自托管或本地模型，适合成本控制和隔离网络环境 | 模块 3 |
| **OpenClaw** | **谨慎** | 开源的“超个人化 AI 助手”：接入日历、邮件、文件越多就越有用，权限也越集中，正是有毒数据流分析要防的模式；Thoughtworks 强调，大厂的同类产品也有同样的风险 | 了解风险即可；这类助手不要接入公司数据 |

## 三、平台

| 条目 | 分档 | 一句话 | 怎么用 |
| --- | --- | --- | --- |
| [Langfuse](https://www.thoughtworks.com/radar/platforms/langfuse)（[GitHub](https://github.com/langfuse/langfuse)） | 试用 | 开源 LLM 工程平台：追踪、提示管理、评估、数据集；SDK 基于 OpenTelemetry。自托管组件较多，先评估规模是否值得 | [应用路线模块 6](tracks/app-builder.md#模块-6--评估驱动的产品化第-1011-周) |
| AWS Bedrock AgentCore | 试用 | 云上的智能体运行平台；更成功的做法是只用它处理会话隔离、安全、可观测等生产问题，业务逻辑留在自己的代码里 | 模块 5 进阶 |
| AG-UI 协议 | 试用 | 统一前端界面和后端智能体之间的通信：流式推理步骤、状态同步、动态组件 | 模块 5 |
| Graphiti | 试用 | 带时间维度的知识图谱，记录事实何时生效、何时失效，用于智能体记忆 | 模块 4 进阶 |
| MCP Apps | 评估 | MCP 首个官方扩展，让 MCP 服务器在对话里返回交互式界面 | 模块 5 |
| Agent Trace | 评估 | Cursor 提出的开放规范，记录每一行代码是人写的还是 AI 写的 | 管理者路线模块 5（审计） |

## 四、语言与框架

| 条目 | 分档 | 一句话 | 怎么用 |
| --- | --- | --- | --- |
| [LiteLLM](https://www.thoughtworks.com/radar/languages-and-frameworks/litellm)（[GitHub](https://github.com/BerriAI/litellm)） | 试用 | AI 网关：多家模型统一接入、重试和故障切换、成本与预算控制、访问控制和数据脱敏。注意：用了某家独有的功能，又会重新绑定到这家。2026-03 曾发生 PyPI 供应链投毒，见[官方说明](https://docs.litellm.ai/blog/security-update-march-2026) | 模块 6 进阶 |
| [Docling](https://www.thoughtworks.com/radar/languages-and-frameworks/docling)（[GitHub](https://github.com/docling-project/docling)） | 试用 | 开源文档解析：PDF、扫描件转成 JSON / Markdown，可自托管，替代云厂商的文档识别服务 | [应用路线模块 4](tracks/app-builder.md#模块-4--知识库与-rag第-67-周) |
| [DeepEval](https://www.thoughtworks.com/radar/languages-and-frameworks/deepeval)（[GitHub](https://github.com/confident-ai/deepeval)） | 试用 | 开源评估框架：RAG 指标、自定义指标，以及工具调用正确性、任务完成度等智能体指标 | 模块 6 |
| LangGraph | 试用 | 被移出“采用”：Thoughtworks 认为“有状态图 + 全局共享状态”不总是最好的做法，很多场景先用简单智能体、需要时再加图结构更精简 | 模块 5 |
| Agent Development Kit（ADK） | 试用 | Google 的智能体框架，部分功能仍未正式发布；同类还有 OpenAI Agents SDK、Claude Agent SDK、Microsoft Agent Framework 等 | 模块 5 |
| LangExtract | 试用 | 用大模型从非结构化文本中抽取结构化信息，每一项都能追溯到原文位置 | 模块 4 |
| GitHub Spec Kit | 评估 | 规格驱动开发工具，团队多在已有代码库中试用 | 模块 3 |
| Superpowers | 评估 | 由可组合 Skills 构成的编程智能体工作流 | 模块 3 |
| [Pipecat](https://github.com/pipecat-ai/pipecat) | 评估 | 开源语音与多模态智能体框架 | 模块 5 进阶（已收录） |
| Unsloth | 评估 | 开源微调与强化学习框架，显著降低显存和成本，消费级 GPU 也能微调 Llama、Qwen、DeepSeek 等开源模型 | 模块 6 进阶 |

---

## 五、这一期的四个主题

Thoughtworks 在本期总结了四个主题，可以作为 2026 年 AI 工程的“底层判断”：

1. **智能体时代，评估技术本身变难了。** 新名词不断出现（规格驱动开发、harness engineering 等），含义相互重叠；很多工具不到一个月大、只有一个维护者。AI 生成的代码越来越多，团队却未必理解它为什么能工作，形成“认知债”。
2. **保住原则，放弃套路。** 结对编程、零信任、变异测试、DORA 指标、整洁代码这些老原则重新变得重要，用来对冲 AI 快速制造复杂度；命令行也重新成为主要界面。
3. **给“权限饥渴”的智能体上锁。** 真正有用的智能体往往需要接触私密数据、外部内容和真实系统，“致命三要素”已经是常态而非配置失误。零信任、最小权限、纵深防御是底线，但没有银弹；更安全的形态是由多个受限智能体组成的流水线，加上强监控。
4. **给编程智能体套上缰绳。** 事前用 Skills、规格驱动开发提高第一次就做对的概率；事后用反馈传感器（编译、lint、测试、变异测试、代码质量分析）让智能体自我纠正，再交给人审。

## 六、怎么用这张雷达

- **构建者**：选型时默认从“采用”和“试用”里挑；“评估”类只在小项目里试，并记录结论；每季度对照“谨慎”七条自查一次。
- **管理者**：把“谨慎”七条变成治理问题，在季度复盘时逐条问技术负责人。例如：我们是不是在用代码行数或 PR 数衡量 AI 提效？员工自己搭的智能体流程有没有登记？跑几天的智能体任务失败后能不能接着跑？
- **更新**：Thoughtworks 第 35 期发布后，核对本文每个条目的分档变化，并在 [CHANGELOG](CHANGELOG.md) 记录。

> 相关：[2026 AI 最佳实践](best-practices-2026.md) · [AI 合规时间线](ai-regulation-tracker.md) · [资源总表](resources.md)
