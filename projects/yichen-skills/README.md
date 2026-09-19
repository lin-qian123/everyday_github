<!-- markdownlint-disable MD013 MD034 -->

# yichen-skills：覆盖内容、研究与本地数据工作的个人 Agent Skill 集合

> 上游仓库：https://github.com/mcncarl/yichen-skills · 归类：Agent 框架与技能生态 · 本页基于 2026-09-20 的中英文 README、各 Skill 入口、自定义 LICENSE、third-party notices、release 与 REST API 静态整理；未安装 Skill、登录平台或读取任何个人数据。

## 定位

`yichen-skills` 汇集 21 类面向 Claude Code / Codex 的工作流，覆盖 X 长文草稿和切片、微信 / 企业微信本地资料、ASR、ChatGPT / Grok 研究、统一检索、内容归档、书签、Agent Memory Vault、剪映草稿与 WeCom 云操作。它更像个人工作流产品线，而不是单一通用 Skill 或经过统一安全认证的 marketplace。

2026-09-20 的 GitHub 官方 Python Trending 抓取显示约 `+260 stars today`；REST API 快照为 `3,902 stars / 1,658 forks / 7 open issues`，API 为 `NOASSERTION`。最新 GitHub Release 是针对单个 X Article uploader 的 `x-article-draft-uploader-v1.0.1`，不能代表所有 Skill 同步达到该版本。

## 用法

不同 Skill 的依赖、授权和平台边界不同；可按名称安装单个 Skill，例如：

```sh
npx skills add mcncarl/yichen-skills --skill yichen-x-slicer
```

使用前必须打开对应子目录的 `SKILL.md` 与 README，检查是否需要浏览器登录态、macOS、Volcengine、Grok CLI、ChatGPT 网页、微信 / 企业微信数据库、私有 runtime 或额外授权。不要把整个仓库当作一个可无条件全局安装的包。

## 原理

- 每个子目录以 `SKILL.md` 描述触发条件、步骤、权限和人机确认，配套脚本负责确定性抓取、转换或验证。
- research family 将搜索、候选核验、已知链接归档和转写拆开，避免把“发现结果”直接升级成下载或写入动作。
- 本地 vault / database 工作流强调 snapshot、只读查询、脱敏 ID、私有输出目录和不回写原应用。
- 平台工作流按 API、CLI 或已有网页登录态选择 backend；README 对 cookies、keys、browser storage 和外发路径给出不同边界。
- 部分功能只是公开 Skill 入口，依赖另行授权的私有 core；公开仓库不包含完整 runtime。

## 价值

- 将中文内容创作、社媒、微信生态、研究和记忆等分散操作沉淀为可读、可执行的 Agent 流程。
- 多处显式区分搜索 / 归档、草稿 / 发布、读取 / 写入、公开入口 / 私有 core，有利于保留人工闸门。
- 脚本、fixtures、checkpoints 和输出合同让部分高摩擦桌面工作流比纯提示词更可复核。
- README 对数据流、凭据和平台限制给出较多说明，可作为继续审计的起点。

## 风险边界

- 根 LICENSE 是“个人学习与非商业使用”自定义条款，不是 OSI 开源许可证；商业、企业内部、客户交付、课程和再打包都需书面授权。
- 部分 Skill 触及 cookies、token、微信 / 企业微信数据库、书签、聊天、客户资料、社媒草稿和本地媒体，属于高敏感权限面。
- “不把 secret 写进仓库”不等于运行时无泄露；浏览器、第三方 API、日志、临时文件、模型上下文和输出目录仍需逐条核对。
- 单个 release、README 安全声明或合成 fixture 不能证明 21 个 Skill、不同系统版本与真实账号都稳定兼容。
- 私有 core 和外部 CLI 不在公开仓库内完整可审计，不能据入口文档推断端到端可复现。
- 本页未运行任何脚本、未核对真实平台条款，也未验证删除、回滚、账号封禁、限流或跨版本兼容。

## 补充建议

1. 只安装当前任务所需的单个 Skill，先阅读其 `SKILL.md`、脚本、依赖和输出路径，再用测试账号 / 合成 snapshot 验证。
2. 把读取、草稿、发布、删除、证书 / 代理变更和凭据捕获分成独立授权，不继承旧任务权限。
3. 在商业或团队场景先取得明确书面授权，并逐项核对第三方组件许可与平台条款。
4. 对每个 Skill 固定 commit，保留输入范围、外发服务、实际写入、回滚与删除回执。

## 参考资料

- 上游 README：https://github.com/mcncarl/yichen-skills
- 中文 README：https://github.com/mcncarl/yichen-skills/blob/main/README.zh.md
- 自定义 LICENSE：https://github.com/mcncarl/yichen-skills/blob/main/LICENSE
- 第三方许可说明：https://github.com/mcncarl/yichen-skills/blob/main/THIRD_PARTY_NOTICES.md
- GitHub REST API：https://api.github.com/repos/mcncarl/yichen-skills
- 维护者网站：https://yichen.ai/
