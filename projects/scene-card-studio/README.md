<!-- markdownlint-disable MD013 -->

# Scene Card Studio

- 仓库：[swping999/scene-card-studio](https://github.com/swping999/scene-card-studio)
- 快照：2026-08-10 抓取；GitHub API 显示其创建于 2026-08-09，约 20 stars、0 forks，Apache-2.0。数字会随时间变化。
- 分类：语音、视频与多模态

## 定位

将个人照片转成可编辑“Scene Card”、版本化生成提示和可审阅图像叙事的视觉导演管线。它强调不是单纯滤镜：先记录可观察证据，再分离解释、导演意图、叙事系统与图像生成结果。

## 用法

README 的 quick start 是 Python 环境中执行 `python -m pip install -e '.[images]'`。项目提供旅行、家庭档案、电影分镜和极简编辑等示例，以及 `story.json`、prompt/render manifest、审阅和 retry 记录；实际接入照片或图像 provider 前需先检查相关配置、访问令牌和输出目录。

## 原理

管线依次执行“照片 → Scene Cards → Narrative System → Prompt Compiler → 生成 → 审美复核 → 重试/接受”。Scene Card 将可见 observation 与带置信度的 interpretation 分开；编译器生成带保留、可变换、必须移除、尺寸和 MIME 等约束的 JSON contract，输出绑定与 review 再检查格式、尺寸和重试来源链。

## 价值

对希望保留照片证据、编辑决策和生成 provenance 的创作者或团队，它比一次性 prompt 更便于修改、复查和交接。结构化 contract 也有助于把“审美意见”变成可定位的输出约束和验收记录。

## 风险边界

“观察/解释分离”不能保证模型不误读人物、关系或情绪；生成图仍可能损害肖像真实性、版权和当事人同意。上传私人照片到任何云端 provider 前，必须单独确认数据保留、训练使用和跨境传输；20 stars 不代表作品质量、隐私或版权风险已被审计。

## 补充建议

从作者明确授权的低敏感样本开始，人工逐卡确认人物、地点和叙事推断。将原图、prompt、生成物和 consent 记录分级保存；对外发布时标示 AI 合成，并保留可撤回/删除流程，避免把推断性叙事当作照片事实。

## 参考资料

- [项目 README 与示例](https://github.com/swping999/scene-card-studio)
- [设计原则](https://github.com/swping999/scene-card-studio/blob/main/DESIGN_PRINCIPLES.md)
- [GitHub API 元数据快照](https://api.github.com/repos/swping999/scene-card-studio)
