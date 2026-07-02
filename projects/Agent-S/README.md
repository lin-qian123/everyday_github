# Agent-S

- GitHub：<https://github.com/simular-ai/Agent-S>
- 官方文章：<https://www.simular.ai/articles/agent-s3>
- 抓取时间：2026-07-03（Asia/Shanghai）
- 今日信号：官方站点页面显示 `Agent S3 - Human-level Computer Use with Wide Scaling` 于 2026-07-02 发布；GitHub API 显示抓取时约 `12k stars / 1.4k forks`。

## 定位

`Agent-S` 是 Simular AI 的开源 computer-use / GUI agent 框架，目标是让 agent 像人一样操作电脑、浏览器和桌面应用。它属于 GUI agent 与 Agent-Computer Interface 路线，不是普通聊天助手，也不是只会改代码的 CLI agent。

最新的 Agent S3 版本强调在 OSWorld 等基准上的宽扩展推理与行为选择，并在 README 中宣称 100-step 设置下接近或超过人类水平表现。

## 用法

项目以 Python 包 `gui-agents` 的形式提供：

```bash
pip install gui-agents
```

本地开发可从源码安装：

```bash
git clone https://github.com/simular-ai/Agent-S.git
cd Agent-S
pip install -e .
```

README 提醒还需要安装 OCR 依赖，例如 macOS 上的：

```bash
brew install tesseract
```

配置模型 API 后，可在 macOS、Windows、Linux 等桌面环境中运行 GUI agent 任务。

## 原理

Agent-S 路线围绕“观察屏幕 -> 规划动作 -> 调用桌面控制工具 -> 记忆和复盘”展开。S3 版本的公开材料重点强调：

1. 对 OSWorld、WindowsAgentArena、AndroidWorld 等 GUI/OS 操作基准的泛化能力。
2. 使用宽扩展和多 rollout 选择提高复杂任务成功率。
3. 将视觉 grounding、规划、记忆和行为选择接成可运行的桌面 agent。

这条线的核心难点是长期任务中的状态理解、屏幕定位、动作误差恢复和安全边界。

## 价值

- 对 GUI agent 研究：提供可运行的开源框架和公开 benchmark 结果。
- 对产品原型：适合评估“agent 直接操作现有软件”能否替代传统 API 集成。
- 对本仓库：与 `cua`、`UI-TARS-desktop`、`GUI-Agents-Paper-List`、`browser-use` 构成 computer-use agent 观察链。

## 风险边界

- 桌面 agent 需要实际控制电脑，误操作、权限越界和隐私泄露风险高于普通聊天/代码补全。
- Benchmark 成绩不等于真实生产环境稳定性；桌面应用版本、分辨率、语言和网络状态都会影响结果。
- 多 rollout 和宽扩展可能显著增加模型调用成本，不能只看成功率。

## 补充建议

- 后续应关注 Agent S3 的代码、论文、视频演示和第三方复测是否一致。
- 与 OpenAI / Anthropic 的 computer-use 能力、`cua` 基础设施和 UI-TARS 系列做横向比较。
- 如果用于真实机器，建议放在隔离账号、虚拟机或低权限沙箱中验证。

## 参考资料

- GitHub 仓库：<https://github.com/simular-ai/Agent-S>
- Agent S3 官方文章：<https://www.simular.ai/articles/agent-s3>
- Agent S3 YouTube 视频：<https://www.youtube.com/watch?v=VHr0a3UBsh4>
- Simular 官网：<https://www.simular.ai>
