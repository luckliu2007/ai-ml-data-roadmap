# AI 技术雷达（2026）

**核实日期：2026-11-05。** 依据 Thoughtworks 技术雷达[第 35 期](https://www.thoughtworks.com/content/dam/thoughtworks/documents/radar/2026/11/tr_technology_radar_vol_35_en.pdf)（2026-11，共 117 个条目）原文，只挑出与本仓库两条路线有关的 AI 条目；上一期是[第 34 期](https://www.thoughtworks.com/content/dam/thoughtworks/documents/radar/2026/04/tr_technology_radar_vol_34_en.pdf)（2026-04，共 118 个条目）。“分档”是 Thoughtworks 交付团队的判断；“怎么用”一列是本仓库的建议，并指向对应模块。第 35 期没有再列出的第 34 期条目仍然保留，并注明“第 35 期未再列出”：Thoughtworks 会给新条目腾位置，不再列出不代表过时。Thoughtworks 每年春秋各发一期，第 36 期（预计 2027 年春季）发布后按新版更新本文。

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
| [上下文工程](https://www.thoughtworks.com/radar/techniques/context-engineering) | 采用（第 34 期；第 35 期未再列出） | 把上下文窗口当作设计对象，而不只是改提示词措辞；原始数据一股脑塞进去会导致“上下文腐化” | [应用路线模块 2](tracks/app-builder.md#模块-2--提示与上下文工程第-23-周) |
| [团队共享的智能体说明](https://www.thoughtworks.com/radar/techniques/curated-shared-instructions-for-software-teams) | 采用（第 34 期；第 35 期未再列出） | 不再靠每个人自己写提示，把 AGENTS.md、CLAUDE.md 等说明文件放进新项目的脚手架模板，团队统一维护 | 模块 3：每个仓库一份 AGENTS.md，由团队评审 |
| [结构化输出](https://www.thoughtworks.com/radar/techniques/structured-output-from-llms) | 采用（第 34 期；第 35 期未再列出） | 程序要消费模型输出时，约束模型按 JSON Schema 等固定格式返回；用 Instructor、Pydantic AI 这类库屏蔽各家差异，并自动校验和重试 | 模块 5、6 |
| [DORA 指标](https://www.thoughtworks.com/radar/techniques/dora-metrics) | 采用（第 34 期；第 35 期未再列出） | 变更前置时间、部署频率、恢复时间、变更失败率，加上新的第五个指标“返工率”。AI 写代码更快，如果这些指标没改善，就没有带来更好的结果 | [管理者路线模块 4](tracks/leader.md#模块-4--从试点到规模化组织与人才第-5-周)；[最佳实践](best-practices-2026.md)管理者第 9 条 |
| 零信任架构 | 采用（第 34 期；第 35 期未再列出） | 构建和运行智能体的默认安全架构：“从不信任、始终验证”、基于身份的安全、最小权限，并持续监控智能体的行为 | 模块 6 安全实践；[智能体授权与管控清单](templates/agent-governance-checklist.md) |
| [智能体沙盒](https://www.thoughtworks.com/radar/techniques/agent-sandboxing) | 采用（第 35 期新增） | 由“编程智能体沙盒执行”扩展而来：智能体已经能操作业务系统，所有智能体都应默认在受限权限的隔离环境里运行；按威胁建模的结果决定隔离到什么程度 | 模块 5、6；[智能体授权与管控清单](templates/agent-governance-checklist.md)；最佳实践构建者第 7 条 |
| [威胁建模](https://www.thoughtworks.com/radar/techniques/threat-modeling) | 采用（第 35 期新增） | 提示注入、自主行动这类风险靠规则扫描查不出来，要由人主导、智能体辅助，定期做；从 MITRE ATLAS 等已知威胁出发，最后明确哪里可以接受不确定的模型行为、哪里必须加确定性护栏 | [应用路线模块 6](tracks/app-builder.md#模块-6--评估驱动的产品化第-1011-周)；[管理者路线模块 5](tracks/leader.md#模块-5--风险治理与合规第-67-周) |
| [交付路径梳理](https://www.thoughtworks.com/radar/techniques/path-to-production-mapping) | 采用（第 35 期新增） | 把从开发机到生产的每一步画出来，再标出痛点。编程智能体让写代码变快后，瓶颈会转到评审、测试和发布环节，要优化端到端流程而不只是写码速度 | [管理者路线模块 4](tracks/leader.md#模块-4--从试点到规模化组织与人才第-5-周)；最佳实践管理者第 9 条 |
| [渐进式上下文披露](https://www.thoughtworks.com/radar/techniques/progressive-context-disclosure) | 采用（第 35 期由试用改为采用） | 先给模型必要的上下文，再按需加载其余内容。正式应用里已几乎普遍这样做：AGENTS.md 保持精简、只放文档链接，MCP 工具和 Skill 用到时再加载，业务应用用 RAG 按问题检索 | 模块 2、5 |
| [变异测试](https://www.thoughtworks.com/radar/techniques/mutation-testing) | 采用（第 35 期由试用改为采用） | 故意往代码里注入错误，看测试能不能发现，用来识破 AI 生成的“覆盖率很高、其实什么都没断言”的测试；智能体也能在工作循环里自己做。全量跑很慢，只针对关键模块或最近改动的代码 | 模块 3 |
| [Agent Skills](https://agentskills.io/) | 试用（第 34 期；第 35 期未再列出） | 把指令、脚本和资料打包，按需加载，减少 token 消耗和指令膨胀；**不要未经审查就复用第三方 Skill**，有供应链风险 | 模块 5 |
| [编程智能体的反馈传感器](https://www.thoughtworks.com/radar/techniques/feedback-sensors-for-coding-agents) | 试用（第 34 期；第 35 期未再列出） | 把编译器、lint、类型检查、测试接进智能体工作流，失败时让它自己先改，再交给人审 | 模块 3；最佳实践构建者第 10 条 |
| [编程智能体沙盒执行](https://www.thoughtworks.com/radar/techniques/sandboxed-execution-for-coding-agents) | 试用（第 34 期；第 35 期未再列出，已扩展为上方的“智能体沙盒”） | 限制文件系统、网络和资源。Thoughtworks 认为沙盒应是默认配置，而不是可选增强 | 模块 3；最佳实践构建者第 7 条 |
| 语义层 | 试用（第 34 期；第 35 期未再列出） | 在数据和使用方（BI、AI 智能体、API）之间统一指标口径、关联关系和访问规则；问数类智能体（text-to-SQL）尤其需要 | 模块 4 进阶 |
| [智能体插件市场](https://www.thoughtworks.com/radar/techniques/agent-plugin-marketplace) | 试用（第 35 期新增） | 多个团队都在用编程智能体时，用 Git 仓库搭一个内部插件市场，统一发布、发现和更新 Skills、说明、MCP 服务器和子智能体定义，不再在仓库之间复制 | [应用路线模块 3](tracks/app-builder.md#模块-3--ai-编程智能体第-45-周)、5 |
| [开源权重模型](https://www.thoughtworks.com/radar/techniques/open-weight-models) | 试用（第 35 期新增） | DeepSeek、GLM、Kimi 等开源权重模型已在需要复杂推理和高质量代码的交付工作中表现良好；除了成本，还有部署灵活、不被厂商绑定、数据主权的好处，不应只当作“便宜的备选” | [应用路线模块 1](tracks/app-builder.md#模块-1--模型认知与选型第-1-周)；[模型选型评分卡](templates/model-selection-scorecard.md) |
| [按风险分级的人工监督](https://www.thoughtworks.com/radar/techniques/risk-tiered-human-oversight) | 试用（第 35 期新增） | 评审深度跟改动可能造成的后果挂钩：最高风险、最难回滚的改动由人亲自做，中等风险走人工评审，低风险由智能体通过 CI 自动合并；可按目录划“高风险区”，或用大模型给改动分级 | 模块 3；[管理者路线模块 5](tracks/leader.md#模块-5--风险治理与合规第-67-周)；[智能体授权与管控清单](templates/agent-governance-checklist.md) |
| [有状态护栏](https://www.thoughtworks.com/radar/techniques/stateful-guardrails) | 试用（第 35 期新增） | 护栏不只检查单条消息，而是看最近几轮对话，并在整个会话里累计“警告 / 封禁”状态，识别逐步展开的越狱和提示词套取；会增加延迟和成本，阈值要调 | [应用路线模块 6](tracks/app-builder.md#模块-6--评估驱动的产品化第-1011-周) |
| [用子智能体管理上下文](https://www.thoughtworks.com/radar/techniques/subagents-for-better-context-management) | 试用（第 35 期新增） | 把探索、工具输出、重试交给子智能体，主会话只收一段摘要，保护主智能体的上下文；一次跑两到四个，窄任务可用更便宜的模型。收益还没有系统测量，要看主会话的上下文是否真的变小 | 模块 2、[应用路线模块 5](tracks/app-builder.md#模块-5--智能体工具与工作流第-89-周) |
| [小语言模型](https://www.thoughtworks.com/radar/techniques/small-language-models) | 试用（第 35 期由评估改为试用） | 摘要、结构化抽取、意图分类、基础编码这类窄而高频的任务，小模型更便宜、延迟更低；除非需要多步推理或可靠的工具调用，智能体场景也可以先考虑小模型 | [应用路线模块 1](tracks/app-builder.md#模块-1--模型认知与选型第-1-周) |
| [有毒数据流分析](https://www.thoughtworks.com/radar/techniques/toxic-flow-analysis-for-ai) | 试用（第 35 期由评估改为试用） | 找出“能读私密数据 + 会接触不可信内容 + 能对外发送”三者同时具备的路径（Simon Willison 所说的[“致命三要素”](https://simonwillison.net/2025/Jun/16/the-lethal-trifecta/)），在被利用前切断；暗藏外泄指令的恶意 Skill 也在此列 | 模块 6 安全实践 |
| 编程智能体小队 | 评估（第 34 期；第 35 期未再列出） | 少量分工明确的智能体（实现、评审等）由一个编排者协调；与“蜂群”不同，后者见下方“谨慎”。第 35 期认为，多数人先在自己掌控下并行跑几个会话，是更稳妥的起点 | 模块 3 进阶 |
| [MITRE ATLAS](https://atlas.mitre.org/) | 评估 | 针对 AI 系统的攻击战术与技术知识库，给威胁建模提供共同的词汇 | 模块 6 安全实践 |
| RAG 中按角色隔离上下文 | 评估（第 34 期；第 35 期未再列出） | 建索引时给每个文本块打上权限标签，检索时按用户身份过滤，模型根本拿不到无权查看的内容 | [应用路线模块 4](tracks/app-builder.md#模块-4--知识库与-rag第-67-周) |
| 用视觉语言模型端到端解析文档 | 评估（第 34 期；第 35 期未再列出） | 用专门训练的视觉语言模型直接把文档图像转成结构化内容，替代“版面检测 + OCR + 后处理”多段流水线 | 模块 4 |
| 衡量与编程智能体的协作质量 | 评估（第 34 期；第 35 期未再列出） | 别掉进“速度陷阱”：看一次通过率、每个任务的来回次数、合并后的返工、构建失败和评审负担；按团队而不是按个人统计，并和 DORA 指标一起看 | 管理者路线模块 4 |
| Skills 作为可执行的入职文档 | 评估（第 34 期；第 35 期未再列出） | 用一个 `/_setup` 之类的 Skill 代替“README + 安装脚本”，让新人（和智能体）按当前环境一步步完成初始化 | 模块 5 |

### 谨慎：十二个反模式

这一组最值得管理者和构建者一起读，可以直接当作自查清单。前 7 个来自第 34 期，后 5 个是第 35 期新增：

| 反模式 | 问题是什么 | 对策 |
| --- | --- | --- |
| [智能体指令膨胀](https://www.thoughtworks.com/radar/techniques/agent-instruction-bloat) | AGENTS.md 越写越长、互相矛盾、过时；整套照搬外部指令集会让情况更糟 | 能写成确定性 hook 或检查的先改写；每换一代模型就重新评估，删掉它已不需要的规则（Anthropic 为新模型删掉了 Claude Code 八成以上的系统提示，效果没有可测的损失）；其余做成按需加载的 Skill |
| [AI 加速的影子 IT](https://www.thoughtworks.com/radar/techniques/ai-accelerated-shadow-it) | 非技术人员从无代码平台转向 Claude Code、Codex 等编程智能体，自己搭出的工具缺少测试、发布流程和监控，一旦被整个部门用起来，安全风险更大 | 提供有监控的内部沙盒和企业级运行框架供人试验；安全上不让步，同时给有用的工具一条转为正式支持的路径 |
| [代码库认知债](https://www.thoughtworks.com/radar/techniques/codebase-cognitive-debt)（第 34 期；第 35 期未再列出） | AI 改代码越来越快，团队对系统“为什么这样设计”的理解跟不上，最终小改动引发连锁故障 | 反馈传感器、关注团队认知负荷、用架构适应度函数持续守住关键约束；第 35 期新增的“追问”（让智能体动手前先就计划向你提问）也被认为有助于缓解 |
| [编程智能体蜂群](https://www.thoughtworks.com/radar/techniques/coding-agent-swarms)（第 34 期；第 35 期未再列出） | 由 AI 动态决定规模的几十到上百个智能体并行开发。最受关注的两个实验（Anthropic 用并行智能体写 C 编译器、Cursor 用一周时间做出浏览器）都选了已有详细规格说明的场景 | 先用小队；没有详细规格和自动化验证，就不要上蜂群 |
| [用代码产出量衡量生产率](https://www.thoughtworks.com/radar/techniques/coding-throughput-as-a-measure-of-productivity) | 用代码行数、PR 数，以及第 35 期点名的“AI 生成代码占比”“消耗的 token 数”衡量 AI 提效，会被当成荣誉徽章，甚至催生专为凑指标的 AI 忙碌工作 | 看 DORA 指标和协作质量（如“一次通过率”），并直接挂钩业务结果；活动指标只当信号，不当目标 |
| [忽视智能体工作流的持久性](https://www.thoughtworks.com/radar/techniques/ignoring-durability-in-agent-workflows)（第 34 期；第 35 期未再列出） | 模型或工具调用一失败，跑了几小时甚至几天的任务就得重来；在开发环境能跑，到生产环境就垮 | 先用智能体框架自带的持久化执行（如 LangGraph、Pydantic AI），关键流程再上 Temporal 等持久化执行平台 |
| [默认使用 MCP](https://www.thoughtworks.com/radar/techniques/mcp-by-default)（第 34 期；第 35 期未再列出） | 把 MCP 当成接任何系统的默认方式。每多一层协议就多一层信息损耗 | 先问是否真需要协议级互通。一个有完善 `--help`、返回 JSON、报错清楚的命令行工具往往就够了；需要结构化契约、OAuth 授权边界、多租户管控时再用 MCP |
| [人在回路的表演](https://www.thoughtworks.com/radar/techniques/human-in-the-loop-theater)（第 35 期新增） | 让人去批准他根本没法认真评估的动作、提示或改动，审批成了走过场，出了问题没有人真正负责 | 按风险分级：只把人能真正判断的改动留给人审；其余改用变异测试、基于属性的测试、形式化模型和语义评审来把控整个系统 |
| [一律用前沿模型](https://www.thoughtworks.com/radar/techniques/blanket-frontier-model-usage)（第 35 期新增） | 不管成本、延迟和实际需要，所有任务都默认用最强的模型；探索、简单修改、摘要这类日常工作往往用小模型或开源权重模型就够了 | 按任务或按子智能体选模型，或让运行框架按复杂度自动切换；在新会话、子智能体、从计划转到实现这类自然边界切换，以保住提示缓存；用上下文分析确认确实省了钱 |
| [对智能体 Skill 的认知投降](https://www.thoughtworks.com/radar/techniques/agent-skill-cognitive-surrender)（第 35 期新增） | 不加理解就整套引入大型社区 Skill 库或重型智能体框架：团队看不懂系统在做什么，未经审查的指令会进入执行流水线，不同来源的 Skill 还可能互相冲突 | 先读、先审，再改编使用；模型越来越强，通用社区 Skill 可能变得多余，更值得积累贴合项目的领域 Skill |
| [AI 驱动的文档泛滥](https://www.thoughtworks.com/radar/techniques/ai-driven-documentation-sprawl)（第 35 期新增） | 用智能体和规格驱动工具批量生成 Markdown 文档，看起来专业、进展很快，但没有质量门禁；过时、矛盾的规格和 ADR 会占用智能体的上下文并把它带偏 | 把 Markdown 当作一等产物，安排人定期删减、合并、修订，让智能体读到的上下文简洁、准确、可信 |
| [朴素的上下文压缩](https://www.thoughtworks.com/radar/techniques/naive-context-compression)（第 35 期新增） | 为省 token 粗暴压缩提示：可能打断提示缓存，账单反而更高；丢失信息让智能体变笨；用大模型做摘要式压缩又增加延迟和成本 | 先分析上下文到底花在哪，再同时评估净成本和任务准确率；优先选只压缩工具输出、保留原始数据引用、只在任务边界一次性裁剪历史的工具 |

---

## 二、工具

| 条目 | 分档 | 一句话 | 怎么用 |
| --- | --- | --- | --- |
| [Claude Code](https://github.com/anthropics/claude-code) | 采用（第 34 期；第 35 期未再列出） | 被 Thoughtworks 内外团队日常用于生产交付，常被当作能力和易用性的参照；第 35 期在 OpenAI Codex 条目中仍把它列为团队日常使用的命令行编程智能体 | [应用路线模块 3](tracks/app-builder.md#模块-3--ai-编程智能体第-45-周) |
| Cursor | 采用（第 34 期；第 35 期未再列出） | 与 Claude Code 一起是交付团队的默认选择；在 IDE 里审核计划再执行的体验更好 | 模块 3 |
| [OpenAI Codex](https://github.com/openai/codex) | 采用（第 35 期由试用改为采用） | 与 Claude Code、OpenCode 并列为团队日常使用的命令行编程智能体；具备操作系统级沙盒、分级审批、集中配置等企业功能，智能体循环以 Apache-2.0 开源，也方便接开源权重模型 | 模块 3 |
| [OpenCode](https://github.com/anomalyco/opencode) | 采用（第 35 期由评估改为采用） | 最主要的开源编程智能体之一，可定制、支持无界面 / 服务模式，适合作为企业级运行框架的底座，常与自托管的开源权重模型搭配；会话共享和协作能力仍不如同类 | 模块 3 |
| Claude Code 插件市场 | 试用（第 34 期；第 35 期未再列出，已泛化为上方的“智能体插件市场”） | 用插件给团队分发 Skills、命令等配置 | 模块 3、5 |
| Dev Containers | 试用（第 34 期；第 35 期未再列出） | 用容器给编程智能体提供隔离环境 | 模块 3 |
| [OpenSpec](https://github.com/Fission-AI/OpenSpec) | 试用（第 35 期由评估改为试用） | 轻量的规格驱动开发框架，适用于各种编程智能体；尤其擅长给已有代码库补写规格，每次改动都是对一份持续维护的规格的增量，智能体产出更可预期。规格文件仍要有人维护 | 模块 3（已收录） |
| [PageIndex](https://github.com/VectifyAI/PageIndex) | 评估（第 34 期；第 35 期未再列出） | 无向量、基于推理的长文档检索 | 模块 4（已收录） |
| [Agent Scan](https://www.thoughtworks.com/radar/tools/agent-scan)（[GitHub](https://github.com/snyk/agent-scan)） | 评估（第 34 期；第 35 期未再列出） | 扫描本机的 MCP 服务器和 Skills，发现提示注入、工具投毒、有毒数据流、硬编码密钥等风险；扫描时要把组件元数据发给 Snyk，误报率需在自己环境中验证。第 35 期在“有毒数据流分析”中提到已成功用它做分析 | 模块 6 安全实践 |
| Bloom | 评估（第 34 期；第 35 期未再列出） | Anthropic 推出的行为评估工具：按设定的目标行为自动生成大量测试对话，检测模型的谄媚、自保等倾向 | 模块 6 进阶 |
| **OpenClaw** | **谨慎**（第 34 期；第 35 期未再列出） | 开源的“超个人化 AI 助手”：接入日历、邮件、文件越多就越有用，权限也越集中，正是有毒数据流分析要防的模式；Thoughtworks 强调，大厂的同类产品也有同样的风险 | 了解风险即可；这类助手不要接入公司数据 |

## 三、平台

| 条目 | 分档 | 一句话 | 怎么用 |
| --- | --- | --- | --- |
| [LiteLLM](https://www.thoughtworks.com/radar/platforms/litellm)（[GitHub](https://github.com/BerriAI/litellm)） | 试用（第 35 期由语言与框架移到平台，分档不变） | 开源 AI 网关：支持 100 多家模型提供商，提供路由、协议转换、鉴权、预算和护栏；Thoughtworks 现在把它看作基础设施而不是库。没升到“采用”主要是安全原因：今年已报告 25 个以上 CVE，要及时打补丁；2026-03 还曾发生 PyPI 供应链投毒，见[官方说明](https://docs.litellm.ai/blog/security-update-march-2026)。用了某家独有的功能，又会重新绑定到这家 | 模块 6 进阶 |
| [Langfuse](https://www.thoughtworks.com/radar/platforms/langfuse)（[GitHub](https://github.com/langfuse/langfuse)） | 试用（第 34 期；第 35 期未再列出） | 开源 LLM 工程平台：追踪、提示管理、评估、数据集；SDK 基于 OpenTelemetry。自托管组件较多，先评估规模是否值得 | [应用路线模块 6](tracks/app-builder.md#模块-6--评估驱动的产品化第-1011-周) |
| AWS Bedrock AgentCore | 试用（第 34 期；第 35 期未再列出） | 云上的智能体运行平台；更成功的做法是只用它处理会话隔离、安全、可观测等生产问题，业务逻辑留在自己的代码里 | 模块 5 进阶 |
| AG-UI 协议 | 试用（第 34 期；第 35 期未再列出） | 统一前端界面和后端智能体之间的通信：流式推理步骤、状态同步、动态组件 | 模块 5 |
| Graphiti | 试用（第 34 期；第 35 期未再列出） | 带时间维度的知识图谱，记录事实何时生效、何时失效，用于智能体记忆 | 模块 4 进阶 |
| MCP Apps | 评估（第 34 期；第 35 期未再列出） | MCP 首个官方扩展，让 MCP 服务器在对话里返回交互式界面 | 模块 5 |
| Agent Trace | 评估（第 34 期；第 35 期未再列出） | Cursor 提出的开放规范，记录每一行代码是人写的还是 AI 写的 | 管理者路线模块 5（审计） |

## 四、语言与框架

| 条目 | 分档 | 一句话 | 怎么用 |
| --- | --- | --- | --- |
| [Docling](https://www.thoughtworks.com/radar/languages-and-frameworks/docling)（[GitHub](https://github.com/docling-project/docling)） | 试用（第 34 期；第 35 期未再列出） | 开源文档解析：PDF、扫描件转成 JSON / Markdown，可自托管，替代云厂商的文档识别服务 | [应用路线模块 4](tracks/app-builder.md#模块-4--知识库与-rag第-67-周) |
| [DeepEval](https://www.thoughtworks.com/radar/languages-and-frameworks/deepeval)（[GitHub](https://github.com/confident-ai/deepeval)） | 试用（第 34 期；第 35 期未再列出） | 开源评估框架：RAG 指标、自定义指标，以及工具调用正确性、任务完成度等智能体指标 | 模块 6 |
| [Promptfoo](https://www.thoughtworks.com/radar/languages-and-frameworks/promptfoo)（[GitHub](https://github.com/promptfoo/promptfoo)） | 试用（第 35 期新增） | 既做评估（含智能体工具调用和 CI 门禁），也做红队测试：描述应用用途、选定风险，它自动生成攻击并给回答打分，把手工试探变成每次修复后都能重跑的测试；可用来验证有状态护栏是否守得住。现属 OpenAI，仍为 MIT 许可；部分高级攻击依赖其托管服务，注意哪些数据会离开公司 | [应用路线模块 6](tracks/app-builder.md#模块-6--评估驱动的产品化第-1011-周)；[评估计划模板](templates/eval-plan.md) |
| [Presidio](https://www.thoughtworks.com/radar/languages-and-frameworks/presidio)（[GitHub](https://github.com/data-privacy-stack/presidio)） | 试用（第 35 期新增） | 识别并脱敏文本中的个人信息（姓名、卡号、地点等），支持自定义识别器，适合在数据共享管控严格的企业里把数据交给大模型之前先脱敏；不是百分之百可靠，可能漏识或误识 | 模块 6 安全实践；[员工 AI 使用规范](templates/ai-use-policy.md) |
| LangGraph | 试用（第 34 期；第 35 期未再列出） | 被移出“采用”：Thoughtworks 认为“有状态图 + 全局共享状态”不总是最好的做法，很多场景先用简单智能体、需要时再加图结构更精简 | 模块 5 |
| Agent Development Kit（ADK） | 试用（第 34 期；第 35 期未再列出） | Google 的智能体框架，部分功能仍未正式发布；同类还有 OpenAI Agents SDK、Claude Agent SDK、Microsoft Agent Framework 等 | 模块 5 |
| LangExtract | 试用（第 34 期；第 35 期未再列出） | 用大模型从非结构化文本中抽取结构化信息，每一项都能追溯到原文位置 | 模块 4 |
| GitHub Spec Kit | 评估（第 34 期；第 35 期未再列出） | 规格驱动开发工具，团队多在已有代码库中试用 | 模块 3 |
| Superpowers | 评估（第 34 期；第 35 期未再列出） | 由可组合 Skills 构成的编程智能体工作流 | 模块 3 |
| [Pipecat](https://github.com/pipecat-ai/pipecat) | 评估（第 34 期；第 35 期未再列出） | 开源语音与多模态智能体框架 | 模块 5 进阶（已收录） |
| Unsloth | 评估（第 34 期；第 35 期未再列出） | 开源微调与强化学习框架，显著降低显存和成本，消费级 GPU 也能微调 Llama、Qwen、DeepSeek 等开源模型 | 模块 6 进阶 |

---

## 五、这一期的四个主题

Thoughtworks 在第 35 期总结了四个主题：

1. **规模化的运行框架工程（harness engineering）。** 给智能体搭建的外围环境（记忆、上下文、反馈循环、护栏）正在成为一门成体系的学科，插件生态开始成形（智能体插件、插件市场、Agent Package Manager）。运行框架是需要持续维护的资产，要评估质量、让它自我改进、用反馈飞轮让智能体越用越好；下一步的难题是做成整个企业共用的运行框架。
2. **不只用前沿模型。** 开源权重模型与闭源前沿模型的差距一年来明显缩小，成本更低，还能部署在自己的云或硬件上，满足隐私要求、降低对单一厂商的依赖；本地编程模型、面向结构化数据的基础模型也在兴起。为每个任务选对模型、做模型路由，正在成为工程团队的职责，Thoughtworks 提醒不要“一律用前沿模型”。
3. **让更多智能体干活。** 上一期的焦点是编程智能体本身，这一期是开发者同时并行跑多个智能体会话、把更大的任务交给智能体整夜运行。多数 Thoughtworks 团队仍在自己直接掌控下跑多个会话，认为这是合适的起点。瓶颈随之转到人的注意力和评审能力上：评审跟不上，监督就会变成“人在回路的表演”；加会话之前，先看评审和交付流程能承受多少。
4. **建设 AI 工厂。** token 经济学归根结底是基础设施经济学：AI 的成本不只取决于模型单价，还取决于模型选择、路由、批处理、数据搬运和平台效率。Kubernetes 正在成为运行大规模 AI 负载的“AI 工厂”底座，模型、GPU、推理引擎、存储和网络越来越作为可编程资源由同一平台层统一调度。

第 34 期的四个主题（[原文 PDF](https://www.thoughtworks.com/content/dam/thoughtworks/documents/radar/2026/04/tr_technology_radar_vol_34_en.pdf)）可以概括为一句话：智能体时代评估技术本身变难、要保住老原则放弃套路、给“权限饥渴”的智能体上锁、用 Skills 和反馈传感器给编程智能体套上缰绳。

## 六、怎么用这张雷达

- **构建者**：选型时默认从“采用”和“试用”里挑；“评估”类只在小项目里试，并记录结论；每季度对照“谨慎”十二条自查一次。
- **管理者**：把“谨慎”十二条变成治理问题，在季度复盘时逐条问技术负责人。例如：我们是不是在用代码行数、PR 数或 AI 代码占比衡量 AI 提效？员工自己搭的智能体流程有没有登记？智能体改动的人工审批是真审还是走过场？是不是所有任务都默认用最贵的模型？
- **更新**：Thoughtworks 第 36 期（预计 2027 年春季）发布后，核对本文每个条目的分档变化，并在 [CHANGELOG](CHANGELOG.md) 记录。

> 相关：[2026 AI 最佳实践](best-practices-2026.md) · [AI 合规时间线](ai-regulation-tracker.md) · [资源总表](resources.md)
