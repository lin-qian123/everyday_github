<!-- markdownlint-disable MD013 -->

# hex

- 主上游：[anomalyco/hex](https://github.com/anomalyco/hex)
- 分类：语音、视频与多模态。
- 核验日期：2026-10-24（Asia/Shanghai）；默认分支 `main` 快照 `50fb90715427`。
- [API](https://api.github.com/repos/anomalyco/hex) 快照：557 stars / 70 forks / 49 open issues；发行列表首项 [app-v2.3.1](https://github.com/anomalyco/hex/releases/tag/app-v2.3.1)（UTC 2026-10-21，正式）。累计量不是今日增长，主线也不等于发行版。

## 定位

HEX 是以 Rust 实现的语音听写应用：按住快捷键说话、松开后本地转写并粘贴到当前应用。macOS 主路径面向 Apple silicon、macOS 15+；Windows 与 Linux 为 beta，能力不完全相同。 [README.md](https://github.com/anomalyco/hex/blob/50fb90715427859252492bcabc91aa5f0e607222/README.md)

## 用法

macOS 可从官方发行下载签名 DMG，或按 README 使用 Homebrew：

```sh
brew install --cask anomalyco/tap/hex
```

首次启动授予麦克风、输入监控和辅助功能权限，并下载本地语音模型。默认 Option 触发听写；先用非敏感短句核语言和粘贴焦点。Voice Action、云改写、持续语音命令需分别选择开启；不要从主线文档推定旧版具备所有功能。 [README.md](https://github.com/anomalyco/hex/blob/50fb90715427859252492bcabc91aa5f0e607222/README.md)

## 原理

本地语音模型完成听写，Modes 负责纠错、应用上下文规则和可选后处理，再经系统辅助功能粘贴。Voice Action / OpenCode 后处理是独立路径，可将指令、选中文本或转写及前台应用等上下文发送给配置的模型服务。 [README.md](https://github.com/anomalyco/hex/blob/50fb90715427859252492bcabc91aa5f0e607222/README.md)

## 价值

适合减少普通听写对云转写的依赖，并将语音输入接入现有编辑器。实际中文准确率、延迟、能耗和快捷键冲突需按设备 / 模型测量；本轮不引用作者跨平台时延数字作为复现结论。

## 风险边界

- 本地识别不覆盖可选云改写、模型下载与自动更新。Voice Action 和语音命令默认关闭；自定义 TypeScript 命令与依赖会以用户权限执行。 [README.md](https://github.com/anomalyco/hex/blob/50fb90715427859252492bcabc91aa5f0e607222/README.md)
- 听写音频默认不保存，但成功粘贴的原始 / 最终文字与有限应用元数据默认保留七天。关闭新历史记录不会删除旧条目，也不关闭诊断日志；日志可能含转写、应用名或 Brave URL，应分开核清理。 [README.md](https://github.com/anomalyco/hex/blob/50fb90715427859252492bcabc91aa5f0e607222/README.md)
- CLI 的 history / meetings 查询为已有本地数据的只读入口；不应把可读历史等同于所有录音流程都无存储。会议功能还需单独核录音授权和保留策略。 [docs/transcript-cli.md](https://github.com/anomalyco/hex/blob/50fb90715427859252492bcabc91aa5f0e607222/docs/transcript-cli.md)、[docs/features/meetings.md](https://github.com/anomalyco/hex/blob/50fb90715427859252492bcabc91aa5f0e607222/docs/features/meetings.md)
- 当前主线已修改 macOS 更新配置域，README 明确 2.3.1 及更早版本用旧域；不要把 main 的管理配置直接套到 app-v2.3.1。代码根许可 MIT，模型权重与第三方组件另核。 [README.md](https://github.com/anomalyco/hex/blob/50fb90715427859252492bcabc91aa5f0e607222/README.md)、[LICENSE](https://github.com/anomalyco/hex/blob/50fb90715427859252492bcabc91aa5f0e607222/LICENSE)

## 补充建议

固定 app tag、系统、语言与模型 revision，以授权语料测中文 CER、端到端粘贴延迟和误触发。分别测试断网听写、云处理失败、目标应用切换、历史关闭 / 删除与日志清理。本轮未安装应用、录音、授予权限或下载模型。

## 参考资料

- [README.md](https://github.com/anomalyco/hex/blob/50fb90715427859252492bcabc91aa5f0e607222/README.md)（固定 commit）。
- [docs/transcript-cli.md](https://github.com/anomalyco/hex/blob/50fb90715427859252492bcabc91aa5f0e607222/docs/transcript-cli.md)（固定 commit）。
- [docs/features/meetings.md](https://github.com/anomalyco/hex/blob/50fb90715427859252492bcabc91aa5f0e607222/docs/features/meetings.md)（固定 commit）。
- [LICENSE](https://github.com/anomalyco/hex/blob/50fb90715427859252492bcabc91aa5f0e607222/LICENSE)（固定 commit）。
- [发行列表](https://github.com/anomalyco/hex/releases)、[仓库 API](https://api.github.com/repos/anomalyco/hex)（动态状态）。
