<!-- markdownlint-disable MD013 -->

# Generative AI for Beginners

> 更新：2026-10-20（Asia/Shanghai）。分类：AI 学习与教育资源。上游 `microsoft/generative-ai-for-beginners`；快照 `c35bc1950f9d`（main）。本文基于官方榜单、认证 API 与上游文件静态研究；热度、版本时间与跨平台证据见[当日日报](../../daily/2026-10-20/ai-hotspots.md)。

## 定位

Microsoft Cloud Advocates 的生成式 AI 入门课程，README 标为 Version 3、21 节课，另有 00 环境设置。用 Learn / Build 区分概念讲解与应用实践，尽可能提供 Python / TypeScript 示例，覆盖提示词、文本 / 聊天 / 搜索、RAG、agents、微调和小模型等。[README.md](https://github.com/microsoft/generative-ai-for-beginners/blob/c35bc1950f9dc56af773d2c362dafce6f76e9a56/README.md)

## 用法

从 `00-course-setup` 选择云开发或本地环境，再按主题进入一节课；有中文等多种翻译。仓库翻译较多，上游建议需要时用 sparse checkout 控制下载范围。为每个样例单独核对依赖、模型和 provider 设置，不要一次执行全库 notebook。[README.md](https://github.com/microsoft/generative-ai-for-beginners/blob/c35bc1950f9dc56af773d2c362dafce6f76e9a56/README.md)[00-course-setup/README.md](https://github.com/microsoft/generative-ai-for-beginners/blob/c35bc1950f9dc56af773d2c362dafce6f76e9a56/00-course-setup/README.md)

课程使用 OpenAI、Azure / Microsoft Foundry 等远端 endpoint，也给 Foundry Local / Ollama 路径；provider 指南描述各自环境变量。其当前文档提醒 GitHub Models 路径迁移到 Foundry，但沿用 `githubmodels` 文件名标签，因此不能据旧文件名认定仍使用旧服务。迁移时间属于课程文档声明，本轮未另查服务生命周期公告。[00-course-setup/03-providers.md](https://github.com/microsoft/generative-ai-for-beginners/blob/c35bc1950f9dc56af773d2c362dafce6f76e9a56/00-course-setup/03-providers.md)

## 原理

以文字、短视频、示例代码和延伸阅读构成课程单元，让学习者将模型 API、检索、工具调用和应用 UX 组合成最小项目。它提供教学 / 参考实现，不负责统一托管这些模型或保证所有 notebook 在同一依赖矩阵下运行。[README.md](https://github.com/microsoft/generative-ai-for-beginners/blob/c35bc1950f9dc56af773d2c362dafce6f76e9a56/README.md)

## 价值

适合作为有编程基础者的实践路线及授课素材索引，可逐步将“模型调用”扩展到检索、责任使用和应用生命周期。选型时可与只讲 prompts 的资料区分，但课程完整程度不能直接换算为就业或学习效果。

## 风险边界

- 课程免费阅读不等于实验免费；Codespaces、云模型、搜索 / 向量资源有独立额度和账单。使用本地编辑器也可能调用云 endpoint，“本地运行”与“离线推理”必须分别检查。[00-course-setup/README.md](https://github.com/microsoft/generative-ai-for-beginners/blob/c35bc1950f9dc56af773d2c362dafce6f76e9a56/00-course-setup/README.md)[00-course-setup/03-providers.md](https://github.com/microsoft/generative-ai-for-beginners/blob/c35bc1950f9dc56af773d2c362dafce6f76e9a56/00-course-setup/03-providers.md)
- `.env`、notebook 输出、分享截图和教学数据可能泄露 key 或输入；安全指南要求保护 secrets、控制日志与审查外部输入。示例不是生产安全验收报告。[docs/SECURITY_GUIDELINES.md](https://github.com/microsoft/generative-ai-for-beginners/blob/c35bc1950f9dc56af773d2c362dafce6f76e9a56/docs/SECURITY_GUIDELINES.md)
- SDK、deployment、API version、服务名称和翻译会漂移；以所固定 commit 的代码与依赖为起点，逐课验证，不把旧教学示例的模型名当作当前可用性保证。[00-course-setup/03-providers.md](https://github.com/microsoft/generative-ai-for-beginners/blob/c35bc1950f9dc56af773d2c362dafce6f76e9a56/00-course-setup/03-providers.md)
- MIT 覆盖仓库许可范围，引用视频、云服务、模型权重等仍有各自条款。API 未列 latest GitHub Release，不用课程 Version 3 冒充发行 tag。本轮未安装依赖、运行 notebook 或评估学习成效。[LICENSE](https://github.com/microsoft/generative-ai-for-beginners/blob/c35bc1950f9dc56af773d2c362dafce6f76e9a56/LICENSE)

## 补充建议

先完成一个低额度文本生成样例，记录 commit、解释器 / SDK、模型 deployment、输入输出和费用，再增加 RAG 的固定答案集及引用核对。教学时使用合成数据，保留失败示例与服务替代方案，并将译文与原文疑点记在同一份学习笔记中。

## 参考资料

- [README.md](https://github.com/microsoft/generative-ai-for-beginners/blob/c35bc1950f9dc56af773d2c362dafce6f76e9a56/README.md)
- [LICENSE](https://github.com/microsoft/generative-ai-for-beginners/blob/c35bc1950f9dc56af773d2c362dafce6f76e9a56/LICENSE)
- [00-course-setup/README.md](https://github.com/microsoft/generative-ai-for-beginners/blob/c35bc1950f9dc56af773d2c362dafce6f76e9a56/00-course-setup/README.md)
- [00-course-setup/03-providers.md](https://github.com/microsoft/generative-ai-for-beginners/blob/c35bc1950f9dc56af773d2c362dafce6f76e9a56/00-course-setup/03-providers.md)
- [docs/SECURITY_GUIDELINES.md](https://github.com/microsoft/generative-ai-for-beginners/blob/c35bc1950f9dc56af773d2c362dafce6f76e9a56/docs/SECURITY_GUIDELINES.md)
- [仓库 API](https://api.github.com/repos/microsoft/generative-ai-for-beginners)
