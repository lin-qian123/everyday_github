# proxybaby

## 定位

`proxybaby` 是面向 macOS、Windows、Linux 的开源 HTTP(S) 代理调试器，提供 SSE、OpenAI、Anthropic 与 ACP 会话的可视化，并带 CLI、规则与 agent skill。截至 2026-08-01 的 GitHub API 快照，它创建于 2026-07-31，约 1 star、0 forks；许可证字段为 `NOASSERTION`，需在使用前人工确认。

## 用法

从项目的 Releases 获取对应平台安装包，先在隔离测试环境阅读根证书安装、系统代理和退出恢复说明。仅对自有或已获授权的应用配置抓包；使用 CLI、规则改写、断点和会话导出前，先确认范围与敏感数据处理策略。

## 原理

它通过本地代理观察 HTTP(S)、HTTP/2、WebSocket 与 SSE 流量，使用动态证书实现授权范围内的 HTTPS 解密；界面再按协议对 AI 流式会话和工具调用字段进行结构化展示。规则与脚本可改写请求或响应。

## 价值

- 对 agent 调试而言，能把模型调用、流式 token、tool-use 与协议错误放进同一观察面。
- 规则、HAR 与 CLI 有助于复现网络问题并将调试步骤自动化。

## 风险边界

- HTTPS MITM、证书信任与流量导出可暴露 API key、会话内容、Cookie 和个人数据；未经授权不得截获他人或生产流量。
- 改写与断点可能改变真实请求，不能替代生产故障处置流程。
- 项目对比表和“唯一”等宣传为作者主张；许可证状态及平台安全性应以发布包、签名和独立测试为准。

## 补充建议

使用专用测试账号、临时 CA、域名 allowlist 与最短日志保留期；运行后移除不再需要的证书与代理设置。对导出物做密钥扫描并限制共享范围。

## 参考资料

- GitHub：<https://github.com/imcuttle/proxybaby>
- Releases：<https://github.com/imcuttle/proxybaby/releases>
- GitHub API 快照：<https://api.github.com/repos/imcuttle/proxybaby>
