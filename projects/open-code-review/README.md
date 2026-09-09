<!-- markdownlint-disable MD013 -->

# OpenCodeReview（alibaba/open-code-review）中文解读

> 证据快照：2026-09-10（Asia/Shanghai）。GitHub REST API 显示 22,148 stars、1,653 forks、166 open issues，Apache-2.0；最新 release 为 `v1.11.7`。本文未把代码发送给模型、未执行 review，也未复现上游 benchmark。

## 定位

OpenCodeReview 是阿里巴巴开源的 AI code-review CLI。它把确定性的文件选择、bundling、规则匹配、评论定位与 reflection 模块，和能读取文件、搜索代码、调用工具的 LLM agent 结合，输出精确到行的结构化审查意见。

它既支持 Git diff review，也可用 `ocr scan` 审查完整文件；并通过 CLI、CI、MCP、skills 与多种 coding-agent 插件接入工作流。

## 用法

前置条件是 Git 2.41 或更新版本。npm 安装入口为：

```bash
npm install -g @alibaba-group/open-code-review
ocr config
ocr review
```

使用前需要配置 OpenAI / Anthropic-compatible 模型 endpoint，或使用 delegation mode 由宿主 coding agent 执行推理。项目也提供完整安装脚本、GitHub release binary、CI 和 agent skill 路径；正式接入应固定 `v1.11.7` 并检查配置与 telemetry 文档。

## 原理

- 确定性 pipeline 选择待审文件、过滤路径、把相关文件组成 review unit，并按文件特征匹配规则。
- 每个 bundle 使用隔离上下文的 sub-agent 处理，便于大 changeset 并发与覆盖。
- agent 根据需要读取完整文件、搜索仓库、查看其他改动，并形成候选问题。
- 独立的 comment-positioning 与 reflection 模块修正行号和内容，再输出结构化评论。
- 上游 AACR-Bench 使用 50 个开源仓库、200 个真实 PR、10 种语言和 1,505 个标注问题，README 同时承认其 recall 低于通用 agent。

## 价值

- 把文件覆盖、规则分发和评论定位从 prompt 约定下沉到确定性工程逻辑，减少审查范围漂移。
- 可在 CLI、CI 或 agent 会话中复用同一 review 规则与输出形态。
- 上游公开 benchmark dataset，使 precision、recall、F1、时间和 token 成本至少具备可复查入口。
- 全文件 scan 和 repo context 对无有效 diff 的审计场景更实用。

## 风险边界

- README 的更高 precision / F1、约 `1/9` token 和更快速度是上游基准结论；模型版本、参数、硬件、prompt、样本选择与污染都需独立复现。
- 上游主动选择较低 recall 换取更少噪声，因此“没有评论”不能证明改动安全或正确。
- 默认模式会把 diff / 代码上下文发送到配置的模型 endpoint；secret、个人数据、客户代码和跨境合规取决于实际 provider 与配置。
- 确定性文件选择能保证流程覆盖，不保证规则完整、模型判断正确或行级评论没有误报。
- MCP、CI token、repository permissions 和自动发布评论会扩大供应链与外部副作用面。

## 补充建议

1. 在含已知缺陷和 clean changes 的本地 golden set 上分别测 precision、recall、定位准确率、token、时间与人工返工。
2. 先用只读、本地输出模式验证；未经批准不要自动把评论发布到真实 PR。
3. 在发送模型前排除 secrets、generated files、vendor code 和受限路径，并记录 endpoint、retention、region 与日志策略。
4. 将 OCR 结果作为 reviewer queue，而非 merge gate 的唯一条件；安全关键代码保留静态分析、测试和人工审查。

## 参考资料

- GitHub：<https://github.com/alibaba/open-code-review>
- GitHub REST API：<https://api.github.com/repos/alibaba/open-code-review>
- Releases：<https://github.com/alibaba/open-code-review/releases>
- 中文文档源：<https://github.com/alibaba/open-code-review/tree/main/pages/src/content/docs/zh>
- AACR-Bench：<https://huggingface.co/datasets/Alibaba-Aone/aacr-bench>
- Assurance case：<https://github.com/alibaba/open-code-review/blob/main/ASSURANCE_CASE.md>
- Telemetry 文档源：<https://github.com/alibaba/open-code-review/blob/main/pages/src/content/docs/zh/telemetry.md>
- LICENSE：<https://github.com/alibaba/open-code-review/blob/main/LICENSE>
