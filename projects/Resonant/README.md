# Resonant

## 定位

Resonant 是 Windows 本地优先的音乐工作站，覆盖编曲、混音、采样器、录音、WAV 导出，并可选接入本地 ACE-Step 生成音乐与 Codex/Claude MCP 工作流。截至 2026-08-03 的 GitHub API 快照：项目创建于 2026-08-02，约 16 stars、3 forks，AGPL-3.0。

## 用法

可从 Releases 下载 Windows x64 安装器或便携包；README 明确指出当前构建未签名，应先核验文件名和发布的 SHA-256。也可在 Windows 上使用 Node.js 22+ 从源码执行 `npm ci`、`npm run check`、`npm run build`、`npm run dev`。本地 AI 生成需另行下载模型，推荐 NVIDIA GPU 约 6--8 GB 显存。

## 原理

桌面工作站将 Flow、Arrange、Mix 三类创作界面与内容寻址的音频库结合；可选 ACE-Step 在本机生成音频。其 agent 模式受限于项目声明的 MCP 契约：语言模型接收结构化的创作/操作信息，而非直接返回音频负载。

## 价值

- 把从生成、编曲到导出的音乐流程放在本机，减少把录音和歌词交给托管服务的依赖。
- 对 AI 生成、真实乐器和导入素材保留同一编辑与混音工作台。

## 风险边界

- 当前仅发布 Windows 构建且未签名；安装与更新需独立验证来源和校验和。
- “本地生成”不自动取得模型、音色库、样本、歌词或人声的版权；项目 README 也不保证输出唯一、无侵权或可受版权保护。
- AGPL-3.0 对修改后网络服务的发布有义务，商用集成前应审阅许可证。

## 补充建议

先用无版权争议的测试素材验证录音、导出、恢复和模型下载磁盘占用；生产创作建立素材来源、模型版本、提示词和人工验听记录，尤其避免仿冒特定真人声线。

## 参考资料

- GitHub：<https://github.com/calesthio/Resonant>
- Releases：<https://github.com/calesthio/Resonant/releases>
- GitHub API 快照：<https://api.github.com/repos/calesthio/Resonant>
