<!-- markdownlint-disable MD013 -->

# tiny-engineer

- 主上游：[jamro/tiny-engineer](https://github.com/jamro/tiny-engineer)
- 分类：前端、UI 与 Agent 交互层。
- 核验日期：2026-10-24（Asia/Shanghai）；默认分支 `main` 快照 `7b32626b50c2`。
- [API](https://api.github.com/repos/jamro/tiny-engineer) 快照：832 stars / 107 forks / 7 open issues；发行列表首项 [v0.2.0](https://github.com/jamro/tiny-engineer/releases/tag/v0.2.0)（UTC 2026-10-05，正式）。累计量不是今日增长，主线也不等于发行版。

## 定位

Tiny Engineer 是把编码 Agent 状态映射为动作的可打印桌面机器人：读文件时张望、写代码时敲键盘、思考时抬头、完成时敲铃。它展示工具事件，不证明 Agent 实际任务已经正确完成。 [README.md](https://github.com/jamro/tiny-engineer/blob/7b32626b50c2479ac272f0d8fcccaf83c15c4280/README.md)

## 用法

按组装指南准备 ESP32-C3、五个 SG90 舵机、OLED、扬声器、控制板与打印件，使用 5 V / 至少 2 A 电源。固件配置 Wi-Fi 后，可按文档为 Claude Code / Cursor / Antigravity 安装 hooks；Codex 等可用自定义 HTTP 或 USB serial 接入。

```sh
npx -y tiny-engineer setup
```

这是上游集成命令，实际使用应先核固定 npm 版本及它修改的 hook 配置。先让机器人执行一个低幅度测试动作，再接 Agent；本轮未运行该命令。 [README.md](https://github.com/jamro/tiny-engineer/blob/7b32626b50c2479ac272f0d8fcccaf83c15c4280/README.md)、[docs/integration.md](https://github.com/jamro/tiny-engineer/blob/7b32626b50c2479ac272f0d8fcccaf83c15c4280/docs/integration.md)

## 原理

宿主 hook 将 Agent 生命周期事件转换为 Wi-Fi HTTP 或 USB serial 命令；ESP32 固件驱动舵机、面部与声音。可用 `/anim` 等 API 控制，语音播放有独立接口。机器人本身不承担 LLM 推理，且事件灯效不能替代测试结果。 [README.md](https://github.com/jamro/tiny-engineer/blob/7b32626b50c2479ac272f0d8fcccaf83c15c4280/README.md)、[docs/api.md](https://github.com/jamro/tiny-engineer/blob/7b32626b50c2479ac272f0d8fcccaf83c15c4280/docs/api.md)

## 价值

适合硬件入门、Agent 交互原型与长任务状态提醒。吸引力在于可改 CAD、固件和事件映射；制作成本必须包含打印、装配、供电与调试，不把宣传中的单块 PCB 意向价写成完整成品成本。 [README.md](https://github.com/jamro/tiny-engineer/blob/7b32626b50c2479ac272f0d8fcccaf83c15c4280/README.md)

## 风险边界

- 固件 HTTP 默认在 LAN 的 80 端口服务，`access_token` 默认空、JSON API 免认证；设置 token 后按 Bearer 校验，HTML 控制页仍公开。首次配网 AP 也默认无密码。应在受控网络先配置认证，或评估 USB serial 路径。 [SECURITY.md](https://github.com/jamro/tiny-engineer/blob/7b32626b50c2479ac272f0d8fcccaf83c15c4280/SECURITY.md)
- 设备只支持 2.4 GHz；需要验证舵机供电、机械限位与停机，避免把自动动作当成无人值守硬件安全保证。 [README.md](https://github.com/jamro/tiny-engineer/blob/7b32626b50c2479ac272f0d8fcccaf83c15c4280/README.md)
- 软件 / 文档为 MIT；指定机械制造文件与 KiCad 硬件采用 CERN-OHL-S-2.0，修改后分发产品涉及对应完整源文件要求；名称和 logo 另有商标边界。不能凭 API 的 NOASSERTION 或软件 MIT 徽标概括全仓库。 [LICENSING.md](https://github.com/jamro/tiny-engineer/blob/7b32626b50c2479ac272f0d8fcccaf83c15c4280/LICENSING.md)、[3d_models/LICENSE](https://github.com/jamro/tiny-engineer/blob/7b32626b50c2479ac272f0d8fcccaf83c15c4280/3d_models/LICENSE)

## 补充建议

先用合成事件测乱序、断连、重复完成和异常退出，机器人敲铃时仍以宿主任务状态为准。固定固件 / npm 版本，记录接线、供电、活动范围和 token 配置。本轮未采购、打印、烧录、联机控制或验证机械安全。

## 参考资料

- [README.md](https://github.com/jamro/tiny-engineer/blob/7b32626b50c2479ac272f0d8fcccaf83c15c4280/README.md)（固定 commit）。
- [docs/integration.md](https://github.com/jamro/tiny-engineer/blob/7b32626b50c2479ac272f0d8fcccaf83c15c4280/docs/integration.md)（固定 commit）。
- [docs/api.md](https://github.com/jamro/tiny-engineer/blob/7b32626b50c2479ac272f0d8fcccaf83c15c4280/docs/api.md)（固定 commit）。
- [SECURITY.md](https://github.com/jamro/tiny-engineer/blob/7b32626b50c2479ac272f0d8fcccaf83c15c4280/SECURITY.md)（固定 commit）。
- [LICENSING.md](https://github.com/jamro/tiny-engineer/blob/7b32626b50c2479ac272f0d8fcccaf83c15c4280/LICENSING.md)（固定 commit）。
- [3d_models/LICENSE](https://github.com/jamro/tiny-engineer/blob/7b32626b50c2479ac272f0d8fcccaf83c15c4280/3d_models/LICENSE)（固定 commit）。
- [发行列表](https://github.com/jamro/tiny-engineer/releases)、[仓库 API](https://api.github.com/repos/jamro/tiny-engineer)（动态状态）。
