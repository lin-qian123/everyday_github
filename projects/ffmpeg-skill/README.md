<!-- markdownlint-disable MD013 -->

# ffmpeg-skill：给 Coding Agent 一组可测量的视频工具

- 上游：[`kajisho5/ffmpeg-skill`](https://github.com/kajisho5/ffmpeg-skill)；仓库 ID：`1356077516`。
- 核读：2026-11-14（Asia/Shanghai）；主线固定于 [`b448ebc65903`](https://github.com/kajisho5/ffmpeg-skill/tree/b448ebc6590352f8599cb92ecaa0f95cae13f5f5)。
- 热度快照：5,408 stars / 467 forks / 29 open issues（含 PR）；来自 [GitHub API](https://api.github.com/repos/kajisho5/ffmpeg-skill)，不代表采用量或质量。

## 定位

为 Claude Code、Cursor、Codex 与 MCP 客户端提供的本地 FFmpeg 工具集，含 42 个编辑、分析、导出和检查工具。重点是“先探测，再编辑，最后验证”的执行契约，剪辑决策仍由人或上层 Agent 作出。Python daily +224；稳定 [v3.8.4](https://github.com/kajisho5/ffmpeg-skill/releases/tag/v3.8.4) 于 UTC 11-13 发布，[npm latest](https://registry.npmjs.org/ffmpeg-skill/latest) 同为 3.8.4。

## 用法

需要 Python 3.10+、FFmpeg 6.1+ 和实际使用的 encoder / filter；Node 16+ 仅供 npm 入口。以下安装会写宿主 skill 目录，先核目标；本轮未执行：

```bash
npx ffmpeg-skill@3.8.4 --codex
npx ffmpeg-skill@3.8.4 doctor
npx ffmpeg-skill@3.8.4 contract --json
```

先 `probe.py` 探测源片，`--dry-run` 看计划，再用 cut / fit / caption / render 等工具；输出后运行 check，画面变化再生成 look 接触表并实际查看。默认新建输出，覆盖需 `--overwrite`。

macOS 上游建议完整 FFmpeg 构建，并提醒 Homebrew `ffmpeg-full` 为 keg-only；应检查 doctor 返回的真实 binary 路径与能力。安装包名不保证子进程调用到所需构建。

## 原理

Python 脚本生成 argv 调用本机 FFmpeg / ffprobe，不接受调用者任意 filter graph。argparse 同时生成机器契约与 MCP schema，减少接口漂移；保存的计划带输入指纹，渲染时拒绝已变化输入。

MCP 使用 stdio JSON-RPC。默认 `tools/list` 只展示核心 12 个，`FFMPEG_SKILL_MCP_FULL=1` 展示全部 42 个；**两种模式都能按名称调用全部工具**，列表不是权限白名单。probe / check / cropdetect 标记只读，其他工具带 destructive 提示，宿主仍需执行权限控制。

## 价值

把格式、时长、声道、响度与失败写成结构化结果，适合可复查的素材流水线。输入指纹、执行计划和保留原片也便于区分计划错误与执行偏差。

## 风险边界

- `verified` 只覆盖实际测量属性，另有 `unverified` 和 visual-check 要求；技术 QA 不代表字幕语义、素材权利、全片音画或艺术效果已验收。
- 3.x 移除 FFmpeg 5.x / Python 3.9，并改变剪切 edit-list、HEVC、VFR 默认值；旧配方不能仅换版本号后假定结果一致。
- v3.8.4 修复部分音轨长度 / 延迟的采样精度；发行说明仍记录视频切入晚一帧、部分 speed-retime 早结束等未解决情形，测量基于 FFmpeg 6.1.1，不能外推所有后端。
- 源码拒绝 URL / 部分 playlist 媒体并使用显式 argv；这不构成 OS 沙箱，进程仍有宿主文件权限，应限定工作目录与可写输出。
- 引擎本地运行，但可选 ASR 可能首次下载权重，宿主 Agent 也有独立数据出口。“无 API key”不代表整个工作流断网。
- MIT 覆盖项目代码；FFmpeg 构建、codec、字体、模型和素材另有条件。

## 补充建议

用自制短片覆盖 VFR、透明度、HDR、字幕和精确音轨长度。固定版本、binary 与探测结果，保存原片、计划、输出和检查；完整观看、听评后再交付，平台模板还需检查实际 UI 安全区。

本页仅静态核读；未安装 skill / MCP、处理素材、跑上游测试或验收视频。

## 参考资料

- [入口与迁移](https://github.com/kajisho5/ffmpeg-skill/blob/b448ebc6590352f8599cb92ecaa0f95cae13f5f5/README.md)。
- [执行和验证契约](https://github.com/kajisho5/ffmpeg-skill/blob/b448ebc6590352f8599cb92ecaa0f95cae13f5f5/docs/contract.md)。
- [MCP 展示与调用](https://github.com/kajisho5/ffmpeg-skill/blob/b448ebc6590352f8599cb92ecaa0f95cae13f5f5/mcp/server.py)。
- [进程和本地媒体检查](https://github.com/kajisho5/ffmpeg-skill/blob/b448ebc6590352f8599cb92ecaa0f95cae13f5f5/scripts/_common/runner.py)。
- [安全报告](https://github.com/kajisho5/ffmpeg-skill/blob/b448ebc6590352f8599cb92ecaa0f95cae13f5f5/SECURITY.md)。
- [MIT 许可](https://github.com/kajisho5/ffmpeg-skill/blob/b448ebc6590352f8599cb92ecaa0f95cae13f5f5/LICENSE)。
