<!-- markdownlint-disable MD013 -->

# Mesh Avatar Studio（shinshin86/mesh-avatar-studio）

> 上游仓库：<https://github.com/shinshin86/mesh-avatar-studio> · 归类：语音、视频与多模态 · 本页基于 2026-10-05 的 GitHub API、README、agent guide、reference、rig schema、manifest 与 LICENSE / sample terms 静态整理，未上传或处理人物图、调用图像生成、运行编辑器 / Playwright 或检查动画质量与素材权利。

- 抓取快照：123 stars、11 forks、0 open issues；仓库创建于 2026-10-04 03:33 UTC。
- 热度信号：GitHub Search 按新建仓库 stars 排序的早期开发者信号；不是 GitHub Trending 或社媒互动量。
- 版本与许可：代码 MIT；无 GitHub Release / tag，private npm manifest `0.1.0`；bundled Miko 角色不在 MIT 内，另受角色使用条款约束。

## 定位

Mesh Avatar Studio 把一张正面半身插画转成可眨眼、说话、转头、呼吸和摆动头发的 2D mesh avatar。coding agent 负责读坐标、创建 rig、切层和渲染固定姿势检查，用户再在本地 React 编辑器中拖动控制点和实时预览。

## 用法

Node 22.17+ 下运行 `npm install && npm run dev` 可先打开只读 sample。制作自有角色时，在仓库中让 Claude Code 或 Codex 按 `docs/agent-guide.md` 处理本地图像，生成 `projects/<name>/`；用户在 editor 中做 pose / lip-sync 检查并拖动修正，必要时再让 Codex 通过内置 image generation 绘制闭眼和元音嘴形变体。

## 原理

agent 先通过 vision check 验证坐标读取能力，再从 zoomed grid 标出头、眼、嘴、头发、手和附件区域，生成 schema v1 的 `rig.json`。Python / Node 工具把源图切成 mesh、mask 和 sprite layer，runtime 对控制区做形变；固定 pose renderer 与 overlay 用于视觉回归，编辑器修改影响切层的字段后会显式要求 rebuild。

## 价值

它把通常依赖专业 rigging 软件的过程拆成“Agent 初稿 + 本地可视化人工校准 + 固定姿势检查”，并公开坐标、layer、schema 与失败准则。项目素材默认留在 gitignored 本地目录，也让用户能在生成图像之前先用纯 mesh 方案评估可行性。

## 风险边界

- 自动坐标和切层高度依赖模型视觉能力、原图姿态、遮挡与透明背景；agent guide 要求 vision check、zoomed grid 和最多三轮 review，仍不能保证自然动画。
- 闭眼 / 嘴形变体会把 `source.png` 与 mask 发送到图像生成服务，必须先获人物 / 委托方授权并确认 provider 的训练、保留和地区政策。
- 代码 MIT 不覆盖输入插画、生成变体、字体或 bundled Miko；Miko 不能作为独立素材包再分发，用户自己的肖像 / 角色权利需另行确认。
- 项目创建不足一天且无 Release / tag；123 stars 只是早期关注，不能证明编辑器稳定、格式长期兼容或导出链成熟。
- 单张图 mesh 无法恢复被头发遮挡的眼、背面、真实深度或复杂附件；生成补图也可能改变身份、服饰和未遮罩区域。
- 本轮未运行 build / e2e、检查 pose 帧、测试长会话 lip sync、导出格式、性能或本地目录泄露。

## 补充建议

只使用自己拥有或获明确授权的 PNG，固定 commit `98b14c2e352c` 并保留原图哈希；先不启用生成变体，逐帧检查 ±30° 转头、闭眼、嘴形、手和头发是否撕裂。若需 image generation，先记录上传同意、provider 和 mask，再用像素差确认遮罩外未变化；交付时把代码许可、角色 / 源图许可和生成制品记录分开。

## 参考资料

- [GitHub 仓库](https://github.com/shinshin86/mesh-avatar-studio)
- [GitHub REST API](https://api.github.com/repos/shinshin86/mesh-avatar-studio)
- [README 与本地工作流](https://github.com/shinshin86/mesh-avatar-studio/blob/main/README.md)
- [Agent guide](https://github.com/shinshin86/mesh-avatar-studio/blob/main/docs/agent-guide.md)
- [Editor / build reference](https://github.com/shinshin86/mesh-avatar-studio/blob/main/docs/reference.md)
- [Rig schema](https://github.com/shinshin86/mesh-avatar-studio/blob/main/docs/rig-fields.md)
- [npm manifest](https://github.com/shinshin86/mesh-avatar-studio/blob/main/package.json)
- [Miko sample terms](https://github.com/shinshin86/mesh-avatar-studio/blob/main/samples/miko-qipao/MIKO_ASSET_TERMS.md)
- [LICENSE](https://github.com/shinshin86/mesh-avatar-studio/blob/main/LICENSE)
