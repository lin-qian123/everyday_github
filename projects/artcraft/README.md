<!-- markdownlint-disable MD013 -->

# ArtCraft（storytold/artcraft）

> 上游仓库：<https://github.com/storytold/artcraft> · 归类：语音、视频与多模态 · 本页基于 2026-10-07 的 GitHub API、README、Rust workspace、Roadmap 与 LICENSE 静态整理，未登录任何 provider、上传素材、生成媒体或验证模型目录与费用。

- 抓取快照：3,167 stars、332 forks、44 open issues。
- 热度信号：GitHub Rust Trending 抓取时约 +300 当日 stars；最后 push 为 2026-10-05。
- 版本与许可：latest Release 为 `artcraft-v0.41.0`；API `NOASSERTION`，根 `LICENSE.md` 是仍标注 WIP 的自定义 fair-source 条款，不是 OSI 许可证；本页固定审计 commit `3210977fb114`。

## 定位

ArtCraft 是面向艺术家、设计师与影视创作者的 AI 图像 / 视频桌面 IDE：把 prompt、2D canvas、3D scene blocking、角色姿态、camera、inpainting、图生视频和多 provider 模型放进一个可视化工作区。它强调在生成前精确构图，而非只做模型聚合网站。

## 用法

普通用户可从 `artcraft-v0.41.0` Release / 官网取得桌面应用；开发者按 `_docs/dev_setup.md` 配置 Rust、Node 与 Tauri，再用统一 launcher 启动前端和原生应用。正式素材前先使用自有或明确授权的测试图，逐一核对登录方式、provider 条款、价格、上传数据、输出许可与删除机制，并保存 prompt、模型、参数和输入 provenance。

## 原理

Rust / Tauri 桌面端结合 React 前端、本地 SQLite task 数据与多组 API client；用户先在 2D / 3D 场景中安排背景、前景、角色、mesh、camera 与 mask，再调用 ArtCraft、Grok、Midjourney、Sora / GPT Image、World Labs 等 provider 生成或编辑图像、视频、音频、mesh 与 world。Roadmap 仍把“移除对 ArtCraft hosted services 的依赖”列为目标。

## 价值

可编辑构图、姿态、镜头和 scene reuse 能把一次性 prompt 变成可重复的创作过程，也更便于对同一输入比较模型。公开 monorepo、桌面 task 数据和多 provider 适配器为研究 AI 创作工作站提供了比单一网页生成器更完整的工程样本。

## 风险边界

- 根许可明确标注 WIP，并限制商业销售、竞争产品、移除社区 / 捐赠 / 付费模型链接和品牌使用；不能把源码可见或免费使用写成 OSI 开源、可自由商用或可再分发。
- LICENSE 称生成资产归用户，不会自动覆盖 provider 条款、训练数据争议、第三方素材、字体、商标、角色、肖像、声音、隐私或各地著作权规则。
- 选择远端 provider 时，prompt、参考图、视频、身份素材、Cookie / token 与费用会进入外部服务；“桌面应用”不等于本地生成或无网络。
- workspace 含 consumer / browser-emulation / cookie client；真实账号接入需审计登录方式、会话存储、自动化许可和账号封禁风险。
- 62-model 等目录、画质和 provider 支持来自上游 README，本轮未逐模型调用；模型可用性、版本、价格、审核与输出稳定性会变化。
- Roadmap 仍计划移除 hosted-service 依赖，离线连续性和“业务结束仍可运行”的承诺尚不能当成已验证技术事实。

## 补充建议

建立素材权利登记和 provider 数据流表，以专用测试账号、低额度和去身份素材先跑；每次生成记录输入哈希、模型 / provider / 版本、参数、费用、人工修改与授权。商业采用前让法务审查 WIP 许可和每个 provider，制作环节增加人物同意、相似性、品牌、字幕 / 字体、音频和最终观看 QA。

## 参考资料

- [GitHub 仓库](https://github.com/storytold/artcraft)
- [GitHub REST API](https://api.github.com/repos/storytold/artcraft)
- [README 与功能目录](https://github.com/storytold/artcraft/blob/main/README.md)
- [artcraft-v0.41.0 Release](https://github.com/storytold/artcraft/releases/tag/artcraft-v0.41.0)
- [Rust workspace 与 provider clients](https://github.com/storytold/artcraft/blob/main/Cargo.toml)
- [开发环境](https://github.com/storytold/artcraft/blob/main/_docs/dev_setup.md)
- [2026 Roadmap](https://github.com/storytold/artcraft/blob/main/ROADMAP.md)
- [WIP ArtCraft License](https://github.com/storytold/artcraft/blob/main/LICENSE.md)
- [上游固定演示视频](https://www.youtube.com/watch?v=kzvQMdg66Go)
