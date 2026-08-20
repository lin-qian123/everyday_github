<!-- markdownlint-disable MD013 -->

# Modly

> 上游仓库：[lightningpixel/modly](https://github.com/lightningpixel/modly) · 归类：语音、视频与多模态 · 本页基于 2026-08-21 的上游 README 与 GitHub API 快照整理。

## 定位

`Modly` 是面向 Windows、Linux 与 Apple Silicon macOS 的本地桌面应用：以开源模型在本机 GPU 上将图像或提示词生成 3D mesh，并提供场景、工作流、网格平滑/减面、扩展与自动化 CLI。它是本地生成工作台，不等同于模型本身，也不保证输入图片的权利、生成几何的正确性或商业可用性。

API 快照：约 7.0k stars、671 forks、61 个开放 issue；创建于 2026-03-17，2026-08-20 有上游推送。API 许可证字段为 `NOASSERTION`，但上游 README 声称 MIT；使用或二次分发前必须以仓库实际 `LICENSE` 和发行物条款为准。Trending 页面展示约 +118 stars，仅作短期关注信号。

## 用法

普通使用可从上游 Releases 获取安装包；开发模式的官方步骤如下：

```sh
npm install
cd api
python -m venv .venv
source .venv/bin/activate  # Windows 改用 .venv\\Scripts\\activate
pip install -r requirements.txt
cd ..
npm run dev
```

最小工作流可先连接“Image → Generate Mesh → Add to Scene”，在 Generate 页面选择该工作流并运行。其 CLI 可在桌面应用运行时调用：

```sh
python tools/modly-cli/agent.py health
python tools/modly-cli/agent.py model list
python tools/modly-cli/agent.py generate --image ./input.png --output ./export.glb
```

README 明确区分 canonical CLI 与实验性 ComfyUI helper；自动化应优先用已文档化的 `health`、`model`、`workflow-run`、`capability`、`process-run`，并在真实桌面 bridge 可用时再宣称可用。

## 原理

应用前端管理场景与工作流，Python API 后端运行本地模型；模型能力通过带 `manifest.json` 的 GitHub 扩展接入。上游列出的官方扩展覆盖 Hunyuan3D 2 Mini、TripoSG 与 Trellis2 GGUF。生成后可在应用内平滑或减面，再把优化 mesh 写回工作区；CLI 则以 JSON 将生成任务、状态和恢复信息暴露给脚本或 agent。

## 价值

- 将图像到 3D、工作流编辑、网格后处理和自动化接口收在本机工作台，适合原型、资产草稿和可重复 batch 流程。
- 本地 GPU 推理可减少把素材上传到第三方服务的需要，但不自动消除模型下载、扩展网络访问或日志泄露。
- CLI 的结构化输出有助于把生成步骤纳入 agent 或 CI 的可审查流水线。

## 风险边界

- 安装扩展会从 GitHub 拉取并执行其运行时；它不是受信任的模型商店，需审计仓库、锁定 revision、扫描依赖和最小化网络权限。
- 3D 生成可能产生破面、尺度/拓扑错误或与参考图不一致的资产；必须在目标引擎、打印或渲染管线中人工验收。
- 输入图像、人物肖像、商标和训练/扩展模型都可能带来版权、肖像权、许可和使用范围约束。
- 本地运行仍消耗显存、磁盘、电力与下载带宽；README 对 macOS 的支持仅指向 Apple Silicon，其他平台须实测。

## 补充建议

1. 先用无敏感、明确有权使用的图片建立质量基线：网格闭合、法线、UV、面数、尺度和任务耗时。
2. 将模型、扩展、工作流 JSON 与输出资产一并版本化；把运行时版本、GPU、参数和 seed 写入交付记录。
3. 在隔离环境先验证 `health`、模型下载、生成、取消和导出失败恢复；不要把实验性 ComfyUI helper 当成稳定生产接口。
4. 发布/二次开发前核对仓库实际许可证、扩展许可证和上游 README 所称的署名要求。

## 参考资料

- [上游 README](https://github.com/lightningpixel/modly)
- [GitHub API 元数据](https://api.github.com/repos/lightningpixel/modly)
- [Modly Releases](https://github.com/lightningpixel/modly/releases)
- [Modly 官方扩展示例](https://github.com/lightningpixel/modly-hunyuan3d-mini-extension)
