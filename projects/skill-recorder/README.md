<!-- markdownlint-disable MD013 -->

# Skill Recorder：从真实工作录制生成可审阅的技能与自动化

- 主上游：[microsoft/skill-recorder](https://github.com/microsoft/skill-recorder)；repository ID `1316443307`。
- 采样日期：2026-10-27（Asia/Shanghai）；分类：Agent 框架与技能生态。
- API 累计快照：5,217 stars / 585 forks / 47 open issues（含 PR 口径），与榜单日增分开。
- 默认分支 `main`；本页主线静态依据固定在 `b05d59036182e897e1a60e90651e775cf5f97e8d`。发行 API 首项 [v0.7.0](https://github.com/microsoft/skill-recorder/releases/tag/v0.7.0)，UTC 2026-09-21T09:48:05Z，正式发行标记。
- 核验层级：读取一手文档、许可、元数据与所列部分实现；未安装运行上游、调用模型或复现实验。

## 定位

Skill Recorder 是 Microsoft 的 Electron 桌面工具，把一次真实操作整理为“意图＋有序步骤”，再生成 SKILL.md 或自动化流程。它希望优先使用 gh、网页读取等原生工具复做任务，而非简单按坐标回放点击；从一个样本泛化到其他任务仍需人工验收。

## 用法

从 Release 的 **Commit-pinned installation** 复制适合系统的完整命令，先阅读脚本和安装说明。当前发布方式是源码发行：下载固定 Node runtime，在本机构建应用；源码压缩包不是可直接启动的安装器。需要有 Copilot 权限的 GitHub 账号，macOS 为主要目标，Windows / Ubuntu 的支持与限制依所选发行核对。

使用顺序是 Record → Analyze → 审阅修改步骤 → Create。先用虚构资料录一个小任务，生成技能时可先打开 Review SKILL.md，再选择添加或导出。预览不写技能文件，但用户也能直接添加 / 导出，因此“提供预览”不能写成强制审批。

开发者在固定源码中可使用以下入口，本轮未执行：

```bash
npm ci
npm run compliance:licenses
npm run dev
```

主线 README 要求 Node.js 24；应用捆绑 Copilot CLI，并固定登录版本。源码主线与 v0.7.0 发行说明须分别阅读。

## 原理

Electron 汇集窗口切换、文档标题、浏览器 URL、剪贴板预览、屏幕关键帧和可选旁白。旁白在本机转写；只有从录制条打开的专用终端纳入完整终端记录，不监视所有既有终端。Analyze 将时间线、图像、转写与按需终端片段交给 Copilot 重建过程，技能 builder 再把该过程改写为可复用指令。

## 价值

适合把已有稳定工作流程转为可编辑的操作说明，减少仅靠口述需求遗漏细节的问题。分析结果、技能正文和试跑结果可以分开审阅；是否比人工写技能节省时间，要同时计算录制、纠错和后续维护成本。

## 风险边界

- **本地录制不等于本地推理**：选择 Analyze 会发送上述记录到 GitHub 云端。敏感扫描 / 脱敏不是完整性保证，旁白、屏幕、URL 和剪贴板都可能含个人或业务信息。
- `FULL_CAPTURE` 对所有支持的信号设为 true，没有按档位选择采集面的用户入口；终端虽只采专用窗口，但其本地 transcript 没有应用级大小上限。
- README 称每次录制提醒隐私；当前 `RecordingPrivacySession` 与 main 的接线实际按**应用进程生命周期**记住已确认状态，确认后后续录制可直接开始。不要把弹窗视为每次录制的强制关卡；本轮未启动 UI 复现。
- SKILL.md 的审阅不会降低执行宿主的权限。生成自动化后仍需检查触发条件、外部写入、账户与数据范围。
- MIT 适用于本仓库代码，捆绑组件、模型和 Copilot 服务条款另计。

## 补充建议

建立“录制样本—人工修订步骤—生成技能—新样本试跑”的小型验收集；用第二个样本检查是否误记了固定用户名、路径或秘密。先只导出技能，在测试账号核对外部副作用后再安排自动化；定期清理录制原始文件，并单独记录 Copilot 数据出口与费用。

## 参考资料

- [README.md](https://github.com/microsoft/skill-recorder/blob/b05d59036182e897e1a60e90651e775cf5f97e8d/README.md)。
- [common/config.ts](https://github.com/microsoft/skill-recorder/blob/b05d59036182e897e1a60e90651e775cf5f97e8d/common/config.ts)。
- [electron/recording-privacy.ts](https://github.com/microsoft/skill-recorder/blob/b05d59036182e897e1a60e90651e775cf5f97e8d/electron/recording-privacy.ts)。
- [electron/main.ts](https://github.com/microsoft/skill-recorder/blob/b05d59036182e897e1a60e90651e775cf5f97e8d/electron/main.ts)。
- [package.json](https://github.com/microsoft/skill-recorder/blob/b05d59036182e897e1a60e90651e775cf5f97e8d/package.json)。
- [LICENSE](https://github.com/microsoft/skill-recorder/blob/b05d59036182e897e1a60e90651e775cf5f97e8d/LICENSE)。
- [仓库 API](https://api.github.com/repos/microsoft/skill-recorder)、[发行 API](https://api.github.com/repos/microsoft/skill-recorder/releases?per_page=1)；动态元数据仅代表本轮采样。
- 事实依据为以上一手材料；价值、风险判断与建议为本库工程分析，未写作实测结论。
