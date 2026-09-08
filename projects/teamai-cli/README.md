<!-- markdownlint-disable MD013 MD034 -->

# teamai-cli（Tencent/teamai-cli）

> 记录日期：2026-09-09（Asia/Shanghai）。本页依据上游中英文 README、usage guide、release、LICENSE 与 GitHub REST API 做静态整理；本轮未安装 npm 包、未连接团队仓库、未注入 hooks / MCP / skills，也未验证跨宿主同步、隐私清理或知识召回效果。

## 定位

`teamai-cli` 是腾讯开源的团队级 agent harness 管理器：用一个 Git 仓库分发 skills、rules、docs、env、agents、hooks 与 MCP 配置，并在 Claude Code、Codex、Cursor、CodeBuddy、WorkBuddy、OpenCode 等宿主间同步。它还覆盖 session learning、BM25 + graph-boost recall、代码知识图谱、团队 usage digest 与 dashboard。

2026-09-09 的 GitHub 官方 TypeScript Trending 抓取显示约 `+1,215 stars today`；REST API 快照为 `2,311 stars / 153 forks / 26 open issues`，最新 release 为 `v0.23.0`（2026-09-08）。API 许可证字段为 `NOASSERTION`，但根 LICENSE 明确给出 MIT 文本；自动化和选型记录应保留这一区别。

## 用法

上游最小入口为：

```bash
npm install -g teamai-cli
cd /path/to/my-project
teamai init https://github.com/yourorg/your-teamai-repo
```

`teamai init` 默认按项目范围安装，也可用 `--scope user` 写入用户范围。管理员 / 独立用户先准备有明确写权限的共享仓库，成员再通过 `teamai pull`、`teamai push`、`teamai status`、`teamai recall`、`teamai doctor` 等命令协作。首次试用应优先使用临时组织、测试仓库和 `--dry-run`，不要直接指向团队所有生产项目。

## 原理

- **Git-native 分发**：成员 push 资源到分支 / MR，经 review merge 后，由 SessionStart hook 拉取到各宿主的原生目录。
- **角色、标签与来源**：管理员可按 role/namespace、tag 和订阅 source 控制成员收到哪些 skills / rules。
- **Hooks 与 MCP 注入**：共享 YAML 被转换为各 AI 工具的 hook / MCP 配置；环境变量占位符用于传递 secret 名称。
- **经验沉淀**：Stop hook 按中断、拒绝、重试等 friction 信号提示分享 learning；session save 与 digest 汇总团队使用记录。
- **知识召回**：recall 默认关闭，启用后会部署 subagent，以 BM25 和代码图谱加权检索团队知识。
- **代码图谱**：TypeScript/JavaScript、Python、Go 优先走 WASM tree-sitter，其他语言或失败场景走 heuristic fallback，并记录 gap。

## 价值

- 解决团队在多个 coding-agent 产品之间重复维护规则、skills 与 MCP 的配置漂移。
- 以 Git/MR 留下资源版本、review 和回滚线索，比口头复制 prompt 更可审计。
- 把 session friction、代码结构和团队知识接入后续任务，减少每个 agent 从零探索。
- 角色与标签给大团队提供比“所有人同步全部能力”更细的分发入口。

## 风险边界

- `teamai pull` 可向项目级或用户级 agent 目录注入 skills、hooks、agents、MCP 与包；共享仓库被入侵会放大为团队级 prompt / execution 供应链事件。
- SessionStart 自动拉取提高一致性，也可能在开发者未审阅新 diff 时改变 agent 行为；Git review 不等于签名、sandbox 或最小权限。
- Hook command、MCP endpoint、外部 source 与 npm / plugin 安装都可能执行代码、访问网络或接触凭据，必须分别设 allowlist。
- “privacy-scrubbed”与 friction scoring 是上游设计声明；本页未用 canary secret 验证 transcript、dashboard、monthly log 或远端仓库中的残留。
- 知识图谱的 heuristic fallback、过期 learning 和自动 recall 可能把错误上下文放大到多个项目。
- API `NOASSERTION` 与根 MIT LICENSE 的差异说明不能只依赖单一元数据字段；第三方订阅 source 仍可能有独立许可。

## 补充建议

- 用独立测试组织建立最小 team repo，只同步一个无副作用 skill；记录 `init/pull/push/uninstall` 对每个宿主目录的精确 diff。
- 对共享仓库启用 branch protection、CODEOWNERS、signed commits/tags 与 pinned source；高权限 hook/MCP 变更要求双人审核。
- 将 user-scope、package 安装、hook command、远程 MCP、env 注入和外部 source 分成独立 capability gate，默认关闭。
- 用 canary secret、过期规则和恶意 skill 测 privacy scrub、recall 排名、撤销、回滚与离线失败行为。

## 参考资料

- GitHub 仓库：https://github.com/Tencent/teamai-cli
- GitHub REST API：https://api.github.com/repos/Tencent/teamai-cli
- 中文 README：https://github.com/Tencent/teamai-cli/blob/main/README.zh-CN.md
- Usage guide：https://github.com/Tencent/teamai-cli/blob/main/docs/usage-guide.md
- `v0.23.0` release：https://github.com/Tencent/teamai-cli/releases/tag/v0.23.0
- LICENSE：https://github.com/Tencent/teamai-cli/blob/main/LICENSE
