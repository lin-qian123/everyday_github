<!-- markdownlint-disable MD013 -->

# Concat

## 定位

Concat 是本地视频编辑器，结合 Rust 原生引擎、GPU 合成、多轨时间线、字幕、语音和背景处理，并提供 MCP / JSON-RPC 自动编辑。README 将其定位为 CapCut 替代，主线仍标 beta；跨平台列表不等于每个平台能力和性能完全相同。

2026-10-30 快照：Rust daily +262 stars；API 累计 12,640 stars / 1,552 forks / 246 open issues（含 PR）。核读 main `f0c0169628c6`；发行 API 首项 [v0.2.8](https://github.com/jub0t/Concat/releases/tag/v0.2.8)，2026-10-20 UTC。以下为文档与有限源码核读，未安装运行。

## 用法

先从固定 GitHub Release 挑选对应平台包并核对校验信息。纯源码构建要求 Rust 1.93+、FFmpeg 7+ 开发库、cmake 和 C++ 编译器：

```bash
git clone https://github.com/jub0t/Concat
cd Concat/src
cargo run -p concat
```

Agent 入口是 concat --mcp。默认 auto：有已启用 Automation 的窗口时连接窗口 API，否则可进入 headless；希望连接失败就停止时显式用 --mcp window。字幕 / 声音 / 抠像模型从 Settings 下载，下载后按上游说明可离线使用。以上均未执行。

## 原理

GUI 和自动化共用编辑命令；MCP 工具 schema 由 API 类型生成，可导入素材、裁切、加字幕、设关键帧、预览和导出。项目进程锁避免另一个进程覆盖打开的工程，编辑通常保留内存直到 project_save。文档明确当前 Agent 不能边看边改窗口里已打开的工程，live mode 仍是计划。

## 价值

适合把可复现剪辑步骤交给脚本或 Agent，同时保留工程和成片两个验收对象。JSON-RPC / MCP 让批量字幕、模板生成和固定规格导出更容易接入工作流。

## 风险边界

- 根为 AGPLv3 文本；README 标 AGPL-3.0-or-later。再分发或服务化修改版时须核许可范围，FFmpeg、声音和模型另查授权。
- API 文档要求 token；远程 API 默认关闭、开启后默认 loopback，但传输本身不加密，暴露其他地址需补传输安全。
- MCP 写入默认限 home；headless 可用 CONCAT_MCP_ROOTS 扩大范围。项目锁和路径规则不是 OS sandbox，也不保证恶意媒体解码安全。
- Windows 当前未签名；不要把未来签名政策当成现有制品已签名。模型下载校验、更新源和发行身份需核。
- 无遥测、无主动上传是 CODE_SIGNING 中的政策声明，本轮未抓包；用户请求的模型下载和版本检查仍联网。
- 语音克隆需声音授权，自动字幕需校对；4K60、10-bit、硬件解码和导出成功率未在本轮验证。

## 补充建议

用有权素材建立短片 fixture，验证字幕错字、时间码、音画同步、色彩、工程回读和导出。分别测 auto / window / headless 的项目冲突与 token 拒绝，保留测试版本、模型来源、工程和最终媒体。

## 参考资料

- [上游仓库](https://github.com/jub0t/Concat)、[仓库 API](https://api.github.com/repos/jub0t/Concat)。
- [README.md](https://github.com/jub0t/Concat/blob/f0c0169628c61de7311f7fc15ee5be82dd611d2e/README.md)。
- [docs/MCP.md](https://github.com/jub0t/Concat/blob/f0c0169628c61de7311f7fc15ee5be82dd611d2e/docs/MCP.md)。
- [CODE_SIGNING.md](https://github.com/jub0t/Concat/blob/f0c0169628c61de7311f7fc15ee5be82dd611d2e/CODE_SIGNING.md)。
- [SECURITY.md](https://github.com/jub0t/Concat/blob/f0c0169628c61de7311f7fc15ee5be82dd611d2e/SECURITY.md)。
- [LICENSE](https://github.com/jub0t/Concat/blob/f0c0169628c61de7311f7fc15ee5be82dd611d2e/LICENSE)。
