<!-- markdownlint-disable MD013 MD034 -->

# openai-plugins（openai/plugins）

> 记录日期：2026-09-08（Asia/Shanghai）。本页依据上游 README、marketplace manifest、仓库结构与 GitHub REST API 做静态整理；本轮未安装任何 plugin、未登录 connector、未运行 MCP / skill / hook，也未验证每个子目录的权限、安全或许可。目录采用 owner-aware 名称，避免覆盖已有 `projects/plugins`。

## 定位

`openai/plugins` 是 OpenAI 维护的 Codex plugin 示例与 marketplace 清单。每个 plugin 位于 `plugins/<name>/`，以 `.codex-plugin/plugin.json` 为必需 manifest，可组合 skills、apps、MCP、agents、commands、hooks 和 assets。默认 marketplace 在 `.agents/plugins/marketplace.json`，API-key login 另有清单。

2026-09-08 的 GitHub JavaScript Trending 抓取显示约 `+45 stars today`；REST API 快照为 `5,475 stars / 788 forks / 39 open issues`，没有 GitHub release，最新 push 为 2026-08-28。API 未返回许可证且根目录未见 LICENSE，因此不能仅因 owner 是 OpenAI 就假定可重用、再分发或商用的统一许可。

## 用法

该仓库更适合作为“审阅 plugin 组成与 marketplace contract”的源码入口：

```bash
git clone https://github.com/openai/plugins.git
cd plugins
```

当前默认 marketplace 静态快照列出 64 个 entry，包含 Linear、Slack、Figma、GitHub、Notion、Cloudflare、Sentry、Codex Security、OpenAI Developers、Data Analytics 等本地目录或外部 URL source。实际安装应通过用户所用 Codex 版本提供的 plugin 界面 / 流程完成，并在安装前查看 manifest、认证时点和所有伴随 surface；本页不推断未在 README 中写明的 CLI 命令。

## 原理

- **Manifest 入口**：`.codex-plugin/plugin.json` 描述 plugin 身份与入口，形成最小可发现契约。
- **多 surface 打包**：一个 plugin 可同时携带 skill 指令、app connector、MCP server、agent、command、hook 与 asset。
- **Marketplace 索引**：中央 JSON 列出 `name`、source、安装 / 认证 policy、category 和可选 product 限制。
- **本地与外部 source**：大多数条目指向仓库内 `plugins/`，部分可直接引用外部 Git 仓库；两者的信任与更新链不同。
- **按认证阶段控制**：清单可标记 `ON_INSTALL` 或 `ON_USE`，但这只描述流程时点，不自动给出最小 scope。
- **示例复合能力**：README 重点列出 Figma、Notion、iOS / macOS / Web、Expo、Netlify、Remotion、Google Slides 等较完整组合。

## 价值

- 提供可读的官方 plugin 结构样本，便于开发者理解单一包如何组合模型指令和外部能力。
- marketplace manifest 让发现、分类、认证时机与产品限制可版本化审阅。
- 公开例子有利于比较只含 skills 的轻插件和带 app / MCP / hook 的高权限插件。
- 统一入口降低每个工具重复编写安装说明和集成 glue 的成本。

## 风险边界

- “curated”或官方仓库不等于每个第三方 connector、外部 source、skill 指令和更新版本都经过完整安全审计。
- Plugin 可同时扩展 prompt、网络、文件、命令、hook 和外部账户；用户看到的一个名称可能对应多条不同权限链。
- `ON_INSTALL` / `ON_USE` 不说明 OAuth scope、数据保留、模型可见内容、写权限或撤销效果，必须查看具体 plugin 与服务条款。
- 外部 Git source、安装后自动更新和依赖下载扩大供应链面；应固定 commit / version 并审阅 diff。
- 本轮 64 个 entry 是抓取时点的 manifest 计数，不是全部已安装、可用、兼容或通过评测的能力。
- 根目录无明确统一 LICENSE；各 plugin、vendor asset、MCP 和外部服务也可能有独立许可。

## 补充建议

- 安装前生成 surface 清单：skills、apps、MCP、agents、commands、hooks、assets、外部 URL、依赖与认证 scope。
- 在可丢弃 profile 中逐个 plugin 安装，记录配置 diff、网络、token、文件写入、撤销与卸载残留。
- 对 marketplace 更新做签名 / provenance、固定版本和人审 diff；外部 URL source 使用单独 allowlist。
- 给每个 connector 建只读最小权限账号和 canary 数据，明确哪些内容会进入模型上下文、日志和第三方服务。

## 参考资料

- GitHub 仓库：https://github.com/openai/plugins
- GitHub REST API：https://api.github.com/repos/openai/plugins
- 上游 README：https://github.com/openai/plugins#plugins
- 默认 marketplace：https://github.com/openai/plugins/blob/main/.agents/plugins/marketplace.json
- Plugin examples：https://github.com/openai/plugins/tree/main/plugins
- OpenAI 官方 YouTube「Introducing Agent Plugins」：https://www.youtube.com/watch?v=UaeWJK_vv-Y
