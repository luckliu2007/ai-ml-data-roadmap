# 2026 AI 最佳实践：最新技术 × AI 战略

**核实日期：2026-10-27。** 每条实践都写明“怎么做 / 依据 / 自查”，依据优先用一手来源（官方规范、厂商工程博客、咨询机构与研究机构的原始报告）。AI 领域变化很快，本文每季度复核一次，变化记入 [CHANGELOG](CHANGELOG.md)。

- 构建者：先读第一部分，再读[第二部分](#二技术最佳实践给构建者)（13 条）
- 管理者：先读第一部分，再读[第三部分](#三战略最佳实践给管理者)（11 条）
- 配套：[AI 技术雷达](tech-radar-2026.md)（该用什么、该警惕什么）、[AI 合规时间线](ai-regulation-tracker.md)（中国 / 欧盟 / 国际的关键日期）
- 两类读者都可以直接用[第四部分的 90 天计划](#四90-天行动计划)

---

## 一、2026 年发生了什么变化

| # | 变化 | 对你意味着什么 | 来源 |
| --- | --- | --- | --- |
| 1 | **智能体标准开始统一托管**。2025-12-09，Linux 基金会成立 Agentic AI Foundation（AAIF），首批项目为 Anthropic 的 MCP、OpenAI 的 AGENTS.md、Block 的 goose；A2A（智能体间通信协议）已于 2026-03 发布 1.0 版，据报道于 2026 年 8 月加入 AAIF | 选技术栈时优先用这些开放标准，降低被单一厂商绑定的风险 | [AAIF 成立公告](https://aaif.io/news/linux-foundation-announces-formation-of-aaif)、[A2A 协议](https://a2a-protocol.org/)（[版本发布](https://github.com/a2aproject/A2A/releases)）、[Forbes 报道](https://www.forbes.com/sites/janakirammsv/2026/08/19/agent2agent-joins-the-agentic-ai-foundation-alongside-mcp/) |
| 2 | **MCP 发布 2026-07-28 版规范**，是协议推出以来最大的一次修订：核心改为无状态（去掉会话握手），新增 `server/discover` 发现机制、Tasks 扩展、MCP Apps、扩展框架和正式的弃用政策，并加固了授权 | 已有的 MCP 服务器要按官方变更说明评估迁移；新项目直接按新规范开发 | [官方博客](https://blog.modelcontextprotocol.io/posts/2026-07-28/)、[变更说明](https://modelcontextprotocol.io/specification/2026-07-28/changelog) |
| 3 | **能力打包与项目说明也有了开放格式**。Agent Skills（一个文件夹 = 指令 + 脚本 + 资源，按需加载）已发布为开放标准；AGENTS.md 是写给编程智能体看的项目说明文件 | 团队的做事方法可以写成 Skill 在不同 AI 工具间复用；每个代码仓库都应该有一份 AGENTS.md | [agentskills.io](https://agentskills.io/)、[AGENTS.md](https://agents.md/) |
| 4 | **从“上下文工程”走向“运行框架”（harness）**。能连续工作数小时、跨越多个上下文窗口的长任务智能体进入实用阶段，关键不在模型而在外层的运行框架：任务拆分、进度记录、自我验证 | 做复杂任务时要设计运行框架，而不是只写一段提示词 | Anthropic：[Effective harnesses for long-running agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents)、[Harness design for long-running apps](https://www.anthropic.com/engineering/harness-design-long-running-apps) |
| 5 | **能力提升快、成本降得快，基准测试很快被“刷满”**。达到同一基准分数的成本快速下降，新基准往往几个月就接近满分；头部模型由少数几家实验室交替领先 | 别用公开排行榜选型，用自己的评估集；架构上保留换模型的余地 | [State of AI Report 2026](https://www.stateof.ai/)、[Stanford AI Index 2026](https://hai.stanford.edu/ai-index/2026-ai-index-report) |
| 6 | **智能体安全成为独立领域**。OWASP 于 2025-12 发布《智能体应用十大风险（2026）》，覆盖目标劫持、工具滥用、身份与权限、记忆投毒、多智能体连锁故障等；State of AI Report 2026 强调，监控要看智能体**做了什么动作**，而不只是它的推理过程 | 智能体上线前按这份清单逐条自查，并记录完整的动作轨迹 | [OWASP Top 10 for Agentic Applications 2026](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/)、[State of AI Report 2026](https://www.stateof.ai/) |
| 7 | **行业开始系统总结反模式**。Thoughtworks 技术雷达第 34 期（2026-04）把“默认使用 MCP”“智能体指令膨胀”“用代码产出量衡量生产率”“AI 加速的影子 IT”“忽视智能体工作流的持久性”等 7 项列为“谨慎”，把上下文工程、结构化输出、DORA 指标列为“采用” | 选型和治理时对照这份反模式清单自查 | [AI 技术雷达（本仓库）](tech-radar-2026.md)、[Thoughtworks 技术雷达](https://www.thoughtworks.com/radar) |
| 8 | **智能体安全从“审批每一步”转向“限制能接触什么”**。Anthropic 2026-05 公开的做法：用户对权限提示的同意率约 93%，逐条审批会疲劳，所以优先在环境层面限制（沙盒、网络出口管控、凭证不进沙盒）。Thoughtworks 指出，“私密数据 + 不可信内容 + 对外通信”三者同时具备，已是大多数有用智能体的默认状态 | 先设计隔离边界，再设计审批点；把凭证放在智能体够不着的地方 | Anthropic：[How we contain Claude across products](https://www.anthropic.com/engineering/how-we-contain-claude)；[Thoughtworks 雷达第 34 期](https://www.thoughtworks.com/content/dam/thoughtworks/documents/radar/2026/04/tr_technology_radar_vol_34_en.pdf) |
| 9 | **监管从原则走向细则**。中国 2026 年施行《网络安全法》AI 条款（1 月），印发《智能体规范应用与创新发展实施意见》（5 月，要求智能体执行操作不得超出用户授权范围），施行《人工智能拟人化互动服务管理暂行办法》（7 月）；欧盟“数字综合法案”2026-07 生效，高风险义务推迟到 2027-12 和 2028-08，但大部分透明度义务 2026-08 起已经适用 | 智能体分级授权从最佳实践变成政策要求；出海业务按新日期倒排合规计划 | [AI 合规时间线（本仓库）](ai-regulation-tracker.md) |

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
  - 工具很多时，不要把全部定义一次性塞进上下文：用工具搜索按需发现，或让模型写代码来调用工具，中间结果留在上下文之外（Anthropic 的测试中，工具搜索把工具定义占用的 token 降低约 85%）；复杂参数附上调用示例；
  - 用多步、结果可验证的真实任务评估工具，留出不参与调优的测试集。
- **依据**：Anthropic《[Writing effective tools for AI agents](https://www.anthropic.com/engineering/writing-tools-for-agents)》《[Introducing advanced tool use](https://www.anthropic.com/engineering/advanced-tool-use)》《[Code execution with MCP](https://www.anthropic.com/engineering/code-execution-with-mcp)》。
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
  - 一定要读轨迹，分清是智能体真错了，还是评分器误判了；
  - 运行环境也是变量：Anthropic 发现，仅基础设施配置不同，就能让 Terminal-Bench 2.0 分数相差最多 6 个百分点。记录资源配置，多次、分天运行；不到 3 个点的差距，配置对齐之前不要下结论。
- **依据**：Anthropic《[Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)》《[Quantifying infrastructure noise in agentic coding evals](https://www.anthropic.com/engineering/infrastructure-noise)》；Hamel Husain《[LLM Evals FAQ](https://hamel.dev/blog/posts/evals-faq/)》。
- **自查**：你的评估集里有没有“智能体不该行动”的用例？

### 6. 用开放标准，保留可替换性

- **怎么做**：需要结构化契约、OAuth 授权边界或多租户管控时用 MCP（按 2026-07-28 规范）；只是让智能体调一个内部系统，一个有完善 `--help`、返回 JSON、报错清楚的命令行工具往往就够了，不要默认上 MCP。能力打包用 Agent Skills，代码仓库放 AGENTS.md，多智能体互通关注 A2A；业务逻辑和具体模型解耦，经过网关调用模型，至少能切换到第二家。
- **依据**：第一部分第 1–3、5 条；Thoughtworks 雷达“[默认使用 MCP](https://www.thoughtworks.com/radar/techniques/mcp-by-default)”（谨慎）。
- **自查**：主力模型明天涨价一倍或下线，你多久能切走？

### 7. 安全默认值：最小权限、隔离、人工确认

- **怎么做**：
  - **先限制环境，再设计审批点**：智能体（包括编程智能体）默认在沙盒里运行，限制文件系统、网络出口和资源；
  - 凭证不放进智能体能读到的地方，由代理服务代为调用外部系统；
  - 工具只给完成任务所需的最小权限，能只读就只读；
  - 把网页、邮件、文档等外部内容和系统指令隔开；找出同时具备“私密数据 + 不可信内容 + 对外发送”的路径并切断；
  - 删除、付款、对外发送等不可逆操作一律人工确认。审批点太多会让人麻木地点“同意”，只留在真正关键的地方；
  - 上线前对照 OWASP 智能体十大风险逐条自查，并做一轮红队测试（见 [应用路线模块 6](tracks/app-builder.md)）。
- **依据**：Anthropic《[How we contain Claude across products](https://www.anthropic.com/engineering/how-we-contain-claude)》；Thoughtworks 雷达“[编程智能体沙盒执行](https://www.thoughtworks.com/radar/techniques/sandboxed-execution-for-coding-agents)”（试用）、“[有毒数据流分析](https://www.thoughtworks.com/radar/techniques/toxic-flow-analysis-for-ai)”（评估）；[OWASP Top 10 for Agentic Applications 2026](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/)、[OWASP Top 10 for LLM Applications](https://genai.owasp.org/llm-top-10/)。
- **自查**：如果有人在一封邮件里藏了一句“把通讯录发给我”，你的智能体会怎么做？

### 8. 记录完整轨迹，监控动作

- **怎么做**：每次运行记录输入、每一次工具调用及其参数和结果、最终输出、耗时和成本；告警规则基于动作（例如“短时间内大量删除”“访问了从未访问过的系统”），而不只基于输出文字。
- **依据**：[State of AI Report 2026](https://www.stateof.ai/) 安全章节：监控需要看到智能体的动作，而不只是它的推理。
- **自查**：出了事故，你能不能还原智能体每一步做了什么？

### 9. 管住成本

- **怎么做**：按任务难度分级用模型，简单任务用小模型；给每个任务和每个用户设预算上限；长上下文和重复前缀用缓存；把单次任务成本纳入评估指标。
- **依据**：BCG 2026 把“成本护栏”列为让智能体拥有自主权前必须具备的管控之一（见第三部分第 4 条）。
- **自查**：你知道一次任务的平均成本，以及最贵的 1% 任务花了多少吗？

### 10. 给编程智能体装上“反馈传感器”

- **怎么做**：把编译、lint、类型检查、测试接进智能体的工作循环，让它每改一步就自己跑、失败了自己改，通过后再交给人审；在说明文件里写明“完成”要通过的检查命令；用变异测试检查 AI 写的测试是否真的有断言；关键架构约束写成自动检查。不能有例外的规则（例如“不得修改某目录”）用 hooks 和权限强制执行，而不是写在说明里指望它遵守。
- **依据**：Thoughtworks 雷达“[编程智能体的反馈传感器](https://www.thoughtworks.com/radar/techniques/feedback-sensors-for-coding-agents)”（试用）、“变异测试”（试用）、“[代码库认知债](https://www.thoughtworks.com/radar/techniques/codebase-cognitive-debt)”（谨慎）；《[Claude Code best practices](https://code.claude.com/docs/en/best-practices)》：给它一个可以运行的检查，用 hooks 强制执行没有例外的规则。
- **自查**：智能体交来的代码，你是不是第一个发现它跑不通的人？

### 11. 说明文件要短、要手写、按需加载

- **怎么做**：AGENTS.md / CLAUDE.md 只写智能体从代码里看不出来的东西（构建和测试命令、关键约定、注意事项），定期删减（Claude Code 官方建议控制在 200 行以内）；较长的流程做成按需加载的 Skill；团队维护一份共享说明，放进新项目的脚手架模板；第三方 Skill 先审再用。
- **依据**：Thoughtworks 雷达“[智能体指令膨胀](https://www.thoughtworks.com/radar/techniques/agent-instruction-bloat)”（谨慎）、“[渐进式上下文披露](https://www.thoughtworks.com/radar/techniques/progressive-context-disclosure)”（试用）、“[团队共享的智能体说明](https://www.thoughtworks.com/radar/techniques/curated-shared-instructions-for-software-teams)”（采用）；《[Claude Code best practices](https://code.claude.com/docs/en/best-practices)》“Keep CLAUDE.md short”。
- **自查**：你的 AGENTS.md 有多少行？上次删减是什么时候？

### 12. 长流程要能断点续跑

- **怎么做**：跑几小时以上、或中途要等人审批的流程，用智能体框架自带的持久化执行保存进度和每一次工具调用；会话日志存在模型上下文之外，崩溃后从日志恢复；流程越关键，越要考虑 Temporal 等专门的持久化执行平台。
- **依据**：Thoughtworks 雷达“[忽视智能体工作流的持久性](https://www.thoughtworks.com/radar/techniques/ignoring-durability-in-agent-workflows)”（谨慎）；Anthropic《[Scaling Managed Agents](https://www.anthropic.com/engineering/managed-agents)》（2026-04）把智能体拆成会话日志、运行框架、沙盒三部分，任何一部分崩溃都可以替换，并从日志恢复。
- **自查**：任务跑到第 3 个小时网络断了，会发生什么？

### 13. 管好 AI 供应链

- **怎么做**：锁定依赖版本（SDK、网关、MCP 服务器、Skills、插件），升级前看变更说明；只从可信来源安装 Skills 和插件，上线前用扫描工具检查；开发机和 CI 上的密钥最小化，出事时能快速全部轮换。
- **依据**：2026-03-24，LiteLLM 有两个 PyPI 版本被投毒，会窃取凭证（[官方说明](https://docs.litellm.ai/blog/security-update-march-2026)）；Thoughtworks 雷达提醒，未经审查复用第三方 Skill 有严重的供应链风险，并把扫描工具 [Agent Scan](https://www.thoughtworks.com/radar/tools/agent-scan) 列为“评估”。
- **自查**：你用的某个 AI 依赖如果今天被投毒，你多久能知道？多久能轮换完所有密钥？

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

### 9. 衡量 AI 提效看交付结果，不看代码量

- **事实**：DORA 2025 年报告（近 5,000 名技术从业者）显示，采用 AI 已能提高软件交付吞吐量，但仍会增加交付的不稳定性；Thoughtworks 雷达把“用代码产出量衡量生产率”列为“谨慎”：用代码行数、PR 数考核，会催生大量审不过来的代码，评审周期反而变长。
- **怎么做**：研发团队用 DORA 指标（变更前置时间、部署频率、恢复时间、变更失败率、返工率）加“一次通过率”（AI 产出不用大改就能用的比例）衡量，按团队而不是按个人统计；非研发团队看业务结果（处理时长、差错率、客户满意度），不看“AI 使用次数”。
- **依据**：[DORA 2025 State of AI-assisted Software Development](https://dora.dev/research/2025/dora-report/)；Thoughtworks 雷达“[DORA 指标](https://www.thoughtworks.com/radar/techniques/dora-metrics)”（采用）、“[用代码产出量衡量生产率](https://www.thoughtworks.com/radar/techniques/coding-throughput-as-a-measure-of-productivity)”（谨慎）。

### 10. 把影子 AI 引进有护栏的沙盒

- **事实**：Thoughtworks 雷达把“AI 加速的影子 IT”列为“谨慎”：非技术人员已能用 AI 工具搭出复杂的智能体流程，缺乏治理就会带来安全风险和大量重复建设。
- **怎么做**：不要一禁了之。提供有监控的内部试验环境；发布清楚的使用规范（用[员工 AI 使用规范模板](templates/ai-use-policy.md)）；会被长期依赖、会动数据或会对外发送的流程，必须登记并转为正式系统。
- **依据**：Thoughtworks 雷达“[AI 加速的影子 IT](https://www.thoughtworks.com/radar/techniques/ai-accelerated-shadow-it)”（谨慎）；DORA 2025 把“清晰并广泛传达的 AI 政策”列为放大 AI 效果的七项基础能力之一。

### 11. AI 是放大器：先补地基，并预期 J 曲线

- **事实**：DORA 2025 的核心结论是，AI 在软件开发中的首要作用是“放大器”：放大高绩效组织的长处，也放大困难组织的问题；最大回报来自内部平台质量、工作流清晰度和团队协同，而不是工具本身。七项基础能力是：清晰并广泛传达的 AI 政策、健康的数据生态、AI 可访问的内部数据、扎实的版本控制、小批量工作、以用户为中心、高质量的内部平台。DORA 2026 年的 ROI 报告还指出，多数组织在获得长期回报之前，会先经历一段生产率下降（J 曲线）。
- **怎么做**：做 AI 预算时，同时列出数据治理、内部平台和流程改造的投入；对“投入后前几个月效果变差”有预期，提前约定评估时点，别在低谷期砍掉项目；ROI 测算做保守、中性、乐观三种情景。
- **依据**：[DORA 2025 报告](https://dora.dev/research/2025/dora-report/)、[DORA：ROI of AI-assisted Software Development](https://cloud.google.com/resources/content/dora-roi-of-ai-assisted-software-development)（J 曲线和三种情景的内容据 [InfoQ 报道](https://www.infoq.com/news/2026/05/dora-roi-ai-assisted-dev-report/)）。

---

## 四、90 天行动计划

| 阶段 | 构建者 | 管理者 |
| --- | --- | --- |
| 第 1–30 天：打基础 | 给主力代码仓库写一份精简的 AGENTS.md，并把测试、lint 接成智能体的反馈；为一个在用的 AI 功能建 20–50 条评估集（含反例）；开始记录完整轨迹和单次成本；锁定 AI 相关依赖的版本 | 选定 2–3 个价值最高的业务域；盘点现有 AI 试点，用[试点立项书](templates/pilot-charter.md)补齐“谁上线、要什么、钱从哪来”；用管控清单给现有智能体定授权等级；对照 [AI 合规时间线](ai-regulation-tracker.md)确认适用的规则和日期 |
| 第 31–60 天：做深一个 | 选一个长任务，按运行框架（功能清单 + 进度文件 + 端到端验证）改造，并支持断点续跑；智能体放进沙盒、凭证移出沙盒；按 OWASP 智能体十大风险做一轮安全自查 | 端到端重设计一个业务域的流程和分工；调整考核，奖励用 AI 重塑工作；启动一线员工再培训；发布[员工 AI 使用规范](templates/ai-use-policy.md)，开放有监控的试验环境 |
| 第 61–90 天：可复制 | 把团队做法写成 Agent Skills 共享；需要互通的工具接入统一到 MCP（新规范）；用[模型选型评分卡](templates/model-selection-scorecard.md)验证能切换第二家模型；按 [AI 事故响应手册](templates/ai-incident-runbook.md)演练一次 | 第一次在利润表层面复盘 AI 投入；研发提效改用 DORA 指标衡量；补齐监督、回滚、审计和成本护栏，再决定是否给智能体升级授权；更新 [AI 战略备忘录](templates/ai-strategy-memo.md) |

## 五、来源

- 技术：[AAIF](https://aaif.io/) · [MCP 2026-07-28 规范](https://modelcontextprotocol.io/specification/2026-07-28/changelog) · [A2A](https://a2a-protocol.org/) · [Agent Skills](https://agentskills.io/) · [AGENTS.md](https://agents.md/) · Anthropic Engineering（[运行框架](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents)、[长时应用的运行框架设计](https://www.anthropic.com/engineering/harness-design-long-running-apps)、[智能体评估](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)、[工具设计](https://www.anthropic.com/engineering/writing-tools-for-agents)、[多智能体研究系统](https://www.anthropic.com/engineering/multi-agent-research-system)、[上下文工程](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)、[Building effective agents](https://www.anthropic.com/engineering/building-effective-agents)、[高级工具调用](https://www.anthropic.com/engineering/advanced-tool-use)、[代码执行与 MCP](https://www.anthropic.com/engineering/code-execution-with-mcp)、[评估中的基础设施噪声](https://www.anthropic.com/engineering/infrastructure-noise)、[托管智能体架构](https://www.anthropic.com/engineering/managed-agents)、[智能体隔离](https://www.anthropic.com/engineering/how-we-contain-claude)） · [OWASP 智能体十大风险](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/) · [Thoughtworks 技术雷达第 34 期](https://www.thoughtworks.com/content/dam/thoughtworks/documents/radar/2026/04/tr_technology_radar_vol_34_en.pdf) · [LiteLLM 供应链事件说明](https://docs.litellm.ai/blog/security-update-march-2026)
- 战略：[BCG（2026-09-30）](https://www.bcg.com/press/30september2026-ai-starting-to-pay-off-companies-generate-value) · [Deloitte（2026-01-21）](https://www.deloitte.com/us/en/about/press-room/state-of-ai-report-2026.html) · [Microsoft Work Trend Index 2026](https://www.microsoft.com/en-us/worklab/work-trend-index/agents-human-agency-and-the-opportunity-for-every-organization) · [State of AI Report 2026](https://www.stateof.ai/) · [Stanford AI Index 2026](https://hai.stanford.edu/ai-index/2026-ai-index-report) · [DORA 2025](https://dora.dev/research/2025/dora-report/) · [DORA ROI 报告](https://cloud.google.com/resources/content/dora-roi-of-ai-assisted-software-development)
- 合规：见 [AI 合规时间线](ai-regulation-tracker.md)
