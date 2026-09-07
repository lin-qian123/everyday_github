<!-- markdownlint-disable MD013 MD034 -->

# funes（huggingface/funes）

> 记录日期：2026-09-08（Asia/Shanghai）。本页依据上游 README、文档、release、LICENSE 与 GitHub REST API 做静态整理；本轮未安装 binary / hook、未索引任何真实会话、未连接 Hugging Face Hub，也未验证检索质量或 secret gate。

## 定位

`funes` 是 Hugging Face 组织下的跨 coding-agent 会话记忆工具。它把 Claude Code、Codex、pi、Hermes 与兼容 Parquet trace 的历史会话索引到统一记忆中，通过本地检索向 agent 暴露 `recall` / `get`，并可将记忆作为 Hugging Face dataset 分享或跨设备读取。

2026-09-08 的 GitHub Rust Trending 抓取显示约 `+42 stars today`；REST API 快照为 `260 stars / 18 forks / 6 open issues`，最新 release 为 `v1.3.0`（2026-09-01），许可证为 Apache-2.0。

## 用法

上游提供预编译安装器，支持 Linux x86_64 / aarch64 与 Apple Silicon macOS：

```bash
curl -fsSL https://huggingface.co/buckets/huggingface/funes/resolve/install.sh | sh
funes add codex
```

安装器会把 binary 放入 PATH；`funes add` 可安装 agent 集成与逐轮 hook。更稳妥的试用方式是先下载固定 `v1.3.0`、校验 `SHA256SUMS`、在可丢弃 profile 中查看 `funes add` 的配置 diff，再只索引合成 session。

## 原理

- **统一 trace shape**：各 agent parser 转成通用 turn/block；新增来源通过 `TraceSource` trait 接入。
- **本地索引**：会话被分块，用固定版本的本地 embedding 模型编码并写入 Lance dataset；原始文本仍保存在行中。
- **混合召回**：vector + BM25 融合后 rerank，并按时间新近性重加权；`recall` 返回段落，`get` 重组完整 turn。
- **Agent 接入**：hook 在每轮和 session 边界更新索引；`funes ask` 可把召回结果交给外部 agent 形成带来源回答。
- **跨宿主记忆**：Claude Code、Codex、pi、Hermes 共用同一检索层，hit 标示来源 agent。
- **Hub 发布**：本地 memory 可 push 为 dataset；新建 repo 默认 private，README 声称索引时 redaction 加上推送前 secret gate。

## 价值

- 将跨工具决策、失败路径和理由保存在可搜索层，减少换 agent 或隔周接续时只剩代码结果的问题。
- 混合检索与可回到原 turn 的引用比把整段历史塞入 prompt 更节省上下文，也更便于审计。
- 固定 embedding 模型并在 memory 中盖章，避免不同模型无提示混用导致向量空间漂移。
- 数据集形态便于团队共享、版本化和跨设备同步，同时保留本地优先路径。

## 风险边界

- Agent transcript 往往包含源码、路径、命令输出、凭据片段、客户数据与失败上下文；它比普通笔记更接近完整工作活动记录。
- 新建 dataset 默认 private 不等于现有 repo 一定 private，也不等于 token、组织权限、fork、cache 与下载副本受控。
- redaction / secret gate 不可能证明识别所有秘密、个人信息或商业敏感语义；原始文本被保留在 dataset 行中会扩大误检后果。
- `funes add` 会安装 hook 并持续索引，可能超出用户原先预期的目录、subagent transcript 和保留期范围。
- 召回结果可能陈旧、来自错误项目或把历史 workaround 当作当前规范；有引用也不代表建议仍然正确。
- 安装器 binary 与 checksum 同源，上游也明确说明 checksum 只能发现损坏 / 不匹配，不能独立认证 bucket。

## 补充建议

- 先列出实际被发现的 session 路径、agent、项目、用户与 subagent 范围；默认 deny，再逐项 allow。
- 用 canary secret、个人信息和已撤销决策测试 index、recall、push、cache、delete 与重新构建，验证不是只隐藏搜索结果。
- Hub 发布前生成可人工审阅的 chunk manifest，并用独立 secret / PII scanner；禁止自动把未知旧 dataset 改成公开。
- 召回结果应显示 session、时间、项目、agent 与版本，并要求当前仓库事实或测试重新验证高影响决策。

## 参考资料

- GitHub 仓库：https://github.com/huggingface/funes
- GitHub REST API：https://api.github.com/repos/huggingface/funes
- 最新 release：https://github.com/huggingface/funes/releases/tag/v1.3.0
- How it works：https://github.com/huggingface/funes#how-it-works
- Hub publishing：https://github.com/huggingface/funes#your-memory-on-the-hub
- LICENSE：https://github.com/huggingface/funes/blob/main/LICENSE
