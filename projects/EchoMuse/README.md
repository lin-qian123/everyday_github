<!-- markdownlint-disable MD013 -->

# EchoMuse（wilbowes/EchoMuse）

> 上游仓库：<https://github.com/wilbowes/EchoMuse> · 归类：语音、视频与多模态 · 本页基于 2026-10-05 的 GitHub API、README、rooting / listening / voice pipeline 文档、Release 与 LICENSE / NOTICE 静态整理，未解锁 Echo Dot、刷写固件、连接 Home Assistant、采集音频或验证局域网安全。

- 抓取快照：1,040 stars、79 forks、150 open issues。
- 热度信号：GitHub Python Trending 抓取时约 +50 当日 stars。
- 版本与许可：根项目 MIT；稳定固件 `v2.17.0`、预发布 `v2.18.0-ea.1`、emOS `emos-v0.10`，第三方组件保留各自许可证。

## 定位

EchoMuse 把 2016 年第二代 Echo Dot 改造成 Home Assistant Assist 的本地语音卫星。它替换或叠加原设备软件，复用麦克风阵列、扬声器、灯环和按钮；局域网 controller 负责 wake word、设备管理与 dashboard，STT、意图和 TTS 则由用户自己的 Home Assistant pipeline 完成。

## 用法

先在 Linux 上通过上游依赖的 `amonet-biscuit` 和 USB 解锁指定型号 Echo Dot，再用 Home Assistant add-on 或 Docker 运行 controller；浏览器 wizard 通过 USB 安装 emOS / FireOS 路径、写入 Wi-Fi 并完成配对。设备会被 Home Assistant 发现为 ESPHome voice satellite，可配置本机或 controller 侧 wake word、音乐、定时器和自定义唤醒词。

## 原理

设备侧采集多通道音频并经局域网送入 controller；默认可在 Dot 上做 wake-word 检测，命中后才发送语音，也可改为 controller 持续接收麦克风流。controller 把语音 turn 桥接到 Home Assistant Assist，并管理多设备仲裁、AEC / 降噪、固件更新、TLS / token 配对和媒体播放；最终云端与否由 Assist pipeline 决定。

## 价值

它为仍具良好麦克风和扬声器的旧设备提供可自托管的再利用路径，并把语音识别、LLM 和 TTS 选择权交回 Home Assistant。公开的硬件分析、协议、音频状态和工程日志也有助于研究远场语音卫星，而不只交付一个黑盒镜像。

## 风险边界

- 仅支持 Echo Dot 2，解锁失败可 soft-brick；恢复依赖第三方 XDA 工具和具体 FireOS 状态，不能把 wizard 写成零风险刷机。
- “无 Amazon 账号 / 无项目云”不等于全链路离线：Assist pipeline 可能使用云 STT / LLM / TTS，controller 还会按配置访问 GitHub 检查更新。
- controller 侧 wake-word 模式会持续把麦克风流发送到局域网 controller；即使设备侧检测，误唤醒仍可能上传数秒非预期音频。软件 mute 不是物理断麦。
- 设备与 controller 的 TLS / token、配对窗口、旧固件兼容和 Home Assistant 凭据都需按版本实测；局域网并非自动可信边界。
- 根 MIT 不覆盖所有 BusyBox、wpa_supplicant、unlock 工具、模型与设备固件；Amazon 商标和硬件保修 / 法域问题也独立存在。
- README 列出 3.5 mm 麦克风停顿、FireOS 6 / WPA3 和 timer / announcement 已知问题；本轮未复测识别率、AEC、更新回滚和多 Dot 仲裁。

## 补充建议

只用确认型号和可恢复备份的闲置设备，先保存原 boot image；把 controller 与智能家居生产网隔离，先固定稳定固件 `v2.17.0` 与 `emos-v0.10`，核对设备是否显示 TLS / token 已生效。用本地 Whisper / Piper 和虚构命令测试误唤醒、断网、更新回滚、mute、录音保留与 support bundle 脱敏后再接真实家庭自动化。

## 参考资料

- [GitHub 仓库](https://github.com/wilbowes/EchoMuse)
- [GitHub REST API](https://api.github.com/repos/wilbowes/EchoMuse)
- [README、隐私与已知问题](https://github.com/wilbowes/EchoMuse/blob/main/README.md)
- [Quickstart](https://github.com/wilbowes/EchoMuse/blob/main/docs/quickstart.md)
- [Rooting 风险](https://github.com/wilbowes/EchoMuse/blob/main/docs/rooting.md)
- [监听模式](https://github.com/wilbowes/EchoMuse/blob/main/docs/listening.md)
- [Voice pipeline](https://github.com/wilbowes/EchoMuse/blob/main/docs/voice-pipeline.md)
- [Releases](https://github.com/wilbowes/EchoMuse/releases)
- [NOTICE](https://github.com/wilbowes/EchoMuse/blob/main/NOTICE.md)
- [LICENSE](https://github.com/wilbowes/EchoMuse/blob/main/LICENSE)
