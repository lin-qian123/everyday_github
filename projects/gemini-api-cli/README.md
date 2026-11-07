<!-- markdownlint-disable MD013 -->

# Gemini API CLI：让现有 Agent 从 Shell 调用模型与托管任务

- 上游：[google-gemini/gemini-api-cli](https://github.com/google-gemini/gemini-api-cli)；仓库 ID：`1224715013`。
- 快照：2026-11-08（Asia/Shanghai）；stars / forks / open issues（含 PR）：471 / 73 / 41；官方 daily 榜 Go +16，不是自然日结算。
- 分类：Agent 框架与技能生态；最新发行：[v0.4.5](https://github.com/google-gemini/gemini-api-cli/releases/tag/v0.4.5)（UTC 2026-10-30 22:14:35，非预发行标记）。
- 核读基线：`main@52fe5da31e5a9629326f126b4a52d2be44659b19`。以下为文档与抽样源码核读，作者声明与本轮运行验证分开。

## 定位

`gemini-api` 是 Google Gemini API 的实验性 / Beta CLI：由现有 Agent 决定工作流程，通过独立命令调用文本、多模态、媒体生成和托管 Agent。它与交互式 coding 产品 Gemini CLI 的名称、安装包和使用目的不同；不要混用两者凭据 / 权限说明。

## 用法

优先从 v0.4.5 发行下载匹配平台的二进制并核对来源，或用固定 Go module 版本：

```bash
go install github.com/google-gemini/gemini-api-cli/cmd/gemini-api@v0.4.5
gemini-api --help
gemini-api generate "测试请求结构" --dry-run
gemini-api agent run --schema
```

上例最后两条用于检查请求 / schema，不应视为已经调用模型。主线 go.mod 要求 Go 1.26.10；自动 toolchain 可能另下载编译器。真实调用需配置 API key，先用 `whoami` 核对来源。结构化结果可用 `--stream=false --output-format json`；后台托管任务保留返回的 interaction ID，再查询状态或取消。本轮没有安装、配置 key 或发送模型请求。

## 原理

Go / Cobra 命令将参数、文件和 JSON body 转成 API 请求，按响应将文本、结构化对象、媒体路径或 interaction ID 交给宿主 Agent。每次 CLI 调用无本地对话状态，延续由服务端 interaction 和宿主保存的 ID 管理。内置 `--usage`、`--schema`、离线模型目录支持按需发现；目录列出模型不证明当前账号有权限或配额。

## 价值

已有 Shell Agent 可复用单个二进制，不必为每类媒体单独集成 SDK；dry-run 便于审阅将发送的请求。主线实现会在 dry-run 跳过 OS keychain 读取。静态请求有效、服务端接受、任务完成和输出质量仍是四个不同结果。

## 风险边界

- 实际请求、上传文件、托管任务和服务端 credentials / webhooks / triggers 都具有外部副作用与费用；上传 / 存储期限按 API 资源及配置分别核，不能从 CLI“无状态”推断服务端不留存。
- 凭据优先级为 flag、环境变量、OS keychain、配置文件。keychain 不可用 / 被禁用时可用 YAML 文件；源码写权限 0600 不等于加密。不要将真实 key 写进示例、Git 或命令历史。
- `--dry-run` 不发请求，不验证额度、权限、模型可用性、推理正确性或媒体质量；`--no-interactive` 只改变交互行为，不构成授权策略。
- main 与发行分别固定；Beta 可能有破坏性变更，README 当前也注明暂不接收外部 PR。不要因开源许可推断贡献流程必然开放。
- README 区分软件 Apache-2.0、其他材料 CC BY 4.0；模型服务条款、上传素材权利与输出用途另核。未运行 API、下载媒体或验收托管 sandbox。

## 补充建议

先把固定版本、离线 schema / dry-run 和预算上限写入自己的调用封装，再用无敏感样本做最小真实请求。分别管理文件、interaction、任务、凭据和生成制品的 ID、取消与清理，避免失败后重复收费。所有后台任务需保存可恢复状态，不把一次 CLI 退出当远端任务已经结束。

## 参考资料

- [README.md](https://github.com/google-gemini/gemini-api-cli/blob/52fe5da31e5a9629326f126b4a52d2be44659b19/README.md)
- [go.mod](https://github.com/google-gemini/gemini-api-cli/blob/52fe5da31e5a9629326f126b4a52d2be44659b19/go.mod)
- [internal/config/config.go](https://github.com/google-gemini/gemini-api-cli/blob/52fe5da31e5a9629326f126b4a52d2be44659b19/internal/config/config.go)
- [internal/config/keyring.go](https://github.com/google-gemini/gemini-api-cli/blob/52fe5da31e5a9629326f126b4a52d2be44659b19/internal/config/keyring.go)
- [LICENSE](https://github.com/google-gemini/gemini-api-cli/blob/52fe5da31e5a9629326f126b4a52d2be44659b19/LICENSE)
- [GitHub API 快照](https://api.github.com/repos/google-gemini/gemini-api-cli)；[发行列表](https://github.com/google-gemini/gemini-api-cli/releases)。
