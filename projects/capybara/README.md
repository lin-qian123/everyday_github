# capybara

## 定位

`capybara` 是 AI agent 的终端 trace debugger：它接收 OTLP、读取 Claude Code 会话文件或导入 trace，落入本地 SQLite 后在 TUI/Web 视图中定位失败工具调用、漂移、重复循环和成本尖峰。截至 2026-07-25，仓库创建于 2026-07-24，约 8 stars、0 forks，属于早期可观察性工具。

## 用法

可通过 `go install github.com/tonquoc0407/capybara/cmd/capybara@latest` 安装，直接运行 `capybara` 启动本机监听和 TUI。已有 OTEL 应用设置 `OTEL_EXPORTER_OTLP_ENDPOINT=http://127.0.0.1:4318`；也可用 `capybara watch claude` 读取本地会话，或以 `import` 导入 JSONL。需避免记录内容时使用 `-no-content`。

## 原理

一个 Go 二进制将 receiver、SQLite、分析器、TUI 和只读 Web 视图整合。它规范化 OpenTelemetry、OpenInference、OpenLLMetry、Vercel AI SDK 等属性，再对 span 做增量分析：例如工具失败后模型仍无依据作答、输出 schema 漂移、错误 payload、循环调用与异常成本。

## 价值

- 将 agent 的最终回答回溯至具体工具、上下文与错误证据，而不只看一次日志。
- 支持 trace diff、replay 和导出 pytest fixture，有助于把偶发失败沉淀为回归用例。
- 本地 SQLite 和单二进制降低试用 observability 的部署门槛。

## 风险边界

- trace、prompt 与工具输出可能含源代码、密钥或个人数据；默认收集前必须确认最小记录范围。
- 内置模型费率表可能滞后，未知模型保持未定价；它不应作为账单核算依据。
- finding 是被动提示而非 CI gate，不能单靠它判定 agent 行为安全或正确。

## 补充建议

在无敏感的测试项目上验证 OTLP schema 与 `-no-content`，再接入真实 agent。将 replay/export 的数据视作敏感测试夹具，纳入权限和保留期管理，并用独立验收测试确认修复。

## 参考资料

- GitHub：<https://github.com/tonquoc0407/capybara>
- OpenTelemetry：<https://opentelemetry.io/>
