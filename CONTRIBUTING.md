# 贡献指南

欢迎补充资源或改进学习设计。参与前请先读 [行为准则](CODE_OF_CONDUCT.md)。

## 参与方式

| 你想做什么 | 怎么做 |
| --- | --- |
| 推荐一份资料 | 填 [推荐资源表单](https://github.com/luckliu2007/ai-ml-data-roadmap/issues/new?template=resource-suggestion.yml) |
| 报告失效链接 | 填 [失效链接表单](https://github.com/luckliu2007/ai-ml-data-roadmap/issues/new?template=broken-link.yml) |
| 指出数字、日期或法规条文有误 | 填 [内容勘误表单](https://github.com/luckliu2007/ai-ml-data-roadmap/issues/new?template=content-error.yml)，附官方原文链接 |
| 直接修改 | Fork 后新建分支，改完发 Pull Request，按 PR 模板自查 |

## 收录标准

1. **服务于某个模块的产出**：说明它放在哪条路线、哪个模块，解决什么问题。
2. **一手优先**：官方文档、标准原文、法规原文、权威报告优先于二手解读；只能找到转载的，要在文中注明来源性质。
3. **可核实**：GitHub 项目要仍在维护、未归档；引用的数据注明来源和发布日期。
4. **不重复**：同类已有更好的，就不再加。

## 写法

- 新增资源写进 [resources.md](resources.md) 对应分组，格式与同表现有条目一致：`| [名称](链接) | 路线 | 说明 | 语言 | 费用 |`，路线用 🛠️（应用构建者）/ 🧭（管理者）。
- 技术雷达条目以 Thoughtworks 原文和条目页为准，分档变化要注明期号。
- 每次改动在 [CHANGELOG.md](CHANGELOG.md) 记一条，写清改了哪个文件、依据是什么。

## 维护方式

链接由 Link Check 每周一检查；每天的[内容雷达](https://github.com/luckliu2007/content-radar)检查已收录项目的健康状况并发现候选，候选经人工核实后才会收录；[ROADMAP.md](ROADMAP.md) 的“持续跟踪”表记录年度报告、技术雷达和法规的下一次核对时机。
