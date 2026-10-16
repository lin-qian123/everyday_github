<!-- markdownlint-disable MD013 -->

# ARTEMIS（google/artemis）中文解读

> 上游仓库：<https://github.com/google/artemis> · 归类：Agent 框架与技能生态 · 证据快照：2026-10-17（Asia/Shanghai）。API：12,040 stars / 1,299 forks / 139 open issues；无 GitHub Release / tag；pyproject.toml `1.0`，Python ≥3.12；Apache-2.0；third_party 另保留上游许可。本页为上游资料与相关代码的静态整理，未安装运行、复测性能或完成全面安全审计。

## 定位

ARTEMIS 是 google/artemis 提供的 Android 自动化与测试系统，通过自然语言、CLI、Web、MCP 和 Python client 连接真实手机或模拟器。它将设备观察、动作执行、历史与诊断串起来，适合授权设备上的 UI 回归和缺陷复现；README 中的 iOS、本地轻量 VLM 等仍列在 roadmap。

## 用法

在备用 Android / emulator 开启 USB debugging，先审阅 `start.sh` 的系统工具安装和全局 IDE / MCP / rules 写入范围。配置模型后，可用 `uv run artemis run "Open Settings, find Battery and tell me current level" --profile flash` 做最小观察任务。Web console 默认 localhost:8000；优先手工生成单个 MCP 配置，不直接对全部 IDE 全局安装。首次任务可能自动安装 Accessibility Helper；可用 `ARTEMIS_HELPER_AUTO_INSTALL=false` 禁止，或按 README 卸载。

## 原理

- 观察综合 accessibility hierarchy、OCR 和视觉模型；元素索引优先，坐标与视觉定位作 fallback。
- Flash 是较快的 observe-and-act 循环；Pro 由 Planner / Operator、动作前 Safety Net 和只读 Checker 组成，支持计划检查点与诊断。
- 历史压缩、截图摘要、可检索会话记录和执行 replay 支撑长流程；MCP 向宿主暴露运行、设备状态、trace 与诊断工具。

## 价值

- 将操作结果和日志、截图、重放绑定，有助于把“Agent 说成功”转成可审查测试证据。
- Flash / Pro 允许按测试复杂度选择延迟与验证成本；同一 Python client 可接入现有测试框架。
- 真实价值应以自己的应用、系统版本和可恢复用例衡量，而不是直接采用作者展示的成功率。

## 风险边界

- 上游称 AndroidWorld 99%+、Flash 约 3–5 秒 / 步，均属于作者报告；本次未复测任务集合、模型版本、重试预算或失败判据，不能推广为任意 App 成功率。
- 控制台安全源码明确无用户账号，能连 TCP 端口者即 operator；Host / Origin 防护防浏览器跨源攻击，不是用户认证。远程访问应使用受控 tunnel，不能直接扩大监听面。
- 手机截图、日志、模型上下文、视频和本地 trace 都可能含敏感信息；手机 helper 只在设备 loopback 通信的声明不覆盖主程序向模型 provider 发出的数据。
- Pro 的 Safety Net 是模型 / 规则层检查；Flash README 明确不含同等动作前保护。支付、外发、删除等动作仍需独立授权。

## 补充建议

用无私人账号的设备建立 10 个金标用例，记录动作、最终界面、模型费用和异常恢复；先测只读导航，再测可逆写入。固定 commit、profile 与模型，收敛 ADB、MCP 与 console 网络范围，清理录像 / trace 并核对 helper 卸载。

## 参考资料

- 上游仓库：<https://github.com/google/artemis>
- GitHub REST API：<https://api.github.com/repos/google/artemis>
- README 与 benchmark 声明：<https://github.com/google/artemis/blob/main/README.md>
- Python manifest：<https://github.com/google/artemis/blob/main/pyproject.toml>
- 控制台安全边界：<https://github.com/google/artemis/blob/main/apps/admin_console/core/security.py>
- 控制台监听默认值：<https://github.com/google/artemis/blob/main/apps/admin_console/server.py>
- 模型与 profile 配置：<https://github.com/google/artemis/blob/main/config/artemis.jsonc>
- trace 本地存储：<https://github.com/google/artemis/blob/main/artemis/telemetry/storage/json_storage.py>
- 许可：<https://github.com/google/artemis/blob/main/LICENSE>
- Releases：<https://github.com/google/artemis/releases>
