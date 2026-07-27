# stackchan-cloud-mcp

## 定位

`stackchan-cloud-mcp` 为 StackChan 桌面机器人补齐云端 MCP 网关接入：通过 OAuth 2.1、VPS、Cloudflare Tunnel 和守护进程，让 claude.ai 可驱动语音、表情、头部与灯光等设备动作。

截至 2026-07-28，GitHub API 显示其创建于 2026-07-27，约 8 stars、2 forks；属于早期开发者信号。

## 用法

需要一台可访问的 VPS、域名或 Tunnel、刷入兼容固件的 StackChan，以及上游网关。先按部署文档配置环境变量与单租户 OAuth 门，再在隔离网络中验证设备连接、TTS/STT 和断线恢复。

## 原理

项目把 claude.ai 的 HTTPS MCP 请求接入 OAuth 代理，再转给 StackChan 网关的 WebSocket；反射弧守护进程负责重连后恢复设备状态。仓库同时给出针对 NAT、音频、表情尺寸和模型下载问题的上游补丁与验证记录。

## 价值

- 将“需要常开电脑”的桌面机器人变为可远程管理的设备工作流。
- 对具身 MCP 的认证、长连接、恢复和可见交互问题提供了具体工程样本。

## 风险边界

- 机器人带摄像头与麦克风；远程控制前必须取得现场同意，并提供明确的采集提示和最小化留存。
- OAuth 门是单租户设计，不应直接当作多用户公网服务。
- VPS、Tunnel、上游 TTS/STT/LLM 与设备固件都会扩大攻击面和成本；“长期可用”主张需独立复现。

## 补充建议

限制入口 IP、轮换密钥、为每项传感器动作留审计记录；在真实部署前用无摄像头/麦克风的测试模式完成渗透检查与断网恢复测试。

## 参考资料

- GitHub：<https://github.com/tianyupaipai-cmd/stackchan-cloud-mcp>
- GitHub API 快照：<https://api.github.com/repos/tianyupaipai-cmd/stackchan-cloud-mcp>
