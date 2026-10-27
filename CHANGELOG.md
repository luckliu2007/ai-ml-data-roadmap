# 更新日志

## 2026-10-27

- 资源总表“AI 编程智能体”新增 microsoft/apm（微软开源的智能体依赖管理器，统一声明 Skills / 插件 / MCP 服务器，MIT，已核实 2026-10 仍在更新）
- 资源总表“安全与红队测试”新增 Tencent/AI-Infra-Guard（腾讯朱雀实验室 AI 红队测试平台，Apache-2.0，有中文文档，已核实 2026-10 仍在更新）
- radar-ignore 新增 4 个工具/产品类候选（增量数据索引引擎、上下文网关工具、个人维护的 Skill 路由框架、企业知识库平台）

## 2026-10-26

- 资源总表“智能体、工具与工作流”新增 ai-boost/awesome-harness-engineering（智能体运行框架资料合集，Foundations 以一手文章为主，已核实 2026-10 仍在更新）
- 资源总表 OWASP Top 10 for LLM Applications 注明最新为 2026 年版（2026-08 发布），持续跟踪表同步更新
- radar-ignore 新增 7 个工具/产品类或不宜收录的候选（提示词优化工具、书籍蒸馏 Skill、3 个图像生成提示词库、知识图谱基础设施、自进化智能体工具）

## 2026-10-25

- 资源总表“AI 编程智能体”新增 github/awesome-copilot（GitHub 官方维护的 Copilot 智能体 / Instructions / Skills 合集，MIT，已核实 2026-10 仍在更新）
- 资源总表“知识库与 RAG”新增 VectifyAI/PageIndex（无向量、基于推理的树索引 RAG，MIT，有官方文档，已核实 2026-10 仍在更新）
- radar-ignore 新增 6 个工具/产品类或不宜收录的候选（与 RAGFlow 定位重复的知识库平台、个人维护的智能体循环模式库、大型 Skills 合集、学术研究 Skills、编程智能体工作流工具、提示词生成 Skill）

## 2026-10-24

- 资源总表“智能体、工具与工作流”新增 bojieli/ai-agent-book（《深入理解 AI Agent：设计原理与工程实践》开源书，Apache-2.0，10 章 + 109 个配套实验，已核实 2026-10 仍在更新）
- radar-ignore 新增 7 个工具/产品类或不宜收录的候选（多智能体编排工具、AI 辅导产品、泄露的系统提示词合集、敏捷开发方法框架、编程智能体加速工具、文件式规划 Skill、角色提示词合集）

## 2026-10-23 · 2026 AI 最佳实践（最新技术 × AI 战略）

- 新增 `best-practices-2026.md`：2026 年 6 项技术变化（AAIF 托管智能体标准、MCP 2026-07-28 规范、Agent Skills 与 AGENTS.md、长任务运行框架、能力与成本趋势、智能体安全），构建者 9 条与管理者 8 条最佳实践（每条附依据与自查），以及 90 天行动计划
- 新增 `templates/agent-governance-checklist.md`：智能体授权等级（A0–A3）与各等级必备管控
- 能力模型概念 5、6 更新为运行框架与开放标准；应用路线模块 3、5、6 加入 AGENTS.md、MCP 新规范、A2A、工具设计、长任务运行框架、智能体评估、OWASP 智能体十大风险；管理者路线模块 2、4、5、6 加入 BCG / Deloitte / 微软 2026 年报告与智能体管控
- 资源总表新增“2026 新标准与工程实践”一节；自测清单两条路线的 L3 各增加一项

## 2026-10-23

- 资源总表“AI 编程智能体”新增 Fission-AI/OpenSpec（规格驱动开发框架，MIT，100+ 贡献者，已核实 2026-10 仍在更新）
- radar-ignore 新增 7 个工具/产品类或与主题无关的候选（上下文压缩工具、学术写作 Skills、去 AI 痕迹改写、书籍转 Skill、图像提示词库、个人整理的 Claude Code 实践合集、智能体审计产品）

## 2026-10-22 · 安全实践、行业案例、中文一手资料（ROADMAP 全部完成）

- 应用路线模块 6 新增“安全实践与红队测试”：攻击面（OWASP、NIST AI 100-2 E2025、MITRE ATLAS）、官方防护指南（Anthropic、OpenAI、Google SAIF）、开源红队工具（promptfoo、garak、PyRIT、Inspect）、Microsoft AI Red Team
- 管理者路线模块 3 新增行业案例：WEF 全球灯塔网络、英格兰银行与 FCA 金融业 AI 调查、Google Cloud 用例汇编（注明厂商来源）
- 管理者路线模块 2、5 新增中文一手资料：“人工智能+”行动意见、《人工智能安全治理框架》2.0 版
- 资源总表新增“安全与红队测试”“行业落地案例”两节

## 2026-10-22 · 语音与电脑操作智能体

- 应用路线模块 5 新增进阶小节“语音与电脑操作智能体”：OpenAI Realtime、Gemini Live、Pipecat、LiveKit Agents、Claude Computer use、browser-use，并附这类智能体的安全要点
- 资源总表同步新增 6 项；雷达配置增加主题关键词过滤；radar-ignore 加入 NousResearch/hermes-agent（通用个人智能体产品，与课程模块无对应）

## 2026-10-22

- radar-ignore 新增 7 个工具/产品类候选（AI 网关、绘图 Skill、情报看板、视频渲染、代码评审工具、记忆系统、求职框架）；其中 OmniRoute、ai-job-search 是已忽略项目转移 owner 后的新地址

## 2026-10-21 · 全面规划升级

- 新增 `ROADMAP.md`（定位、待补强方向、维护机制）
- 两条路线加入 OWASP Top 10 for LLM Applications：应用路线模块 6 上线前安全自查，管理者路线模块 5 治理必读

## 2026-10-21（二）

- 资源总表“课程”新增 AI Engineering from Scratch（rohitg00，MIT，20 阶段 542 节可运行课程，已核实 2026-10 仍在更新）
- radar-ignore 新增 6 个工具/产品类候选（编程智能体周边工具、AI 网关、智能体编排平台）

## 2026-10-21

- 资源总表“智能体、工具与工作流”新增 DeepSeek Harness（DeepSeek 官方开源智能体框架，已核实官网 deepseek.com/harness 与仓库互相对应、仍在更新；星标增速异常，故不标星数）
- radar-ignore 新增 2 个与主题无关或存在平台条款风险的候选

## 2026-10-20

- 资源总表“AI 编程智能体”新增 addyosmani/agent-skills（覆盖规格到上线的工程流程 Skills，已核实仍在更新）
- radar-ignore 新增 2 个增长异常的候选

## 2026-10-19

- 资源总表“趋势与产业报告”新增 State of AI Report 2026（Air Street Capital，2026-10 发布，已核实官网可访问）
- radar-ignore 新增 4 个增长异常且与主题无关的候选

## [1.0.0] - 2026-10-16 · 首版

- 能力模型：两条路线共用的 8 个核心概念 + L1–L4 四级能力标准
- 应用构建者路线（12 周 6 模块）：模型选型、提示与上下文工程、AI 编程智能体、RAG、智能体与 MCP / Skills、评估驱动的产品化
- 管理者路线（8 周 6 模块）：能力与局限、产业影响、用例发现、试点到规模化、风险治理（中 / 欧 / 美）、AI 战略
- 模板：用例画布、评估计划、AI 战略备忘录、每周记录
- 自测清单与资源总表（50+ 项，均于 2026-10-16 核实）
- 每周链接检查 CI
