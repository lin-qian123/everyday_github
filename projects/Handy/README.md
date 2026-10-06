<!-- markdownlint-disable MD013 -->

# Handy（cjpais/Handy）

> 上游仓库：<https://github.com/cjpais/Handy> · 归类：语音、视频与多模态 · 本页基于 2026-10-07 的 GitHub API、README、release、签名说明与 LICENSE 静态整理，未授予麦克风 / 辅助功能权限、下载模型或用真实语音测试识别质量。

- 抓取快照：33,047 stars、3,072 forks、164 open issues。
- 热度信号：GitHub Rust Trending 抓取时约 +103 当日 stars；最后 push 为 2026-10-05。
- 版本与许可：latest Release / tag 为 `v0.9.8`，MIT；本页固定审计 commit `a94b403e0610`。

## 定位

Handy 是跨 Windows、macOS、Linux 的本地语音转文字桌面应用：用户按快捷键录音，应用离线执行 VAD 与 ASR，再把文字输入当前应用。它强调免费、可扩展和核心转写不上传云端，主要价值是可访问性与日常听写。

## 用法

优先从 `v0.9.8` Release 取得对应平台制品，并按 README 使用 Tauri updater 公钥与 `.sig` 做签名校验；首次启动只授予麦克风和必要的辅助功能 / 输入权限。选择 Whisper Small / Medium / Turbo / Large 或 Parakeet V3 模型后，以无敏感短句校准语言、快捷键、粘贴方式与准确率，再决定是否保留历史和启用第三方集成。

## 原理

快捷键控制录音，Silero VAD 过滤静音，Whisper 或 Parakeet 在本机执行语音识别；结果进入历史，并通过剪贴板、模拟输入或平台工具写回当前文本框。不同系统用各自全局快捷键与输入机制，Linux 可依赖 `xdotool`、`wtype`、`ydotool` 或 `dotool`，模型文件保存在应用数据目录或 Hugging Face cache。

## 价值

核心转写可以在断网条件下运行，避免把每段语音交给托管 ASR，并覆盖常见桌面系统、不同模型与 GPU / CPU 路径。上游还提供制品签名校验说明、CLI 控制和已知限制，便于团队做可审计部署。

## 风险边界

- “完全离线”主要描述核心识别路径；首次下载模型、更新、官网、Homebrew / winget 和第三方 Raycast extension 仍有网络与独立供应链，需分别审计。
- 麦克风、全局快捷键、辅助功能、剪贴板和模拟输入都是高敏感权限；焦点变化或粘贴延迟可能把转写写入错误窗口，README 已记录相关已知问题。
- transcript history、词典、debug 日志与模型 cache 会留在本机；离线不等于自动加密、最小保留或多用户隔离。
- ASR 会误听姓名、数字、专业词和多语切换；转写结果不能直接驱动医疗、法律、财务或生产命令。
- MIT 覆盖应用代码，不自动覆盖 Whisper / Parakeet 权重、训练数据、第三方包与用户录音权利；会议和他人声音还需明确同意。
- 上游签名验证提高制品完整性，但不能替代源码复现、恶意依赖审计或运行权限控制；非官方包管理器条目也非 Handy 团队维护。

## 补充建议

在专用本地账户中测试，关闭自动发送 debug 日志，设定历史保留期并排除密码 / 医疗 / 客户数据；用授权语音金标按语言、口音、噪声、数字和专业词统计 WER / 人工返工。针对每个目标应用做粘贴回读，失败时只把结果留在可审阅窗口，不自动提交表单或命令。

## 参考资料

- [GitHub 仓库](https://github.com/cjpais/Handy)
- [GitHub REST API](https://api.github.com/repos/cjpais/Handy)
- [README 与工作原理](https://github.com/cjpais/Handy/blob/main/README.md)
- [v0.9.8 Release](https://github.com/cjpais/Handy/releases/tag/v0.9.8)
- [构建说明](https://github.com/cjpais/Handy/blob/main/BUILD.md)
- [Tauri updater 配置与公钥](https://github.com/cjpais/Handy/blob/main/src-tauri/tauri.conf.json)
- [MIT License](https://github.com/cjpais/Handy/blob/main/LICENSE)
- [已知 issues](https://github.com/cjpais/Handy/issues)
