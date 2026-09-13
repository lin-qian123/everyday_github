<!-- markdownlint-disable MD013 -->

# Git AI（git-ai-project/git-ai）中文解读

> 证据快照：2026-09-14（Asia/Shanghai）。GitHub REST API 显示 2,683 stars、291 forks、213 open issues，最新 GitHub Release 为 `v1.7.5`（2026-09-09），API 与根文件均为 Apache-2.0；当前 main 的 `Cargo.toml` 已写 `1.7.6`，因此默认分支状态领先于最新发布包。本文未运行 installer、daemon、agent integration、Git rewrite 或归因统计。

## 定位

Git AI 是一个 Git 扩展，用 Git Notes 记录 coding agent 报告的行级归因，并把代码行关联到 agent、model、session 与 prompt。它提供 `git ai blame`、commit stats 和团队版观测能力，试图让 AI 生成代码从不可见的聊天过程变成可追溯的工程 metadata。

它不是通过代码风格猜测“这行是不是 AI 写的”的检测器。上游明确说明归因来自支持的 agent 在写文件时调用 checkpoint，因此准确性依赖集成、工作目录、rewrite 映射和 metadata 保留。

## 用法

上游提供 shell installer，也可从 Rust 源码构建。安装后正常提交，再查看归因：

```bash
curl -sSL https://usegitai.com/install.sh | bash
git commit
git ai blame src/example.rs
git ai stats --json
```

正式环境不应直接管道执行网络脚本；先下载、校验 release 与 installer，再在副本仓库测试 supported agent、worktree、rebase、squash、stash 和 push Notes 的行为。

## 原理

- 支持的 coding agent 在 edit/write/patch 或 shell 写文件时调用 `git-ai checkpoint`，记录哪些变更属于哪个 session。
- commit 时将行级归因写入 Git Notes，把 model、agent、接受率和操作者 Git identity 与 commit 关联。
- 本地 daemon 在 rebase、cherry-pick、stash、squash、reset 等历史重写后重新映射归因；上游称其为 eventually consistent。
- `git ai blame` 在普通 blame 旁显示 agent 归因，`git ai stats` 汇总 AI/human additions、accepted lines、model 与 session。
- 开源未登录模式把 prompt 存在本地 SQLite；Git Notes 会随配置的 ref 推送，cloud/team 模式有不同上传与访问范围。

## 价值

- 为 AI 修改保留 intent/session 指针，代码评审和事故回溯不必只依赖易丢失的聊天窗口。
- 采用 Git Notes 而非改源码格式，能把 attribution 与代码内容分离，并复用 Git 的 commit/ref 模型。
- 明示“agent 自报告”比事后概率检测更容易审计其证据链和失效模式。
- 统计 accepted/reworked lines 可作为研究输入，但必须与测试、review、缺陷和业务结果结合。

## 风险边界

- agent 未集成、checkpoint 漏报、shell cwd 错误或文件被外部工具修改时，归因可能缺失；自报告不能作为法务、版权或恶意行为的取证结论。
- Git Notes 会包含哪些行由 AI 生成、model/agent、接受率及操作者姓名/邮箱，任何有仓库访问权的人都可能读取这些 metadata。
- 上游 data-privacy 文档说明 OSS 模式的 error/exception telemetry 默认开启，需显式关闭或重定向；“local-first”不是“默认零出站”。
- 个人 dashboard、team/cloud 模式可上传完整 prompt、response、tool/MCP/skill 事件和身份；best-effort secret stripping 不能保证删除所有敏感信息。
- rebase/squash/merge 后的行映射、格式化和多 agent 同改一行存在歧义；上游支持矩阵需要在团队真实工作流独立回归。
- main 版本领先 release，且 installer 会管理 agent integrations；应固定版本并审计更新路径，而不是依赖每日自动变化。

## 补充建议

1. 先用合成仓库和假身份建立 gold attribution，逐项测试 patch、shell、formatter、worktree 与全部 rewrite 操作。
2. 明确哪些 Git Notes ref 会被 push/fetch，按最小可见性设置 remote 与 CI，避免把身份或工作方式无意发布到公共仓库。
3. 默认关闭 OSS telemetry，不启用 cloud/dashboard；若团队确需上传，先完成 prompt/源码分类、DLP、访问、保留和删除评审。
4. 将 attribution 作为 review 线索，不用于自动拒绝贡献、个人绩效或许可证判断；用 commit、diff、测试和人工证据交叉核验。

## 参考资料

- GitHub：<https://github.com/git-ai-project/git-ai>
- GitHub REST API：<https://api.github.com/repos/git-ai-project/git-ai>
- Releases：<https://github.com/git-ai-project/git-ai/releases>
- Git AI standard：<https://github.com/git-ai-project/git-ai/blob/main/specs/git_ai_standard_v3.0.0.md>
- 数据隐私：<https://github.com/git-ai-project/git-ai/blob/main/data-privacy.md>
- 官方文档：<https://usegitai.com/docs>
- 官方 YouTube：<https://www.youtube.com/@git-ai>
- LICENSE：<https://github.com/git-ai-project/git-ai/blob/main/LICENSE>
