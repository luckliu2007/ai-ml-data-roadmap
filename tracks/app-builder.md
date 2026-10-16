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

🛠️ 动手
- 选 5 个你工作中的真实任务（例如总结会议纪要、写 SQL、改合同条款），在 3 个不同模型上各跑一遍，记录质量、速度、成本。

📦 产出：一张“任务 × 模型”对比表，以及你自己的默认选型规则（什么任务用哪档模型）。

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
- Anthropic《[Claude Code best practices](https://code.claude.com/docs/en/best-practices)》：先探索、再计划、再编码、再验证的工作流，适用于所有编程智能体。
- 主流开源 / 官方编程智能体，任选一个上手：[Claude Code](https://github.com/anthropics/claude-code)、[OpenAI Codex CLI](https://github.com/openai/codex)、[Gemini CLI](https://github.com/google-gemini/gemini-cli)。

🛠️ 动手
- 做一个解决自己真实痛点的小工具，例如：批量整理文件、把 Excel 生成周报、一个内部查询网页。
- 刻意练习：先让智能体写计划，你审核后再执行；让它先写测试；每次只改一件事。

📦 产出：一个放在 GitHub 上的可运行小工具，README 写清楚用途、运行方式，以及“哪些部分 AI 写、哪些部分我改”。

✅ 自测：能独立判断 AI 生成的代码哪里可能出错，并让它修正。

---

## 模块 4 · 知识库与 RAG（第 6–7 周）

🎯 让模型基于**你的资料**回答，并给出处：检索增强生成（RAG）的原理、取舍与常见失败。

📖 必读
- [RAG_Techniques](https://github.com/NirDiamant/RAG_Techniques)：数十种进阶 RAG 技术的可运行 notebook，挑“分块、混合检索、重排序、评估”四节精读。
- [RAGFlow](https://github.com/infiniflow/ragflow)：开源 RAG 引擎，擅长复杂文档（PDF、表格）解析，可直接部署体验。
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
- [MCP 官方文档](https://modelcontextprotocol.io/) + [MCP For Beginners](https://github.com/microsoft/mcp-for-beginners)（微软，多语言示例）。
- [Agent Skills](https://github.com/anthropics/skills)：把指令、脚本和资源打包成智能体可按需加载的能力。
- 中文系统教程：[hello-agents《从零开始构建智能体》](https://github.com/datawhalechina/hello-agents)。

🛠️ 动手（三选一，建议都试）
- **低代码**：用 [n8n](https://github.com/n8n-io/n8n)、[Dify](https://github.com/langgenius/dify) 或 [Coze Studio](https://github.com/coze-dev/coze-studio) 搭一个“收到邮件 / 表单 → AI 分类摘要 → 写入表格 → 通知负责人”的流程。
- **代码**：用 [OpenAI Agents SDK](https://github.com/openai/openai-agents-python) 或任一框架写一个能调用 2–3 个工具的智能体。
- **MCP**：写一个最小 MCP 服务器，把你的一份数据（例如项目清单）接进 AI 助手。

📦 产出：一个可演示的工作流或智能体，附一页设计说明：为什么用工作流 / 智能体、工具权限边界、出错时如何人工接管。

✅ 自测：能对一个需求判断“用工作流就够了”还是“需要智能体”，并说出理由。

---

## 模块 6 · 评估驱动的产品化（第 10–11 周）

🎯 把 demo 变成产品：用评估集证明效果，用错误分析驱动改进，设计好人机协作体验。

📖 必读
- Hamel Husain《[LLM Evals FAQ](https://hamel.dev/blog/posts/evals-faq/)》+《[Your AI Product Needs Evals](https://hamel.dev/blog/posts/evals/)》。核心方法：
  1. 先亲自读 20–50 条真实记录做**错误分析**，再写自动化检查；
  2. 失败类型从数据中归纳，不预先拍脑袋定指标；
  3. 用**通过 / 不通过**的二元判断，而不是 1–5 分；
  4. 由一位领域专家定质量标准；
  5. 能用代码断言的就不用“大模型当裁判”，用了也要对照人工标注校准。
- [Google PAIR People + AI Guidebook](https://pair.withgoogle.com/guidebook/)：AI 产品的用户体验设计方法（信任、可解释、出错处理）。
- [Microsoft Guidelines for Human-AI Interaction](https://www.microsoft.com/en-us/haxtoolkit/ai-guidelines/)：18 条经过研究验证的人机交互设计准则。
- Chip Huyen《[AI Engineering](https://huyenchip.com/books/)》第 3–4 章（评估方法论）。

🛠️ 动手
- 给模块 4 或 5 的产出建一个 ≥50 条的评估集（用 [评估计划模板](../templates/eval-plan.md)），跑一轮基线。
- 做一轮错误分析 → 改进 → 重跑，记录通过率变化。
- 补齐产品化清单：成本估算、延迟、失败兜底、敏感信息处理、用户反馈入口。

📦 产出：评估集 + 两轮迭代的结果对比 + 一页上线检查清单。

✅ 自测：别人问“这个 AI 功能效果怎么样”时，你能拿出数字，并说清这些数字怎么来的。

---

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
