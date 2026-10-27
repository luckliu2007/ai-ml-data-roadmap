# 应用构建者路线（12 周）

**适合**：产品经理、业务骨干、独立开发者、想把 AI 用进工作流的工程师。会一点 Python 或愿意让 AI 编程智能体帮你写代码即可，不需要数学推导。

**终点**：交付一个**有评估集、真实用户在用、能说清效果数据**的 AI 应用（达到 [L3–L4](../framework.md#应用构建者路线)）。

每个模块的结构：🎯 目标 · 📖 必读（一手资料） · 🛠️ 动手 · 📦 产出 · ✅ 自测

---

## 模块 1 · 模型认知与选型（第 1 周）

🎯 理解主流模型的差异，学会按任务选模型，而不是“只用最出名的那个”。

📖 必读
- [Artificial Analysis](https://artificialanalysis.ai/)：独立第三方对各家模型质量、速度、价格的横向评测。
- [LMArena 排行榜](https://lmarena.ai/leaderboard)：基于大量真人盲评的模型排名。
- 各家官方文档的模型概览页（Claude / OpenAI / Gemini / DeepSeek / 通义千问），重点看上下文长度、价格、是否支持工具调用和多模态。
- 别忽略开源权重模型和小模型：Thoughtworks 技术雷达第 34 期把[小语言模型](https://www.thoughtworks.com/radar/techniques/small-language-models)列为“评估”，在摘要、基础编码等任务上，小模型的性价比已开始超过大模型；数据不能出境或必须本地部署时，开源权重模型往往是首选。

🛠️ 动手
- 选 5 个你工作中的真实任务（例如总结会议纪要、写 SQL、改合同条款），在 3 个不同模型上（至少一个开源权重模型或小模型）各跑一遍，用[模型选型评分卡](../templates/model-selection-scorecard.md)记录质量、稳定性、成本和延迟。

📦 产出：一张填好的模型选型评分卡，以及你自己的默认选型规则（什么任务用哪档模型、主模型出问题时切到哪个）。

✅ 自测：能解释为什么排行榜第一的模型，不一定适合你的任务。

---

## 模块 2 · 提示与上下文工程（第 2–3 周）

🎯 从“问一句”升级到“设计模型看到的全部信息”：角色、任务、约束、示例、参考资料、输出格式。

📖 必读
- Anthropic《[Prompt engineering overview](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/overview)》：官方提示工程指南，结构清楚、例子实用。
- OpenAI《[Prompt engineering](https://developers.openai.com/api/docs/guides/prompt-engineering)》：官方指南，可与上一篇对照着读。
- Anthropic《[Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)》：为什么“上下文工程”取代了“提示工程”成为核心能力，以及压缩、结构化笔记、子智能体等手法。
- 参考手册：[Prompt Engineering Guide](https://www.promptingguide.ai/)（[GitHub](https://github.com/dair-ai/Prompt-Engineering-Guide)，有中文版）。

🛠️ 动手
- 把模块 1 的 5 个任务各写成“生产级提示”：明确角色和目标、给 2–3 个示例、指定输出格式、写清楚“不知道时怎么办”。
- 对同一任务做 A/B：只改一个变量（加示例 / 加参考资料 / 改输出格式），记录效果差异。

📦 产出：一个**提示库**（Markdown 或表格），每条包含用途、提示正文、适用模型、已知失败情况。

✅ 自测：能说清“提示写得好”和“给对了上下文”分别解决什么问题。

---

## 模块 3 · AI 编程智能体（第 4–5 周）

🎯 用 AI 编程智能体把想法变成可运行的工具。这是 2025–2026 年对非专业开发者杠杆最大的能力。

📖 必读
- Anthropic《[Claude Code best practices](https://code.claude.com/docs/en/best-practices)》：三条主线是告诉它代码里看不到的信息（说明文件要短，建议 200 行以内）、给它一个可以运行的检查、用 hooks 和权限强制执行不能有例外的规则。思路适用于所有编程智能体。
- [AGENTS.md](https://agents.md/)：写给编程智能体看的项目说明文件（开放格式，现由 AAIF 托管）：项目结构、构建和测试命令、代码规范。不管用哪家编程智能体，每个仓库都应该有一份。
- Thoughtworks 技术雷达第 34 期的编程智能体实践（汇总见本仓库 [AI 技术雷达](../tech-radar-2026.md)）：[反馈传感器](https://www.thoughtworks.com/radar/techniques/feedback-sensors-for-coding-agents)（把编译、lint、测试接进智能体的工作循环，试用）、[沙盒执行](https://www.thoughtworks.com/radar/techniques/sandboxed-execution-for-coding-agents)（默认在隔离环境里运行，试用）、[智能体指令膨胀](https://www.thoughtworks.com/radar/techniques/agent-instruction-bloat)（说明越写越长，规则反而被忽略，谨慎）。想先写规格再让智能体实现，可以试 [OpenSpec](https://github.com/Fission-AI/OpenSpec) 或 [GitHub Spec Kit](https://github.com/github/spec-kit)。
- 主流开源 / 官方编程智能体，任选一个上手：[Claude Code](https://github.com/anthropics/claude-code)、[OpenAI Codex CLI](https://github.com/openai/codex)、[Gemini CLI](https://github.com/google-gemini/gemini-cli)。

🛠️ 动手
- 做一个解决自己真实痛点的小工具，例如：批量整理文件、把 Excel 生成周报、一个内部查询网页。
- 刻意练习：先让智能体写计划，你审核后再执行；让它先写测试；每次只改一件事。
- 给这个小工具的仓库写一份 AGENTS.md，再让智能体按它工作，对比有没有这份说明时的差别。
- 把测试和 lint 命令写进 AGENTS.md，让智能体每次改完自己跑、失败了自己修；在容器（如 Dev Containers）或工具自带的沙盒模式里运行它。

📦 产出：一个放在 GitHub 上的可运行小工具，README 写清楚用途、运行方式，以及“哪些部分 AI 写、哪些部分我改”。

✅ 自测：能独立判断 AI 生成的代码哪里可能出错，并让它修正。

---

## 模块 4 · 知识库与 RAG（第 6–7 周）

🎯 让模型基于**你的资料**回答，并给出处：检索增强生成（RAG）的原理、取舍与常见失败。

📖 必读
- [RAG_Techniques](https://github.com/NirDiamant/RAG_Techniques)：数十种进阶 RAG 技术的可运行 notebook，挑“分块、混合检索、重排序、评估”四节精读。
- [RAGFlow](https://github.com/infiniflow/ragflow)：开源 RAG 引擎，擅长复杂文档（PDF、表格）解析，可直接部署体验。
- [Docling](https://github.com/docling-project/docling)：开源文档解析库，把 PDF、扫描件转成结构化的 Markdown / JSON，可自托管，Thoughtworks 雷达列为“试用”。RAG 答得好不好，很大程度取决于文档解析得好不好。
- 权限：知识库里的资料有查看权限之分时，建索引时就给每个文本块打上权限标签，检索时按用户身份过滤，模型根本拿不到无权查看的内容（Thoughtworks 雷达“RAG 中按角色隔离上下文”，评估）。
- Chip Huyen《AI Engineering》（O'Reilly，2025）第 6 章（RAG 与智能体）。[书籍资源仓库](https://github.com/chiphuyen/aie-book)。

🛠️ 动手
- 用你部门的 20–50 份真实文档搭一个问答助手（用 RAGFlow、Dify 或自己写代码均可）。
- 准备 30 个真实问题和标准答案，统计：答对率、引用是否正确、“答不出时是否承认不知道”。

📦 产出：一个知识库问答助手 + 一份失败案例分析（至少归纳 3 类失败原因：没检索到 / 检索到但答错 / 资料本身有冲突）。

✅ 自测：遇到“答错了”能定位是检索问题还是生成问题。

---

## 模块 5 · 智能体、工具与工作流（第 8–9 周）

🎯 掌握“工作流 vs 智能体”的选择，会用 MCP 接工具、用 Skills 打包能力、用低代码平台搭流程。

📖 必读
- Anthropic《[Building effective agents](https://www.anthropic.com/engineering/building-effective-agents)》：最被广泛引用的智能体设计文章，提炼出提示链、路由、并行、编排者-执行者、评估者-优化者五种工作流模式，核心建议是“能用简单方案就别上智能体”。
- OpenAI《[A practical guide to building agents](https://cdn.openai.com/business-guides-and-resources/a-practical-guide-to-building-agents.pdf)》：从选模型、定义工具、写指令到护栏设计的实操指南。
- [12-Factor Agents](https://github.com/humanlayer/12-factor-agents)：把智能体做成可靠软件的 12 条原则。
- Anthropic《[Writing effective tools for AI agents](https://www.anthropic.com/engineering/writing-tools-for-agents)》：工具少而精、按工作流设计、返回高信号信息、把工具描述当提示词来写。
- Anthropic《[Introducing advanced tool use](https://www.anthropic.com/engineering/advanced-tool-use)》《[Code execution with MCP](https://www.anthropic.com/engineering/code-execution-with-mcp)》：工具多了以后，用工具搜索按需加载定义，让模型写代码来调用工具、把中间结果留在上下文之外，可以大幅减少 token 消耗。
- Anthropic《[Effective harnesses for long-running agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents)》：长任务智能体的运行框架：功能清单、进度文件、一次只做一个功能、端到端验证后才算完成。
- [MCP 官方文档](https://modelcontextprotocol.io/) + [MCP For Beginners](https://github.com/microsoft/mcp-for-beginners)（微软，多语言示例）。按 [2026-07-28 版规范](https://modelcontextprotocol.io/specification/2026-07-28/changelog)开发：这一版改为无状态核心，旧的 HTTP+SSE 传输已弃用。多个智能体之间互相调用，看 [A2A 协议](https://a2a-protocol.org/)。Thoughtworks 雷达提醒[不要默认使用 MCP](https://www.thoughtworks.com/radar/techniques/mcp-by-default)：一个有完善 `--help`、返回 JSON 的命令行工具往往就够了，需要结构化契约、OAuth 授权或多租户管控时再上 MCP。
- [Agent Skills](https://github.com/anthropics/skills)：把指令、脚本和资源打包成智能体可按需加载的能力。格式已发布为开放标准，见 [agentskills.io](https://agentskills.io/)。
- 中文系统教程：[hello-agents《从零开始构建智能体》](https://github.com/datawhalechina/hello-agents)。

🛠️ 动手（三选一，建议都试）
- **低代码**：用 [n8n](https://github.com/n8n-io/n8n)、[Dify](https://github.com/langgenius/dify) 或 [Coze Studio](https://github.com/coze-dev/coze-studio) 搭一个“收到邮件 / 表单 → AI 分类摘要 → 写入表格 → 通知负责人”的流程。
- **代码**：用 [OpenAI Agents SDK](https://github.com/openai/openai-agents-python) 或任一框架写一个能调用 2–3 个工具的智能体。框架选择上，Thoughtworks 雷达把 [LangGraph](https://github.com/langchain-ai/langgraph)、[Google ADK](https://github.com/google/adk-python) 列为“试用”，并提醒很多场景先用简单智能体、需要时再加图结构；任务会跑很久的，选支持持久化执行（断点续跑）的框架。
- **MCP**：写一个最小 MCP 服务器，把你的一份数据（例如项目清单）接进 AI 助手。

📦 产出：一个可演示的工作流或智能体，附一页设计说明：为什么用工作流 / 智能体、工具权限边界、出错时如何人工接管、中途失败如何恢复。

✅ 自测：能对一个需求判断“用工作流就够了”还是“需要智能体”，并说出理由。

### 进阶（可选）：语音与电脑操作智能体

文字智能体做顺之后，可以往两个方向扩展：**实时语音**（电话客服、口语陪练、会议助手）和**操作电脑 / 浏览器**（自动填表、跨系统搬运数据）。

| 方向 | 资源 | 说明 |
| --- | --- | --- |
| 实时语音 | [OpenAI Realtime API 指南](https://developers.openai.com/api/docs/guides/realtime)、[Gemini Live API](https://ai.google.dev/gemini-api/docs/live-api) | 官方文档：低延迟的语音进、语音出，支持打断和工具调用 |
| 实时语音 | [Pipecat](https://github.com/pipecat-ai/pipecat)（约 1.7 万星）、[LiveKit Agents](https://github.com/livekit/agents)（约 1.5 万星） | 开源框架：把语音识别、大模型、语音合成和电话 / WebRTC 串成可上线的语音智能体 |
| 操作电脑 | [Claude Computer use 工具文档](https://platform.claude.com/docs/en/agents-and-tools/tool-use/computer-use-tool) | 官方文档：让模型看屏幕截图、移动鼠标、敲键盘 |
| 操作浏览器 | [browser-use](https://github.com/browser-use/browser-use)（约 12 万星） | 开源库：让智能体打开网页、点击、填表、提取信息 |

⚠️ **这类智能体的风险明显更高**：
- 语音会带来误识别和身份冒用问题。涉及转账、改密码等敏感操作时，一律要求二次确认或转人工。
- 操作电脑和浏览器的智能体会读取网页内容，而网页里可能藏着恶意指令（提示注入）。务必放在隔离的虚拟机或沙盒里运行，只给完成任务所需的最小权限，对照 [OWASP Top 10 for LLM Applications](https://genai.owasp.org/llm-top-10/) 自查。

---

## 模块 6 · 评估驱动的产品化（第 10–11 周）

🎯 把 demo 变成产品：用评估集证明效果，用错误分析驱动改进，设计好人机协作体验。

📖 必读
- Hamel Husain《[LLM Evals FAQ](https://hamel.dev/blog/posts/evals-faq/)》+《[Your AI Product Needs Evals](https://hamel.dev/blog/posts/evals/)》。核心方法：
- Anthropic《[Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)》：智能体评估的专门方法：评最终结果而不是死卡步骤，正反例平衡，多次运行看 pass@k 和 pass^k，能力评估和回归评估分开，一定要读轨迹。
  1. 先亲自读 20–50 条真实记录做**错误分析**，再写自动化检查；
  2. 失败类型从数据中归纳，不预先拍脑袋定指标；
  3. 用**通过 / 不通过**的二元判断，而不是 1–5 分；
  4. 由一位领域专家定质量标准；
  5. 能用代码断言的就不用“大模型当裁判”，用了也要对照人工标注校准。
- [Google PAIR People + AI Guidebook](https://pair.withgoogle.com/guidebook/)：AI 产品的用户体验设计方法（信任、可解释、出错处理）。
- [Microsoft Guidelines for Human-AI Interaction](https://www.microsoft.com/en-us/haxtoolkit/ai-guidelines/)：18 条经过研究验证的人机交互设计准则。
- [OWASP Top 10 for LLM Applications](https://genai.owasp.org/llm-top-10/)：大模型应用最常见的 10 类安全风险（提示注入、敏感信息泄露、过度授权的智能体等）及防护措施。上线前逐条自查。
- Chip Huyen《[AI Engineering](https://huyenchip.com/books/)》第 3–4 章（评估方法论）。

🛠️ 动手
- 给模块 4 或 5 的产出建一个 ≥50 条的评估集（用 [评估计划模板](../templates/eval-plan.md)），跑一轮基线。
- 做一轮错误分析 → 改进 → 重跑，记录通过率变化。
- 补齐产品化清单：成本估算、延迟、失败兜底、敏感信息处理、用户反馈入口；对照 OWASP LLM Top 10 做一次安全自查（重点：提示注入、工具权限、输出中的敏感信息）。

📦 产出：评估集 + 两轮迭代的结果对比 + 一页上线检查清单。

✅ 自测：别人问“这个 AI 功能效果怎么样”时，你能拿出数字，并说清这些数字怎么来的。

### 进阶（上线前必做）：安全实践与红队测试

评估回答“效果好不好”，安全测试回答“会不会被人故意弄坏”。上线前至少做一轮：

| 步骤 | 资源 | 做什么 |
| --- | --- | --- |
| 1. 了解攻击面 | [OWASP Top 10 for LLM Applications](https://genai.owasp.org/llm-top-10/)、[OWASP 智能体应用十大风险（2026）](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/)、[NIST AI 100-2 E2025 对抗性机器学习分类](https://csrc.nist.gov/pubs/ai/100/2/e2025/final)、[MITRE ATLAS](https://atlas.mitre.org/) | 弄清提示注入、越狱、数据泄露、模型投毒等攻击方式分别是什么 |
| 2. 按官方指南加防护 | [Anthropic：缓解越狱与提示注入](https://platform.claude.com/docs/en/test-and-evaluate/strengthen-guardrails/mitigate-jailbreaks)、[OpenAI：安全最佳实践](https://developers.openai.com/api/docs/guides/safety-best-practices)、[Google SAIF](https://saif.google/) | 输入过滤、输出审核、把外部内容和系统指令隔开、最小工具权限、人工复核 |
| 3. 自动化红队测试 | [promptfoo](https://github.com/promptfoo/promptfoo)（约 2.6 万星）、[garak](https://github.com/NVIDIA/garak)（NVIDIA，约 1 万星）、[PyRIT](https://github.com/microsoft/PyRIT)（微软）、[Inspect](https://github.com/UKGovernmentBEIS/inspect_ai)（英国 AI 安全研究所） | 用开源工具批量生成攻击样本，跑出失败案例，补进评估集 |
| 4. 学习红队方法 | [Microsoft AI Red Team](https://learn.microsoft.com/en-us/security/ai-red-team/) | 微软 AI 红队公开的方法、培训材料和经验总结 |

⚠️ 只测试你自己的应用或已获授权的系统。

📦 产出（追加）：一份安全测试记录，包括测了哪些攻击类型、发现了什么、怎么修的，以及修复后重跑的结果。

### 进阶（上线前建议做）：结构化输出、可观测性与网关

| 主题 | 资源 | 做什么 |
| --- | --- | --- |
| 结构化输出 | [Instructor](https://github.com/567-labs/instructor)、[Pydantic AI](https://github.com/pydantic/pydantic-ai) | Thoughtworks 雷达“[采用](https://www.thoughtworks.com/radar/techniques/structured-output-from-llms)”：程序要用模型输出时，约束成 JSON Schema，并自动校验和重试 |
| 追踪与可观测 | [OpenTelemetry GenAI 语义约定](https://github.com/open-telemetry/semantic-conventions-genai)、[Langfuse](https://github.com/langfuse/langfuse)、[Arize Phoenix](https://github.com/Arize-ai/phoenix) | 记录每次模型调用和工具调用的输入输出、成本、延迟。用 OpenTelemetry 标准埋点，以后换工具不用重写；GenAI 约定目前仍是 Development 状态，字段可能改名，要固定版本 |
| AI 网关 | [LiteLLM](https://github.com/BerriAI/litellm) | 多家模型统一接入、故障切换、预算控制、访问控制和数据脱敏（雷达“试用”）。锁定版本：2026-03 曾有两个 PyPI 版本被投毒 |
| 评估框架 | [DeepEval](https://github.com/confident-ai/deepeval)、[promptfoo](https://github.com/promptfoo/promptfoo) | 把评估集写成能在 CI 里自动跑的测试；DeepEval 有工具调用正确性、任务完成度等智能体指标（雷达“试用”） |
| 评估环境 | Anthropic《[Quantifying infrastructure noise in agentic coding evals](https://www.anthropic.com/engineering/infrastructure-noise)》 | 资源配置不同，智能体评估分数可差 6 个百分点；记录配置、多次运行，不到 3 个点的差距别急着下结论 |
| 微调（按需） | [Unsloth](https://github.com/unslothai/unsloth) | 提示和 RAG 都试过仍达不到要求、又有足够的标注数据时，再考虑微调开源模型（雷达“评估”） |

📦 产出（追加）：一个追踪看板，能看到单次任务成本、P95 延迟和失败率，并能点开任意一次运行的完整轨迹。

---

> 2026 年构建者最佳实践的完整清单（工具设计、上下文、运行框架、智能体评估、开放标准、安全、可观测、成本、反馈传感器、说明文件、断点续跑、供应链）见 [2026 AI 最佳实践](../best-practices-2026.md#二技术最佳实践给构建者)；该用什么、该警惕什么见 [AI 技术雷达](../tech-radar-2026.md)。

## 毕业项目（第 12 周）

把前面的某个产出推到真实用户手里（同事、团队或客户），运行至少 2 周：

- 有 ≥50 条评估样本，每次改动都重跑；
- 有使用量、成功率、成本三个基础指标；
- 有一次基于真实失败案例的改进记录；
- 写一篇复盘：做对了什么、低估了什么、下一步是什么。

完成后用 [self-assessment.md](../self-assessment.md) 复测，目标 L3，争取 L4。

## 参考课程（按需补充）

| 资源 | 用途 |
| --- | --- |
| [DeepLearning.AI 课程](https://www.deeplearning.ai/courses) | 大量 1–2 小时的免费短课：智能体、RAG、评估、MCP 等，适合按模块补课 |
| [Generative AI for Beginners](https://github.com/microsoft/generative-ai-for-beginners) | 微软 21 课，系统入门 |
| [Claude Cookbooks](https://github.com/anthropics/claude-cookbooks) | 官方可运行示例：工具调用、RAG、多模态、智能体 |
| [llm-cookbook](https://github.com/datawhalechina/llm-cookbook) | Datawhale 中文版吴恩达大模型系列课程 |
