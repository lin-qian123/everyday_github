<!-- markdownlint-disable MD013 -->

# lazycodex（code-yeongyu/lazycodex）

> 记录日期：2026-09-06（Asia/Shanghai）。本页依据上游 README、源码目录、release、LICENSE 与 GitHub REST API 做静态整理；本轮未执行安装器、未修改 Codex 配置，也未运行其多 agent 工作流或 benchmark。

## 定位

`LazyCodex` 是面向 Codex 的第三方 agent harness 分发层，借鉴 LazyVim/LazyVim 的“预配置发行版”思路，把 OmO（oh-my-openagent）的项目记忆、规划、执行、验证、skills、hooks、多模型路由和诊断封装为一套安装体验。

2026-09-06 的 GitHub 官方 TypeScript Trending 抓取显示约 `+10 stars today`；REST API 快照为 `3,396 stars / 214 forks / 19 open issues`，最新 release 为 `v4.19.4`，许可证为 MIT。它不是 OpenAI 官方 Codex 组件，兼容性和权限边界应按第三方插件处理。

## 用法

上游推荐通过 `npx` 安装：

```bash
npx lazycodex-ai install
npx lazycodex-ai doctor
```

README 还提供实验性的 Codex plugin marketplace 路径。安装说明明确涉及 plugin cache、hooks、MCP servers、agent roles、bin links 与 `~/.codex/config.toml` 的 managed sections；应先在可丢弃 Codex profile 中审查变更，避免直接改动主力配置。

## 原理

- **薄分发层**：LazyCodex 自身主要负责将 OmO 核心作为 Codex 可安装的 harness 组合并提供文档/站点。
- **项目记忆**：`init-deep` 等工作流先生成代码库地标和项目上下文，供后续 agent 使用。
- **三类主流程**：规划、执行和持续/超长任务命令把不同阶段与检查点组织起来。
- **Skills 与 hooks**：在 Codex 生命周期周围增加专用技能、前后置 hooks 和 bootstrap 逻辑。
- **多模型路由**：按任务类别选择不同模型/推理档位，目标是兼顾质量和配额；实际可用模型取决于 Codex 版本与账户。
- **多 agent 角色**：为 explorer、librarian、plan、reviewer 等角色安装配置，并依赖 Codex 的原生多代理能力。

## 价值

- 为希望快速采用结构化 agent 工作流的 Codex 用户提供一套统一安装、doctor 与卸载入口。
- 把记忆、规划、执行、验证与角色分工放到相对连贯的操作模型中。
- 源码和 MIT 许可便于审查其配置改动、模型路由和插件生命周期。
- Doctor 有助于发现 plugin cache、hooks、MCP 和配置的缺失或版本漂移。

## 风险边界

- 一行安装会触及用户级 Codex 配置、hooks、agent roles、MCP 和可执行文件；这属于高信任供应链入口，不应只凭 stars 安装。
- “autonomous”“verified completion”是工作流能力描述，不代表任务自动正确、测试充分或外部动作已获授权。
- 多模型路由可能改变费用、数据 provider、延迟和结果可复现性；模型名称/档位会随 Codex 版本与账户变化。
- 子 agent 和 hooks 会扩大提示注入、权限继承、日志和配额消耗面；必须对每个角色设置清晰工具与目录边界。
- 上游宣传中的质量、stars 或 token 叙述不能替代固定版本 A/B benchmark；本轮没有运行任何样例。
- 第三方 marketplace 与上游 OmO 子模块形成多层更新链，需 pin commit/tag 并检查 submodule 和发布包一致性。

## 补充建议

- 先备份并 diff `~/.codex/config.toml`、agent、skill、plugin、MCP 和 bin 目录，在专用 profile 安装固定版本。
- 审查安装脚本、bootstrap hooks、submodule revision 和所有下载 URL，再允许执行。
- 用同一小仓库、同一模型和同一任务做原生 Codex 与 LazyCodex A/B，比较成功率、token、耗时、diff 大小和返工。
- 验证 doctor、upgrade、uninstall 后是否清除 managed sections 且不破坏用户已有配置。
- 对 autonomous 模式设置独立工作区、网络 allowlist、低额度 key 和人工合并门，不让“自动完成”直接进入生产。

## 参考资料

- [GitHub 仓库](https://github.com/code-yeongyu/lazycodex)
- [GitHub REST API](https://api.github.com/repos/code-yeongyu/lazycodex)
- [v4.19.4 Release](https://github.com/code-yeongyu/lazycodex/releases/tag/v4.19.4)
- [项目文档](https://lazycodex.ai/docs)
- [MIT LICENSE](https://github.com/code-yeongyu/lazycodex/blob/main/LICENSE)
- [README 引用的 X 帖](https://x.com/justsisyphus/status/2060210365338939452)
