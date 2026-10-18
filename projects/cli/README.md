<!-- markdownlint-disable MD013 -->

# Google Workspace CLI（gws）

> 更新：2026-10-19（Asia/Shanghai）。分类：办公、商业与行业应用。上游 `googleworkspace/cli`；本文基于官方榜单、认证 API 与文档 / 源码静态核验，未安装运行。源码快照 `a3768d0e82ad`；Release 与主分支行为分别说明。热度见[当日官方榜单](https://github.com/trending/rust?since=daily)。

## 定位

googleworkspace/cli 的命令名是 gws，把 Drive、Gmail、Calendar、Sheets、Docs 等 Workspace API 统一为 CLI、JSON 输出与 agent skills。目录按真实仓库名保留为 cli，避免把命令名当成另一个上游。README 明示这不是 Google 正式支持的产品，且 v1.0 前可能有破坏性变更。[来源 1](https://github.com/googleworkspace/cli/blob/a3768d0e82ad83cca2da97724e46bea4ff0e6dbd/README.md)

官方 Rust Trending 约 +51 当日 stars；API 为 31,653 / 2,003 / 136（stars / forks / open issues）；最新稳定 Release v0.22.5；Apache-2.0。[来源 2](https://api.github.com/repos/googleworkspace/cli)[来源 3](https://github.com/googleworkspace/cli/releases/tag/v0.22.5)[来源 7](https://github.com/googleworkspace/cli/blob/a3768d0e82ad83cca2da97724e46bea4ff0e6dbd/LICENSE)

## 用法

从对应平台 Release 或上游包管理入口安装。先准备 Cloud project、OAuth client 和所需 API；auth setup 可自动化部分配置，auth login 选择服务 / scope。先只做 schema 和小页读取：[来源 1](https://github.com/googleworkspace/cli/blob/a3768d0e82ad83cca2da97724e46bea4ff0e6dbd/README.md)

```bash
gws schema drive.files.list
gws drive files list --params '{"pageSize": 5}'
```

有写入的请求先用 `--dry-run` 看目标和 JSON，再在测试资源执行。README 提醒未验证 OAuth app 的 scope 数量限制会影响 recommended preset；应只选实际服务，不为省步骤默认授权全部能力。本轮未登录 Workspace、安装技能或调用任何账户 API。

## 原理

运行时读取 Google Discovery Service，把资源、方法、参数和 request schema 动态生成命令；手工 helper 以 `+` 区分。JSON / NDJSON 输出便于脚本与 agent 消费，skills 负责常见工作流组织，实际权限来自 token 和 Google 账户。[来源 1](https://github.com/googleworkspace/cli/blob/a3768d0e82ad83cca2da97724e46bea4ff0e6dbd/README.md)[来源 4](https://github.com/googleworkspace/cli/blob/a3768d0e82ad83cca2da97724e46bea4ff0e6dbd/docs/skills.md)

凭据优先级包括显式 access token、credentials file、加密凭据和 plaintext fallback。Model Armor 清洗是可选路径；executor 仅在提供 sanitize template 后检查响应，命中后是否阻断另取决于模式，不是默认保证。[来源 1](https://github.com/googleworkspace/cli/blob/a3768d0e82ad83cca2da97724e46bea4ff0e6dbd/README.md)[来源 5](https://github.com/googleworkspace/cli/blob/a3768d0e82ad83cca2da97724e46bea4ff0e6dbd/crates/google-workspace-cli/src/executor.rs)

## 价值

适合减少逐服务 curl / SDK 胶水代码，也可把只读 Workspace 数据接入已有 agent。Discovery 动态生成提高 API 覆盖速度，同时要求稳定工作流保留 schema 快照与版本；“API 可用”不等于业务流程正确。

## 风险边界

- OAuth scope、service account / delegation 与账户权限决定真实可读写范围。技能不会把已有 token 自动降为只读；邮件发送、分享、删除和管理操作需单独验权。
- 凭据静态加密保护存储，不能阻止同用户或持解密能力的恶意进程使用；README 仍保留 plaintext credentials fallback，需核实际选中路径。[来源 1](https://github.com/googleworkspace/cli/blob/a3768d0e82ad83cca2da97724e46bea4ff0e6dbd/README.md)[来源 6](https://github.com/googleworkspace/cli/blob/a3768d0e82ad83cca2da97724e46bea4ff0e6dbd/crates/google-workspace-cli/src/auth.rs)
- Dynamic Discovery 会使命令面随 API 变化，不能仅固定 CLI 二进制就假定 schema 永不变。
- Gmail / Docs / 文件内容可携带 prompt injection。可选 Model Armor 不是授权系统，warn 与 block 的差异及失败策略要实测。[来源 5](https://github.com/googleworkspace/cli/blob/a3768d0e82ad83cca2da97724e46bea4ff0e6dbd/crates/google-workspace-cli/src/executor.rs)
- dry-run 不是远端执行成功证明，也不是账户最终权限测试；Cloud project、API 配额、扩展安装和 npx 供应链均另需治理。
- 根代码 Apache-2.0，外部 Google API、模型安全服务和数据按各自条款处理。[来源 7](https://github.com/googleworkspace/cli/blob/a3768d0e82ad83cca2da97724e46bea4ff0e6dbd/LICENSE)

## 补充建议

先以只读 scope 和测试文件夹做 schema、分页、权限不足与字段缺失试验；记录 CLI 版本、Discovery schema、scope 和资源 ID。需要写入时逐类设置动作确认和验收，保留预览、实际响应与最终资源状态，避免由一次终端认证默认扩散为全局 agent 权限。

## 参考资料

1. [README、身份与认证约束](https://github.com/googleworkspace/cli/blob/a3768d0e82ad83cca2da97724e46bea4ff0e6dbd/README.md)
2. [仓库 API](https://api.github.com/repos/googleworkspace/cli)
3. [v0.22.5 Release](https://github.com/googleworkspace/cli/releases/tag/v0.22.5)
4. [Skills 索引](https://github.com/googleworkspace/cli/blob/a3768d0e82ad83cca2da97724e46bea4ff0e6dbd/docs/skills.md)
5. [执行器与可选清洗](https://github.com/googleworkspace/cli/blob/a3768d0e82ad83cca2da97724e46bea4ff0e6dbd/crates/google-workspace-cli/src/executor.rs)
6. [凭据实现](https://github.com/googleworkspace/cli/blob/a3768d0e82ad83cca2da97724e46bea4ff0e6dbd/crates/google-workspace-cli/src/auth.rs)
7. [LICENSE](https://github.com/googleworkspace/cli/blob/a3768d0e82ad83cca2da97724e46bea4ff0e6dbd/LICENSE)
