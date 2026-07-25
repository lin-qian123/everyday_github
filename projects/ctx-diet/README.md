# ctx-diet

## 定位

`ctx-diet` 是一个 Claude Code `PostToolUse` hook，试图在工具输出进入上下文前压缩冗长内容。作者报告其个人机器上 91,287 次命令节省 65.6% 输入 token；截至 2026-07-26，仓库创建于 2026-07-25，约 2 stars、0 forks，MIT 许可。该指标是作者自测，尚无独立复现。

## 用法

项目要求 `bash` 与 `jq`。按 README 安装 hook 后，先运行其验证步骤，再在可丢弃的 Claude Code 项目中测试 `ps`、目录列表、大日志和失败测试输出；应确认报错与显式错误没有被压缩，并保留一键关闭 hook 的配置。

## 原理

Claude Code 的 `PostToolUse` 在工具执行后、输出入模前触发。hook 可根据命令/输出模式生成紧凑摘要，或通过 `updatedToolOutput` 替换原始输出；作者特别区分应压缩的冗余信息与必须原样保留的失败证据。

## 价值

- 针对长会话中“早期大输出被后续每轮携带”的成本放大问题。
- 用 hook 而非要求开发者手工少看日志，能把优化放到统一入口。
- MIT 且实现较小，便于审计、fork 和对照测试。

## 风险边界

- 压缩会损失细节，可能隐藏 stack trace、文件名、警告或安全线索，不能替代原始日志。
- README 已说明 `pipefail` 与失败正则等已知坑；错误配置可能让 hook 静默失效或误判成功。
- 节省率只来自作者环境，模型版本、工具习惯和会话长度不同会显著影响结果。

## 补充建议

为每次压缩保存原始输出的本地引用或可展开附件；建立包含失败测试、权限错误、敏感输出和超长 diff 的回归夹具，测量 token、诊断成功率及误压缩率，而非只看节省比例。

## 参考资料

- GitHub：<https://github.com/illuwa/ctx-diet>
- Claude Code hooks 文档：<https://docs.anthropic.com/en/docs/claude-code/hooks>
