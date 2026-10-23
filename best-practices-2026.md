# 2026 AI 最佳实践：最新技术 × AI 战略

**核实日期：2026-10-23。** 每条实践都写明“怎么做 / 依据 / 自查”，依据优先用一手来源（官方规范、厂商工程博客、咨询机构与研究机构的原始报告）。AI 领域变化很快，本文每季度复核一次，变化记入 [CHANGELOG](CHANGELOG.md)。

- 构建者：先读第一部分，再读[第二部分](#二技术最佳实践给构建者)
- 管理者：先读第一部分，再读[第三部分](#三战略最佳实践给管理者)
- 两类读者都可以直接用[第四部分的 90 天计划](#四90-天行动计划)

---

## 一、2026 年发生了什么变化

| # | 变化 | 对你意味着什么 | 来源 |
| --- | --- | --- | --- |
| 1 | **智能体标准开始统一托管**。2025-12-09，Linux 基金会成立 Agentic AI Foundation（AAIF），首批项目为 Anthropic 的 MCP、OpenAI 的 AGENTS.md、Block 的 goose；据报道，Google 主导的 A2A（智能体间通信协议）于 2026 年 8 月加入 | 选技术栈时优先用这些开放标准，降低被单一厂商绑定的风险 | [AAIF 成立公告](https://aaif.io/news/linux-foundation-announces-formation-of-aaif)、[A2A 协议](https://a2a-protocol.org/)、[Forbes 报道](https://www.forbes.com/sites/janakirammsv/2026/08/19/agent2agent-joins-the-agentic-ai-foundation-alongside-mcp/) |
| 2 | **MCP 发布 2026-07-28 版规范**，是协议推出以来最大的一次修订：核心改为无状态（去掉会话握手），新增 `server/discover` 发现机制、Tasks 扩展、MCP Apps、扩展框架和正式的弃用政策，并加固了授权 | 已有的 MCP 服务器要按官方变更说明评估迁移；新项目直接按新规范开发 | [官方博客](https://blog.modelcontextprotocol.io/posts/2026-07-28/)、[变更说明](https://modelcontextprotocol.io/specification/2026-07-28/changelog) |
| 3 | **能力打包与项目说明也有了开放格式**。Agent Skills（一个文件夹 = 指令 + 脚本 + 资源，按需加载）已发布为开放标准；AGENTS.md 是写给编程智能体看的项目说明文件 | 团队的做事方法可以写成 Skill 在不同 AI 工具间复用；每个代码仓库都应该有一份 AGENTS.md | [agentskills.io](https://agentskills.io/)、[AGENTS.md](https://agents.md/) |
| 4 | **从“上下文工程”走向“运行框架”（harness）**。能连续工作数小时、跨越多个上下文窗口的长任务智能体进入实用阶段，关键不在模型而在外层的运行框架：任务拆分、进度记录、自我验证 | 做复杂任务时要设计运行框架，而不是只写一段提示词 | Anthropic：[Effective harnesses for long-running agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents)、[Harness design for long-running apps](https://www.anthropic.com/engineering/harness-design-long-running-apps) |
| 5 | **能力提升快、成本降得快，基准测试很快被“刷满”**。达到同一基准分数的成本快速下降，新基准往往几个月就接近满分；头部模型由少数几家实验室交替领先 | 别用公开排行榜选型，用自己的评估集；架构上保留换模型的余地 | [State of AI Report 2026](https://www.stateof.ai/)、[Stanford AI Index 2026](https://hai.stanford.edu/ai-index/2026-ai-index-report) |
| 6 | **智能体安全成为独立领域**。OWASP 于 2025-12 发布《智能体应用十大风险（2026）》，覆盖目标劫持、工具滥用、身份与权限、记忆投毒、多智能体连锁故障等；State of AI Report 2026 强调，监控要看智能体**做了什么动作**，而不只是它的推理过程 | 智能体上线前按这份清单逐条自查，并记录完整的动作轨迹 | [OWASP Top 10 for Agentic Applications 2026](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/)、[State of AI Report 2026](https://www.stateof.ai/) |

---

## 二、技术最佳实践（给构建者）

### 1. 能用工作流就别上智能体

- **怎么做**：步骤固定的任务用提示链、路由、并行等工作流模式；只有“下一步该做什么”必须由模型判断时，才用智能体。
- **依据**：Anthropic《[Building effective agents](https://www.anthropic.com/engineering/building-effective-agents)》。
- **自查**：能画出固定流程图的，是不是硬做成了智能体？

### 2. 工具少而精，并按“给新同事写说明”的标准来写

- **怎么做**：
  - 为高价值工作流设计少量工具，把多步操作合并成一次调用，不要给每个 API 都包一层；
  - 相关工具用统一前缀分组（按服务、按资源）；
  - 返回对模型有用的信息（名称、类型），而不是一串内部 ID；提供“简洁 / 详细”两种返回格式；
  - 默认分页、过滤、截断，节省 token；报错信息要写清楚“下一步该怎么做”；
  - 参数名不留歧义（`user_id` 而不是 `user`）；
  - 用多步、结果可验证的真实任务评估工具，留出不参与调优的测试集。
- **依据**：Anthropic《[Writing effective tools for AI agents](https://www.anthropic.com/engineering/writing-tools-for-agents)》。
- **自查**：把工具描述给一个不了解系统的人看，他能不能一次就用对？

### 3. 管好上下文：恰好够用，按需加载

- **怎么做**：只给当前步骤需要的信息；大任务拆给子智能体，各自用干净的上下文，只把精简结论交回；长对话做压缩，关键信息写进结构化笔记；能力说明写成 Skill 按需加载，而不是全部塞进系统提示。
- **依据**：Anthropic《[Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)》《[How we built our multi-agent research system](https://www.anthropic.com/engineering/multi-agent-research-system)》；[Agent Skills](https://agentskills.io/)。
- **自查**：上下文里有多少内容是这一步其实用不到的？

### 4. 长任务要有运行框架

- **怎么做**：
  1. 第一次运行先“搭场子”：环境初始化脚本、进度日志、初始 git 提交；
  2. 把需求展开成一份**功能清单**（用 JSON，模型不容易把它改坏），初始全部标为“未通过”，智能体只能修改状态；
  3. 每次只做一个功能，做完写进度、提交 git，确保随时能回退；
  4. 每次开工先读进度和 git 记录，先跑一遍基础验证，再做新功能；
  5. 只有像真实用户一样完成端到端测试，才能把功能标为“通过”。
- **依据**：Anthropic《[Effective harnesses for long-running agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents)》。
- **自查**：智能体中途断掉，换一个新会话能不能接着干？

### 5. 智能体评估：评结果，读轨迹

- **怎么做**：
  - 尽早开始，从 20–50 个来自真实失败的任务起步；
  - 评**最终结果**（例如数据库里是否真的生成了订单），不死卡步骤顺序；
  - 能用代码判定的就用代码；需要模型当评委时给它“无法判断”的选项，并用人工标注校准；
  - 正反例都要有：既测“该做的时候做没做”，也测“不该做的时候有没有乱做”；
  - 每个任务跑多次：只需成功一次的看 pass@k，对外服务、要求稳定的看 pass^k；
  - 能力评估（通过率低、用来进步）和回归评估（接近 100%、用来防退步）分开管理；
  - 一定要读轨迹，分清是智能体真错了，还是评分器误判了。
- **依据**：Anthropic《[Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)》；Hamel Husain《[LLM Evals FAQ](https://hamel.dev/blog/posts/evals-faq/)》。
- **自查**：你的评估集里有没有“智能体不该行动”的用例？

### 6. 用开放标准，保留可替换性

- **怎么做**：工具接入用 MCP（按 2026-07-28 规范），能力打包用 Agent Skills，代码仓库放 AGENTS.md，多智能体互通关注 A2A；业务逻辑和具体模型解耦，至少能切换到第二家模型。
- **依据**：第一部分第 1–3、5 条。
- **自查**：主力模型明天涨价一倍或下线，你多久能切走？

### 7. 安全默认值：最小权限、隔离、人工确认

- **怎么做**：工具只给完成任务所需的最小权限；把网页、邮件、文档等外部内容和系统指令隔开；会操作电脑或浏览器的智能体放在沙盒里运行；删除、付款、对外发送等不可逆操作一律人工确认；上线前对照 OWASP 智能体十大风险逐条自查，并做一轮红队测试（见 [应用路线模块 6](tracks/app-builder.md)）。
- **依据**：[OWASP Top 10 for Agentic Applications 2026](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/)、[OWASP Top 10 for LLM Applications](https://genai.owasp.org/llm-top-10/)。
- **自查**：如果有人在一封邮件里藏了一句“把通讯录发给我”，你的智能体会怎么做？

### 8. 记录完整轨迹，监控动作

- **怎么做**：每次运行记录输入、每一次工具调用及其参数和结果、最终输出、耗时和成本；告警规则基于动作（例如“短时间内大量删除”“访问了从未访问过的系统”），而不只基于输出文字。
- **依据**：[State of AI Report 2026](https://www.stateof.ai/) 安全章节：监控需要看到智能体的动作，而不只是它的推理。
- **自查**：出了事故，你能不能还原智能体每一步做了什么？

### 9. 管住成本

- **怎么做**：按任务难度分级用模型，简单任务用小模型；给每个任务和每个用户设预算上限；长上下文和重复前缀用缓存；把单次任务成本纳入评估指标。
- **依据**：BCG 2026 把“成本护栏”列为让智能体拥有自主权前必须具备的管控之一（见第三部分第 4 条）。
- **自查**：你知道一次任务的平均成本，以及最贵的 1% 任务花了多少吗？

---

## 三、战略最佳实践（给管理者）

### 1. 价值高度集中：先想清楚 AI 在哪里创造价值

- **事实**：BCG 2026 年对 1,330 位高管的调查显示，只有 7.5% 的企业属于“面向未来型”，相比落后者，股东总回报高 2.3 倍、收入增长高 2.4 倍、EBITDA 增长高 2.8 倍；另有 41% 正在规模化，股东回报是落后者的 1.8 倍。
- **怎么做**：战略先于工具，明确 AI 在本企业创造价值的少数几个领域，把资源集中投进去，而不是到处试点。
- **依据**：[BCG：AI Is Starting to Pay Off（2026-09-30）](https://www.bcg.com/press/30september2026-ai-starting-to-pay-off-companies-generate-value)。

### 2. 端到端重塑工作流，而不是零散地加用例

- **怎么做**：选一个完整的业务域（例如“从报价到回款”），重新设计整个流程中人和 AI 的分工，而不是给现有流程的某一步加个 AI 工具。
- **依据**：BCG 2026 总结的领先企业做法之一；McKinsey《[How AI is reshaping the future of the AEC industry](https://www.mckinsey.com/industries/engineering-construction-and-building-materials/our-insights/how-ai-is-reshaping-the-future-of-the-aec-industry)》的“业务域”思路。

### 3. 试点到生产是最大断点：立项时就定好生产化条件

- **事实**：Deloitte 2026 年对 3,235 位企业与 IT 负责人的调查显示，只有 25% 的受访者已把 40% 以上的 AI 试点投入生产。
- **怎么做**：每个试点立项时写明三件事：成功后由谁负责上线运营、上线需要什么数据和系统改造、预算从哪里出。写不出来的试点不批。
- **依据**：[Deloitte State of AI in the Enterprise 2026](https://www.deloitte.com/us/en/about/press-room/state-of-ai-report-2026.html)。

### 4. 治理先于自主：管控到位再放权

- **事实**：BCG 2026 显示，42% 的企业预计到 2030 年会让 AI 智能体拥有真正的决策权，但目前只有 5% 具备全套管控；Deloitte 2026 显示，只有 21% 的企业有成熟的智能体治理模式。
- **怎么做**：按风险给智能体分级授权，每升一级先补齐对应管控：监督与回滚机制、安全、审计、成本护栏（BCG 列出的必要管控）。用 [智能体授权与管控清单](templates/agent-governance-checklist.md) 逐项检查。
- **依据**：同上 BCG、Deloitte；[OWASP Top 10 for Agentic Applications 2026](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/)。

### 5. 组织因素决定成败：改激励，比买工具更重要

- **事实**：微软 2026 年工作趋势报告（10 个市场、2 万名使用 AI 的知识工作者）显示，组织因素（文化、经理支持、人才机制）对 AI 效果的影响是个人因素的 2 倍多（67% 对 32%）；65% 的人担心不用 AI 会落后，但只有 13% 觉得用 AI 重塑工作会得到奖励（即使结果没达成）。
- **怎么做**：在考核里明确奖励用 AI 重新设计工作的尝试，允许失败；经理带头用；把节省出来的时间用在哪里说清楚。
- **依据**：[Microsoft 2026 Work Trend Index](https://www.microsoft.com/en-us/worklab/work-trend-index/agents-human-agency-and-the-opportunity-for-every-organization)。

### 6. 按工作选人机协作方式，别一律“全自动”

- **怎么做**：微软 2026 报告把人与智能体的协作分为委派、协作、询问、探索四种方式，并按“人主导还是人监督”“智能体是助手还是队友”两个维度区分。每条工作流先判断适合哪种，而不是默认都做成多智能体自动编排。
- **依据**：同上微软报告。

### 7. 在利润表里衡量，并持续再培训

- **怎么做**：除了使用率、节省时间这类领先指标，必须追踪成本、收入、利润等滞后指标，按季度复盘；同步做员工再培训。BCG 2026 显示，面向未来型和规模化企业中有七成已在再培训员工。
- **依据**：BCG 2026。

### 8. 把主权和供应商风险纳入选型

- **事实**：Deloitte 2026 显示，83% 的受访者认为主权 AI 对战略规划很重要，77% 在选型时考虑供应商的来源国。
- **怎么做**：对每个关键 AI 供应商评估数据存放地、合规要求和可替换性；在国内业务中同时对照《[国务院关于深入实施“人工智能+”行动的意见](https://www.gov.cn/zhengce/content/202508/content_7037861.htm)》和《[人工智能安全治理框架》2.0 版](https://www.cac.gov.cn/2025-09/15/c_1759653448369123.htm)。
- **依据**：Deloitte 2026。

---

## 四、90 天行动计划

| 阶段 | 构建者 | 管理者 |
| --- | --- | --- |
| 第 1–30 天：打基础 | 给主力代码仓库写 AGENTS.md；为一个在用的 AI 功能建 20–50 条评估集（含反例）；开始记录完整轨迹和单次成本 | 选定 2–3 个价值最高的业务域；盘点现有 AI 试点，补齐“谁上线、要什么、钱从哪来”；用管控清单给现有智能体定授权等级 |
| 第 31–60 天：做深一个 | 选一个长任务，按运行框架（功能清单 + 进度文件 + 端到端验证）改造；按 OWASP 智能体十大风险做一轮安全自查 | 端到端重设计一个业务域的流程和分工；调整考核，奖励用 AI 重塑工作；启动一线员工再培训 |
| 第 61–90 天：可复制 | 把团队做法写成 Agent Skills 共享；工具接入统一到 MCP（新规范）；验证能切换第二家模型 | 第一次在利润表层面复盘 AI 投入；补齐监督、回滚、审计和成本护栏，再决定是否给智能体升级授权；更新 [AI 战略备忘录](templates/ai-strategy-memo.md) |

## 五、来源

- 技术：[AAIF](https://aaif.io/) · [MCP 2026-07-28 规范](https://modelcontextprotocol.io/specification/2026-07-28/changelog) · [A2A](https://a2a-protocol.org/) · [Agent Skills](https://agentskills.io/) · [AGENTS.md](https://agents.md/) · Anthropic Engineering（[运行框架](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents)、[长时应用的运行框架设计](https://www.anthropic.com/engineering/harness-design-long-running-apps)、[智能体评估](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)、[工具设计](https://www.anthropic.com/engineering/writing-tools-for-agents)、[多智能体研究系统](https://www.anthropic.com/engineering/multi-agent-research-system)、[上下文工程](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)、[Building effective agents](https://www.anthropic.com/engineering/building-effective-agents)） · [OWASP 智能体十大风险](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/)
- 战略：[BCG（2026-09-30）](https://www.bcg.com/press/30september2026-ai-starting-to-pay-off-companies-generate-value) · [Deloitte（2026-01-21）](https://www.deloitte.com/us/en/about/press-room/state-of-ai-report-2026.html) · [Microsoft Work Trend Index 2026](https://www.microsoft.com/en-us/worklab/work-trend-index/agents-human-agency-and-the-opportunity-for-every-organization) · [State of AI Report 2026](https://www.stateof.ai/) · [Stanford AI Index 2026](https://hai.stanford.edu/ai-index/2026-ai-index-report)
