<!-- markdownlint-disable MD013 MD034 -->

# oh-my-hermes：Hermes Agent 的工作流、路由与记忆层

> 上游仓库：https://github.com/rlaope/oh-my-hermes · 归类：Agent 框架与技能生态 · 本页基于 2026-09-15 的上游 README、架构/记忆文档、benchmark 说明、release、LICENSE 与 GitHub REST API 静态整理；未在本机安装或运行。

## 定位

`oh-my-hermes`（OMH）不是另一个基础 agent runtime，而是叠加在 [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) 上的操作层。它把任务分流、模型链、专家 skills、并行交付、证据状态、可审阅长期记忆和终端 HUD 组合成一套可安装插件，目标是让 Hermes 的“规划、执行、验证、记忆”边界更显式。

2026-09-15 的 GitHub 官方综合 / Python Trending 抓取显示约 `+52 stars today`；REST API 快照为 `2,009 stars / 161 forks / 13 open issues`，MIT，最新 release 为 `v2.0.3`（2026-09-12）。这些数字是公开关注度和仓库状态，不是能力或稳定性证明。

## 用法

上游提供脚本、Homebrew、Bun、npm 和 Hermes skill tap 等安装路径。相比直接执行远端脚本，更适合审计的起点是先固定 release 或 commit，再用包管理器安装：

```sh
brew install rlaope/tap/omh
# 或
npm install -g oh-my-hermes

omh setup
omh doctor
omh model
```

上游给 agent 的安装协议特别要求先把 `refs/heads/main` 解析为完整 commit SHA，再读取该 SHA 下的 `INSTALL_FOR_AGENTS.md`。这能降低分支在审阅与执行之间变化的风险，但仍应先检查安装脚本将写入的用户级配置、skills、plugin bundle 和状态目录。

## 原理

- **请求路由**：按任务复杂度和类型选择 `quick`、`deep`、`architect`、`writing` 等类别，并为类别配置模型、effort 和失败回退链。
- **工作流与 skills**：由 `ulw-*` 工作流组织计划、并行 lane、交付与验证，并从生成式 catalog 中按需加载领域 skills。
- **证据状态**：HUD 区分 `Plan · not run`、`Code · running`、`Code · reported done` 与 `Test · verified`，避免把执行器自报完成等同于验证通过。
- **并行执行**：对声明为互不共享文件的工作单元使用独立 worktree，并以 typed result、revision、命令和环境绑定验证回执。
- **长期记忆**：候选记忆先进入 review card，获批后才进入带来源、过期和 attention tier 的文件型存储；prepared recall 只是上下文，不是重新验证过的事实或执行证据。
- **Hermes 边界**：OMH 负责准备 prompt、路由、状态和记忆；真正的工具权限、模型调用和代码执行仍落在 Hermes 或被委派的 executor 上。

## 价值

- 把“已经计划”“执行器说完成”“测试确实通过”拆成不同状态，有利于长任务交接和复核。
- 模型链、任务类型和 per-family calibration 都可见、可改，便于控制成本、延迟与能力取舍。
- 记忆采用审阅、来源、过期和 scope，而不是把所有历史对话静默注入每次请求。
- workflow、skills、HUD 与 doctor 集中在一个插件，降低单独拼装多套 Hermes 扩展的维护成本。

## 风险边界

- README 的产品 A/B 章节明确写着“尚未发布 measured run”；仓库中的离线 pilot、单模型任务数字或自身 PR corpus 不能外推为通用提速、降本或质量结论。
- OMH 会安装/更新技能、插件、模型配置和本地状态；它是高信任供应链组件，不能因为 MIT 或固定 SHA 就跳过逐项审计。
- worktree、typed result 和回执不等于 OS sandbox。shell、网络、凭据、模型 provider 和真实仓库权限仍由宿主环境决定。
- 长期记忆即使经过 review，也可能保存过时、敏感或错误结论；摘要、scope 和 lineage 不证明原始事实仍然成立。
- 多模型回退可能改变数据路径、费用、上下文窗口和响应语义；配置“可见”不代表 provider 条款与数据治理已经满足。
- 本页只做静态上游审查，没有复现安装、路由、fan-out、memory、成本表或 benchmark。

## 补充建议

1. 固定 `v2.0.3` 或完整 commit，在可丢弃 Hermes profile 和副本仓库中运行 `setup` / `doctor`，保存安装前后 diff。
2. 用同一组小任务验证四种状态是否与真实进程、测试日志和 Git revision 一致，再测试中断、失败和恢复。
3. 先关闭真实凭据与云端 provider，用合成记忆检查 review、expiry、scope、correct/retire 与删除残留。
4. 复现上游 benchmark 时固定模型、价格表、硬件、任务 corpus 和缓存，并把训练/准备成本与失败任务计入分母。

## 参考资料

- 上游 README：https://github.com/rlaope/oh-my-hermes
- 架构说明：https://github.com/rlaope/oh-my-hermes/blob/main/docs/ARCHITECTURE.md
- 长期记忆说明：https://github.com/rlaope/oh-my-hermes/blob/main/docs/MEMORY.md
- 产品 A/B 边界：https://github.com/rlaope/oh-my-hermes/tree/main/benchmarks/product-ab/v1
- `v2.0.3` release：https://github.com/rlaope/oh-my-hermes/releases/tag/v2.0.3
- GitHub REST API：https://api.github.com/repos/rlaope/oh-my-hermes
- LICENSE：https://github.com/rlaope/oh-my-hermes/blob/main/LICENSE
