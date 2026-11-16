<!-- markdownlint-disable MD013 -->

# Claude-BugHunter（elementalsouls/Claude-BugHunter）

- GitHub：<https://github.com/elementalsouls/Claude-BugHunter>
- 核查：2026-11-17（Asia/Shanghai）07 时段；7,394 stars / 1,145 forks / 19 open issues（含 PR）；仓库 ID `1229774092`。
- 热度：官方综合 / Python daily +1,057；首次建档，不是今日首发。
- 固定 main：`2f9a226d38d35d28d06f1ed63753799d498a2b3d`；插件清单 `2.1.0`；最新 Release [v2.1](https://github.com/elementalsouls/Claude-BugHunter/releases/tag/v2.1) 为 UTC 2026-06-05。当前目录树可数 83 个 skill、15 个 command，与 API 简介仍写 82 不同。
- 许可与证据：代码 MIT；方法、文档等内容 CC BY 4.0。静态核读相关材料，未安装、扫描目标或运行 Agent。

## 定位

面向已授权安全评估的 Claude Code 技能包，组合方法知识、范围约束、证据整理与报告流程。它包含可选 Python engagement engine；技能包、默认确定性映射和主动 Agent 测试是不同入口，不能笼统称为自动发现漏洞的模型。[固定 README](https://github.com/elementalsouls/Claude-BugHunter/blob/2f9a226d38d35d28d06f1ed63753799d498a2b3d/README.md)

## 用法

README 推荐宿主插件 marketplace 安装；另有复制安装和独立 `cbh` CLI。插件路径不自动提供 clone-only 的 `hunt` scaffold，CLI 也需单独安装。先固定版本并阅读安装器，在自有实验环境选择需要的入口；本轮未执行安装或测试命令。[安装说明](https://github.com/elementalsouls/Claude-BugHunter/blob/2f9a226d38d35d28d06f1ed63753799d498a2b3d/INSTALL.md)

复制安装器默认写入 `~/.claude/skills`、commands 与 shell helper，并可能向 shell rc 加 `source`；`--no-shell` 只跳过 rc 修改。`--all` 可扩展到多个宿主目录，`--burp-mcp` 另改 MCP 配置。跨宿主主要迁移知识层，slash commands 与 engine 编排仍有 Claude Code 专属部分。[安装器](https://github.com/elementalsouls/Claude-BugHunter/blob/2f9a226d38d35d28d06f1ed63753799d498a2b3d/scripts/install.sh)

## 原理

技能通过 `SKILL.md` 注入方法与检查表；engine 文档把默认路径描述为确定性 recon / 排序 / 映射，主动 hunt 才调用 Agent。无模型费用不表示没有网络活动：历史 URL 查询、现场抓取和探测仍会访问外部系统。[engine 设计](https://github.com/elementalsouls/Claude-BugHunter/blob/2f9a226d38d35d28d06f1ed63753799d498a2b3d/engine/README.md)

范围模块按 host / domain、通配、CIDR 或 regex 匹配，deny 优先、无匹配默认拒绝。裸域名规则也接纳子域；这是一项具体语义，不能只看“allowlist”字样。该模块不构成宿主进程、凭据或全部网络请求的隔离证明。[范围实现](https://github.com/elementalsouls/Claude-BugHunter/blob/2f9a226d38d35d28d06f1ed63753799d498a2b3d/engine/scope.py)

## 价值

可把研究过程中的范围、候选、验证和证据组织起来，减少材料散落。README 自述 681 条披露报告模式、其中 433 条逐条引用；本轮未核读全部案例，也未验证所谓 battle-tested 的外推范围。

更有用的是保留可证伪的评测：上游 2026-08-25 baseline 在三个 Juice Shop 题目上，skills-off / on 均为 3/3，中位轮数 2 / 3、费用 $0.178 / $0.254。作者明确指出天花板效应，结果只能支持该小样本的流程与费用观察，不能推出技能普遍无效或普遍提升能力。[历史 baseline](https://github.com/elementalsouls/Claude-BugHunter/blob/2f9a226d38d35d28d06f1ed63753799d498a2b3d/eval/BASELINE.md)

## 风险边界

- 仅对自有或明确授权资产使用；报告确认门与提示词不能代替授权范围，也不等于各网络组件均已受控。[安全政策](https://github.com/elementalsouls/Claude-BugHunter/blob/2f9a226d38d35d28d06f1ed63753799d498a2b3d/SECURITY.md)
- “read-only”是上游默认 Agent 行为约束，主动探测仍会造成请求与日志；可选 intrusive 行为、MCP、宿主工具和实际权限须单独管理。默认 mapping 也不能视为离线。
- 技能 lint 检结构及秘密 / 客户标识泄漏，上游明确说它不是恶意代码或 prompt injection 检测器；通过 lint 不证明安装内容可信。
- 稳定发行 v2.1 的说明仍为 71 skills，当前 main 已到 83；固定 tag 与跟随 main 不等价。API / 插件字段写 MIT 不覆盖内容：`*.py`、`*.sh` 等代码 MIT，Markdown、词表、规则等内容 CC BY 4.0。[代码许可](https://github.com/elementalsouls/Claude-BugHunter/blob/2f9a226d38d35d28d06f1ed63753799d498a2b3d/LICENSE)、[内容许可](https://github.com/elementalsouls/Claude-BugHunter/blob/2f9a226d38d35d28d06f1ed63753799d498a2b3d/LICENSE-CONTENT)
- 证据、状态与模型上下文可含目标信息；应先脱敏，再决定哪些内容能给外部模型。没有完成全仓安全审计、效果复现或全部引用核验。

## 补充建议

先用合成材料检查安装 diff、范围匹配、状态恢复与证据脱敏，再在隔离实验目标做小样本验证。评估时固定模型、预算、题目难度和 oracle，同时记录误报、失败、费用及未完成分母；扩大到陌生任务后再判断 skill 的增益。

## 参考资料

- [仓库 API](https://api.github.com/repos/elementalsouls/Claude-BugHunter)、[v2.1 发行](https://github.com/elementalsouls/Claude-BugHunter/releases/tag/v2.1)、[插件清单](https://github.com/elementalsouls/Claude-BugHunter/blob/2f9a226d38d35d28d06f1ed63753799d498a2b3d/.claude-plugin/plugin.json)。
- 本文固定 SHA 的 README、安装器、范围实现、安全政策、历史评测和两份许可见对应段落；统计基于完整目录树，内容核读为抽样。
