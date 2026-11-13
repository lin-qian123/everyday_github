<!-- markdownlint-disable MD013 -->

# OpenCodeReview：将审查覆盖与模型判断分开核验

- 上游：[`alibaba/open-code-review`](https://github.com/alibaba/open-code-review)；仓库 ID：`1241960226`。
- 核读：2026-11-14（Asia/Shanghai）；主线固定于 [`0e9060da66af`](https://github.com/alibaba/open-code-review/tree/0e9060da66af36a96a15516e76a001953095318b)。
- 热度快照：50,388 stars / 3,742 forks / 338 open issues（含 PR）；来自 [GitHub API](https://api.github.com/repos/alibaba/open-code-review)，不代表采用量或质量。

## 定位

阿里巴巴开源 AI code-review CLI，用确定性的文件筛选、分组、规则和定位，配合能读文件、搜索代码的 LLM Agent 输出行级评论；支持全文件 scan、委托模式与 CI / 插件。

综合 / Go daily +206。稳定 [v1.13.9](https://github.com/alibaba/open-code-review/releases/tag/v1.13.9) 于 UTC 11-13 发布，[npm latest](https://registry.npmjs.org/@alibaba-group%2Fopen-code-review/latest) 同为 1.13.9；从 9 月 v1.11.7 说明原位更新。

## 用法

需要 Git 2.41+；固定版本，在不含敏感资料的测试仓库开始。上游入口，本轮未执行：

```bash
npm install -g @alibaba-group/open-code-review@1.13.9
ocr config provider
ocr config model
ocr review
```

配置向导可能测试模型连通性。普通 review command / skill 用 OCR 自己的 provider；delegate-review / delegate skill 则由宿主调用模型，OCR 端无需另配 LLM，鉴权与费用须区分。

仅看候选范围可先 `ocr delegate preview`，再 `ocr delegate rule <path>` 取规则。接 CI 时先输出本地报告，再决定是否发布真实 PR 评论；全文件审查用 `ocr scan`。

## 原理

pipeline 选文件、过滤、组成 bundle、匹配规则；每组用独立上下文 Agent 调查，再定位和 reflection。确定性步骤约束流程，模型负责语义判断。

v1.13.9 将 excluded 文件记入 run coverage，在零 finding 的 PR summary 展示 warnings，并修复每请求工具声明约束。主线 manifest 明确：selected 为分母，等于 completed、reused、failed、waived 四个互斥集合之和；excluded 单列。被选择、完成、复用、失败、豁免与排除须分别看，不能只读评论数。

## 价值

更容易追溯哪些文件进入流程、哪些未审、哪些沿用结果。覆盖清单和 warnings 有助于解释“为什么没有报问题”，并安排人工补审。

## 风险边界

- AACR-Bench 的高 precision / F1、约 1/9 token 和速度是上游结论；README 承认以较低 recall 换少噪声。无 finding 不证明无缺陷，流程覆盖也不是语义覆盖。
- 普通模式向配置模型发送代码；委托模式改由宿主处理，仍须核出口和权限。MCP、规则和 CI 有独立信任范围。
- 遥测文档声明默认关闭；开启导出结构化指标 / 事件而不含 prompt / response，但组路径、repo.dir、错误元数据仍可能敏感。`content_logging` 当前是保留配置，不能当有效内容开关。
- 会话转录存本机，另开 `OCR_RAW_LOGGING=1` 会记录原始请求 / 响应体；头部脱敏不代表正文已脱敏，本地日志与遥测出口应分别治理。
- assurance case 是上游安全论证，非本轮渗透、验签或权限实验；自定义 credential command、Agent shell 与 MCP server 按本地用户配置运行。
- 根代码为 Apache-2.0；provider、宿主账号与 benchmark 数据有各自条件。

## 补充建议

用已知缺陷和 clean changes 同测 precision、recall、定位、耗时与总 token，同时导出 selected / failed / waived / excluded，避免将缩小覆盖当提速。升级时单验工具声明、过滤与零 finding warnings，核保存的 provider、endpoint 和日志策略。

本页为固定文件、发行与 npm 元数据核读；未执行 review / scan、调用模型、发评论、抓 OTLP 流量或复现基准。

## 参考资料

- [模式、架构与基准](https://github.com/alibaba/open-code-review/blob/0e9060da66af36a96a15516e76a001953095318b/README.md)。
- [覆盖分母与排除](https://github.com/alibaba/open-code-review/blob/0e9060da66af36a96a15516e76a001953095318b/internal/session/manifest.go)。
- [Provider 与配置](https://github.com/alibaba/open-code-review/blob/0e9060da66af36a96a15516e76a001953095318b/pages/src/content/docs/zh/configuration.md)。
- [委托模式](https://github.com/alibaba/open-code-review/blob/0e9060da66af36a96a15516e76a001953095318b/pages/src/content/docs/zh/integrations/delegate.md)。
- [遥测与原始日志](https://github.com/alibaba/open-code-review/blob/0e9060da66af36a96a15516e76a001953095318b/pages/src/content/docs/zh/telemetry.md)。
- [上游安全论证](https://github.com/alibaba/open-code-review/blob/0e9060da66af36a96a15516e76a001953095318b/ASSURANCE_CASE.md)。
- [Apache-2.0 许可](https://github.com/alibaba/open-code-review/blob/0e9060da66af36a96a15516e76a001953095318b/LICENSE)。
