<!-- markdownlint-disable MD013 -->

# Open Computer Use

> 更新：2026-10-19（Asia/Shanghai）。分类：Agent 框架与技能生态。上游 `iFurySt/open-computer-use`；本文基于官方榜单、认证 API 与文档 / 源码静态核验，未安装运行。源码快照 `5136415f52b8`；Release 与主分支行为分别说明。热度见[当日官方榜单](https://github.com/trending/swift?since=daily)。

## 定位

第三方开源桌面控制服务，通过 MCP 向 agent 提供 macOS、Linux、Windows 的 UI 状态与动作，另有本地 JS / REPL 包装。macOS 利用 Accessibility / 截图，Linux / Windows 走各自原生后端；功能和可靠性不能跨平台直接类推。[来源 1](https://github.com/iFurySt/open-computer-use/blob/5136415f52b87f419227bae28767cf469a6bc3b5/README.md)[来源 4](https://github.com/iFurySt/open-computer-use/blob/5136415f52b87f419227bae28767cf469a6bc3b5/docs/SECURITY.md)

官方 Swift Trending 约 +29 当日 stars；API 为 2,499 / 240 / 25（stars / forks / open issues），稳定 Release v1.1.2，MIT。它受 Codex Computer Use 启发，不是 OpenAI 官方项目，也不代表拥有相同审批机制。[来源 1](https://github.com/iFurySt/open-computer-use/blob/5136415f52b87f419227bae28767cf469a6bc3b5/README.md)[来源 2](https://api.github.com/repos/iFurySt/open-computer-use)[来源 3](https://github.com/iFurySt/open-computer-use/releases/tag/v1.1.2)

## 用法

按上游 npm / Release 安装，macOS 需 14.0+，并给其专用 app 授予 Accessibility 与 Screen Recording。先检查权限与 runtime 能力，再选择离散 MCP tools 或 JS 接口：[来源 1](https://github.com/iFurySt/open-computer-use/blob/5136415f52b87f419227bae28767cf469a6bc3b5/README.md)

```bash
ocu doctor --json
ocu capabilities --json
```

doctor 缺权限也可能 exit 0，调用者必须检查 allGranted，授权变化后重新查询。`install-codex-mcp` 等命令会写对应客户端配置，应先备份；可手工配置 `open-computer-use mcp`。本轮仅审文档与源码，未安装、授权或控制用户桌面。

## 原理

MCP host 经本地 stdio 调 native runtime；macOS CLI 与 app agent 使用权限收窄的 Unix socket。工具通过 app 参数与状态快照定位目标；JS adapter 也经 native MCP 调 CUA，但 JS 本身可读文件、环境、模块和网络。[来源 4](https://github.com/iFurySt/open-computer-use/blob/5136415f52b87f419227bae28767cf469a6bc3b5/docs/SECURITY.md)

截图通常在内存编码回传，是否被发给模型、写入 host 日志和长期保存，由 MCP host 另行决定。项目本身不引入第三方上传服务的声明，不能扩大成整个 agent 链路零外发。

## 价值

为没有自带桌面工具的 MCP 客户端提供统一接入，结构化可访问性状态可降低完全依赖截图坐标的成本。定向 query、权限检查和失败时拒绝回退的设计值得评估；“非侵入”仍需针对应用、系统版本和动作验证。

## 风险边界

- 上游明确当前缺 session approval / 动态 app policy；仅有密码管理器 denylist，终端、浏览器和系统组件并非普遍阻止。调用者需自行约束高影响动作。[来源 4](https://github.com/iFurySt/open-computer-use/blob/5136415f52b87f419227bae28767cf469a6bc3b5/docs/SECURITY.md)
- `ocu js` 是任意本地 JavaScript，Worker 超时和 native safety gates 不构成完整 JS sandbox；只接受离散工具的 host 可直连 `mcp`。[来源 4](https://github.com/iFurySt/open-computer-use/blob/5136415f52b87f419227bae28767cf469a6bc3b5/docs/SECURITY.md)
- global pointer / keyboard 可影响真实前台；global fallback 需额外环境开关，部分私有 SPI 不受系统兼容承诺保护。get_app_state 也可能改变遮挡渲染状态，不能一概视为无副作用。[来源 4](https://github.com/iFurySt/open-computer-use/blob/5136415f52b87f419227bae28767cf469a6bc3b5/docs/SECURITY.md)
- Locked Use 是另一路需管理员权限的系统认证集成，会安装组件并加入锁屏授权规则；安全文档仍列自动解锁、Keychain、Secure Input、故障等未完全通过项。不能因指南提供 enable 命令就视作已完成安全验收。[来源 4](https://github.com/iFurySt/open-computer-use/blob/5136415f52b87f419227bae28767cf469a6bc3b5/docs/SECURITY.md)[来源 5](https://github.com/iFurySt/open-computer-use/blob/5136415f52b87f419227bae28767cf469a6bc3b5/docs/locked-use.en.md)
- MIT 与供应链文档不等于当前下载制品已核签名 / provenance。本轮未下载二进制或复测上游测试。[来源 6](https://github.com/iFurySt/open-computer-use/blob/5136415f52b87f419227bae28767cf469a6bc3b5/docs/SUPPLY_CHAIN_SECURITY.md)[来源 7](https://github.com/iFurySt/open-computer-use/blob/5136415f52b87f419227bae28767cf469a6bc3b5/LICENSE)

## 补充建议

先用一次性桌面账户和无隐私 TextEdit 类应用验证观察、点击、目标失效、遮挡及权限拒绝，再扩大目标。普通 MCP、JS REPL 与 Locked Use 分别评估；涉及系统认证的路径需专门恢复演练，不跟普通安装合并启用。

## 参考资料

1. [README 与 doctor 语义](https://github.com/iFurySt/open-computer-use/blob/5136415f52b87f419227bae28767cf469a6bc3b5/README.md)
2. [仓库 API](https://api.github.com/repos/iFurySt/open-computer-use)
3. [v1.1.2 Release](https://github.com/iFurySt/open-computer-use/releases/tag/v1.1.2)
4. [安全默认与未闭环项](https://github.com/iFurySt/open-computer-use/blob/5136415f52b87f419227bae28767cf469a6bc3b5/docs/SECURITY.md)
5. [Locked Use 安装范围](https://github.com/iFurySt/open-computer-use/blob/5136415f52b87f419227bae28767cf469a6bc3b5/docs/locked-use.en.md)
6. [供应链说明](https://github.com/iFurySt/open-computer-use/blob/5136415f52b87f419227bae28767cf469a6bc3b5/docs/SUPPLY_CHAIN_SECURITY.md)
7. [LICENSE](https://github.com/iFurySt/open-computer-use/blob/5136415f52b87f419227bae28767cf469a6bc3b5/LICENSE)
8. [上游 README 演示视频](https://www.youtube.com/watch?v=2s6aVpGiwaQ)
