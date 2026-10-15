<!-- markdownlint-disable MD013 -->

# Phone Harness（ShawnPana/phone-harness）中文解读

> 上游仓库：<https://github.com/ShawnPana/phone-harness> · 归类：Agent 框架与技能生态 · 证据快照：2026-10-16（Asia/Shanghai）。API：3,665 stars / 371 forks / 62 open issues；MIT；Release / Python manifest `0.3.2` / `0.3.2`。本页为上游文档与相关源码的静态整理，未安装运行、接入真实数据 / 凭据、复测性能或完成全面安全审计。

## 定位

Phone Harness 让 Claude Code、Codex 等宿主通过统一的 Python helpers 操作真实或云端手机。桌面 iPhone 依赖 macOS iPhone Mirroring，Android 依赖 adb，云端 iPhone 走 HTTPS。它提供屏幕观察、定位与动作执行链，适合受监督的手机 UI 测试和重复操作。

## 用法

官方 onboarding 推荐用 uv 和 Python 3.12 安装；先固定 `phone-harness==0.3.2`，阅读 `onboarding.md`，由用户完成配对、屏幕录制 / 辅助功能授权或 adb 确认，再运行 `phone-harness --doctor`。先执行 `phone-harness config set telemetry false`，从测试手机的设置 / 天气页只读观察开始；helpers 如 `screen()`、`find_text()`、`tap()`、`type_text()` 由 CLI 预载。

## 原理

- 本地 iPhone：捕获镜像窗口，用 Apple Vision OCR 得到文字和坐标，再发 HID 事件完成点击、滑动和输入。
- Android：通过 adb `screencap`、accessibility tree 与 `input` 获取屏幕并操作；可走 USB 或网络。
- 云端设备：Android 仍用 adb；iPhone 通过 HTTPS POST 操作、在宿主 OCR。`cloud start` / `cloud stop` 管理租用会话，属于额外托管服务。

## 价值

- 将“看屏幕 → 找目标 → 动作 → 重新观察”变成可脚本化接口，方便复用小型测试助手。
- 跨 iOS / Android 尽量保持 helper 一致，降低宿主编写平台专用自动化的成本。
- `--doctor`、明确的配对步骤与版本输出便于定位授权、窗口和连接问题。

## 风险边界

- 真实手机含私人消息、验证码和支付入口；点击与输入可以产生外发、下单等真实副作用，屏幕文字也可能向 Agent 注入指令。
- `config.py` 默认 `telemetry=True`；遥测源码向 PostHog 发送 CLI event，其结构可携带 task（截断至 20,000 字符）、output、steps、错误和宿主 / 模型标识。不能将“匿名 usage”理解成不传任务内容；关闭后仍应检查实际网络。
- iPhone 解锁会暂停镜像；PIN 锁定 Android 需要用户，且不支持多点触控、相机 / Face ID 流程，DRM 画面可能黑屏。不要据此期待无人值守跨锁屏执行。
- 云手机引入托管方、登录状态与计费边界；本地 MIT 代码许可不代表云服务免费或私有数据只留本地。

## 补充建议

- 用无私人账号的备用手机先做 10 个可恢复 UI 用例，记录 OCR 漏检、误点与成功后的画面证据。
- 为支付、发消息、删除、登录 / 2FA 等动作设置独立确认；限制 adb 监听与网络可达范围。
- 以 `PHONE_HARNESS_TELEMETRY=0` 或持久配置关闭遥测，检查截图、workspace 与日志的保留，云会话结束核对 stop 和账单。

## 参考资料

- 上游仓库：<https://github.com/ShawnPana/phone-harness>
- GitHub REST API：<https://api.github.com/repos/ShawnPana/phone-harness>
- 使用说明：<https://github.com/ShawnPana/phone-harness/blob/main/README.md>
- 安装排错：<https://github.com/ShawnPana/phone-harness/blob/main/install.md>
- 人工配对与 onboarding：<https://github.com/ShawnPana/phone-harness/blob/main/onboarding.md>
- 默认配置：<https://github.com/ShawnPana/phone-harness/blob/main/src/phone_harness/config.py>
- 遥测数据结构：<https://github.com/ShawnPana/phone-harness/blob/main/src/phone_harness/telemetry.py>
- Python manifest：<https://github.com/ShawnPana/phone-harness/blob/main/pyproject.toml>
- LICENSE：<https://github.com/ShawnPana/phone-harness/blob/main/LICENSE>
- Releases：<https://github.com/ShawnPana/phone-harness/releases>
