<!-- markdownlint-disable MD013 -->

# generative-media-skills

## 定位

`calesthio/generative-media-skills` 是一套面向 AI agent 的生成媒体生产技能库，覆盖图像、视频、音频、语音、音乐、3D、avatar、互动媒体等 25 个类别。它不是单一模型封装，而是把供应商选择、创意导演、制作工艺、QA、权利和交付规范写成可加载 skill。

## 用法

README 建议在 agent 中直接请求加载对应技能：

```text
Use generative-media-skills.
Load the necessary skills required for the below task.
Create a 15-second premium product launch clip.
```

项目声称可用于 Claude Code、Codex、GitHub Copilot、Cursor 以及任何能加载 Agent Skills 的 runtime，也可与 OpenMontage 组合使用。

## 原理

仓库将媒体生产链拆成可组合技能：选择系统、导演执行、构建交付物、运行确定性检查、保留 provenance 和 rights evidence。部分 skill 带脚本、参考材料和 `EVAL.md`，让 agent 在需要时加载细分知识，而不是一次性把所有上下文塞入模型。

## 价值

- 把生成媒体从“写 prompt”推进到制作流程和交付 QA。
- 对品牌短片、产品图、播客、avatar、房地产媒体、社交短视频等场景有实用入口。
- Provider-independent 结构能降低模型快速变化带来的维护成本。
- 对中文仓库中已有 `video-production-skills`、`FableCut`、`hyperframes` 是互补路线。

## 风险边界

- 媒体生成供应商、价格、限制和模型能力高度易变，skill 中的 provider 信息需要持续校验。
- 权利、肖像、声音克隆、训练数据和平台政策风险不能只靠 agent 判断。
- 技能数量多不等于可交付质量稳定，仍需人类创意和法务审核。
- 生成内容可能有水印、版权、误导性或品牌一致性问题。

## 补充建议

- 生产使用时把 rights / consent / provenance 作为强制验收项。
- 对每个供应商技能记录最后验证日期和官方文档链接。
- 将 deterministic QA 脚本优先用于字幕、时长、分辨率、loudness、manifest 和交付格式。

## 参考资料

- GitHub: <https://github.com/calesthio/generative-media-skills>
- OpenMontage: <https://github.com/calesthio/OpenMontage>
