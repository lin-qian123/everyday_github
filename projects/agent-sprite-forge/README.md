<!-- markdownlint-disable MD013 -->

# agent-sprite-forge

- 上游：[0x0funky/agent-sprite-forge](https://github.com/0x0funky/agent-sprite-forge)；分类：语音、视频与多模态。
- 核读：2026-11-01（Asia/Shanghai）；固定主线 `5324342fdfab72430f4e9604f3fe427009f8596d`。
- [仓库 API](https://api.github.com/repos/0x0funky/agent-sprite-forge) 快照：4,763 stars / 473 forks / 14 open issues（含 PR）；发行首项 [v0.4.0](https://github.com/0x0funky/agent-sprite-forge/releases/tag/v0.4.0)，2026-10-06 UTC。发行与主线分别看。
- 证据：上游文档及指定文件静态核读；本轮未安装运行、调用模型或复现作者实验。

## 定位

面向 Claude Code、Codex 和 Grok 的游戏美术技能与 Python 工具链。v0.4 的主路线是“一张批准的角色原画 → 每个动作一段图生视频 → 可交付动画包”，另有程序绘图和地图工具。它组织生成与加工流程，不是自带图像 / 视频模型。官方 Python daily 榜本轮显示 +51 stars。

## 用法

按固定 README 的 Codex 路线，在独立目录安装：

```bash
git clone https://github.com/0x0funky/agent-sprite-forge.git
cd agent-sprite-forge
git checkout 5324342fdfab72430f4e9604f3fe427009f8596d
python -m pip install -r requirements.txt
python tools/install_skills.py --apply --host codex
```

`--apply` 会写技能目录并备份已有副本；`--check --host codex` 可查漂移。视频处理还需 ffmpeg 5.1+，重新开启 Agent 会话后加载技能。先用 `generate2dsprite` 生成 / 审阅 master，再用 `video2dsprite` 规划动作、逐动作审片和导出。

开始付费生成前，可用 `skills/generate2dmedia/scripts/route_media.py resolve --kind image` 查看路线；真实生成命令带 `--dry-run` 只输出计划。显式设置 `--budget-usd` / `--max-calls`，并记录 reference 图的来源与使用权。

## 原理

`route_media.py` 默认按已配置 API → 本机已登录 CLI → 无可用路线时程序绘图的顺序选择。之后做抠像、对位、循环选择、单次动作重计时、HD / 像素后处理和封包；共享 master、尺寸与色彩约束减轻跨动作漂移。状态文件帮助续跑，`.forge/ledger.jsonl` 记录调用与估价。

数值 QC 负责轮廓、缩放、边缘、动作等门槛，人工审查负责武器变化、遮脸与语义错误。输出含 atlas / animation.json，以及 Godot、Aseprite 等格式；“文件能解析”和“目标编辑器中可正确使用”是两项验收。

## 价值

把随机生成素材的后处理拆成可重放步骤，并保留选片、路线和成本线索。适合小型游戏原型及已有授权角色素材的动作扩展；工程收益应以返工次数、人工修图时间和实际引擎回读评估。

## 风险边界

- 配置 API key 会被上游视为可直接发请求的授权，默认没有预算上限；“本机 CLI”也可能调用云模型并消耗订阅额度。源码中的此行为不代表本轮已授权或执行调用。
- 作者 10 月 6 日验证记录包含 CLI 实跑，但明确没有 live API provider 调用；API adapter 的 mock 测试不能证明供应商端行为已验证。
- QC 在同次运行的 42 个已标注 takes 上调整，不能据此声称泛化零误拒。记录还披露颜色漂移、动作慢放、手动挑帧及部分旧片复用。
- 作者说明 Godot / LDtk / Aseprite / Tiled 导入仍未实测。MIT 代码许可不自动覆盖生成平台条款、输入角色或第三方素材。

## 补充建议

先做一个授权角色、两个动作的小包：保存原始片、逐帧审查和预算账本，导入实际引擎后检查 alpha、脚底滑动、碰撞、命中时刻及循环接缝。分别验 mock、CLI 和 API 路线；无法生成的动作保留失败记录，不用 QC 通过替代美术验收。

## 参考资料

- [固定 README / 安装与导出](https://github.com/0x0funky/agent-sprite-forge/blob/5324342fdfab72430f4e9604f3fe427009f8596d/README.md)。
- [媒体路线、授权与预算逻辑](https://github.com/0x0funky/agent-sprite-forge/blob/5324342fdfab72430f4e9604f3fe427009f8596d/skills/generate2dmedia/scripts/route_media.py)。
- [作者验证记录及未闭环项](https://github.com/0x0funky/agent-sprite-forge/blob/5324342fdfab72430f4e9604f3fe427009f8596d/docs/validation-2026-10-06.md)。
- [MIT 许可](https://github.com/0x0funky/agent-sprite-forge/blob/5324342fdfab72430f4e9604f3fe427009f8596d/LICENSE)。
