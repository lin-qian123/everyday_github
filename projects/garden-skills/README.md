<!-- markdownlint-disable MD013 -->

# Garden Skills

> 上游仓库：[ConardLi/garden-skills](https://github.com/ConardLi/garden-skills) · 归类：Agent 框架与技能生态 · 本页基于 2026-08-27 的上游 README、目录说明与 GitHub API 快照整理。

## 定位

Garden Skills 是面向 Claude Code、Cursor、Codex 和其他 coding agent 的技能集合，将网页/视频演示、前端设计、图像生成、知识检索和文章生成等工作流封装为可加载的 `SKILL.md` 与配套资源。API 快照为 10,898 stars、1,387 forks、16 个开放 issue，MIT；代码最近一次推送快照为 2026-07-12，Trending 页面抓取时显示约 +537 当日 stars。项目热度和技能安装数只能说明公开关注度，不能证明所有 skill 质量、兼容性或安全性一致。

## 用法

上游优先推荐用 `skills` CLI 按需安装全部集合或单个 skill：

```sh
# 安装全部技能
npx skills add ConardLi/garden-skills

# 只安装某个技能到当前项目
npx skills add ConardLi/garden-skills -s web-design-engineer

# 安装到全局 skills 目录
npx skills add ConardLi/garden-skills -s gpt-image-2 --global
```

当前 README 展示的主要入口包括 `web-video-presentation`、`web-design-engineer`、`gpt-image-2`、`beautiful-article`，以及与检索相关的 `kb-retriever`。实际使用前应只复制需要的目录，并逐个阅读其 `SKILL.md`、脚本和外部资源说明。

## 原理

- 每个 skill 以自然语言规则、工作流步骤、模板和质量检查组成，agent 在匹配任务时读取对应目录并据此生成内容或调用工具。
- 部分 skill 将输出约束为 HTML、Markdown、图像提示或文章结构；`dist/`、演示页面和相关脚本为这些约束提供示例或打包入口。
- 它更像“可移植的工作方法层”，不是统一 runtime：模型、工具调用、文件写入、网络访问和宿主权限仍由 Claude Code、Cursor、Codex 等执行环境决定。
- 集合化仓库通过 `skills` CLI、Claude plugin 或手工复制分发内容，但不同宿主对目录发现、命令权限和资源加载的行为可能不同。

## 价值

- 把前端审美、检索步骤、图像提示和文章结构等重复经验沉淀为可复用的 agent 上下文，减少每次从零写 prompt。
- 纯文本 skill 易于 Git 管理、审阅、分叉和迁移，便于在团队内形成项目级方法规范。
- 按需安装可以把通用 coding agent 变成特定领域工作台，例如网页设计、知识库检索或图文内容制作。
- 集合中的示例和模板可作为比较不同 agent 输出质量的起点，但需要结合自己的验收规则。

## 风险边界

- skill 不是沙箱、权限系统或事实核验器；其中的命令、脚本和网络调用会继承宿主 agent 的真实权限。
- “production-ready”是上游定位，不是对每个 skill 在所有模型、宿主、输入和地区环境中的独立验证结果。
- 图像、文章和网页生成可能涉及版权、品牌、个人资料和第三方素材；技能模板不会自动授予训练、发布或商用许可。
- 检索类 skill 可能把本地文档、URL 或搜索结果送入模型；安装前应审计 provider、外部 endpoint、日志和缓存的数据流。
- 多个 skill 同时加载会产生命名冲突、规则遮蔽、重复调用和上下文膨胀；安装数量不等于 agent 能力线性增加。

## 补充建议

1. 采用锁定版本或 release ZIP，先在临时宿主和合成资料上验证每个 skill 的入口、依赖、写入路径和网络请求。
2. 将“能生成”与“可交付”分开：为网页做无障碍/性能检查，为检索做来源回链，为图像做素材权利与人物同意检查。
3. 对会调用 shell、浏览器、图像 API 或本地文件的 skill 设置最小权限和人工批准；不要把集合目录整体加入长期 allowlist。
4. 团队使用时维护一份启用清单、版本锁、变更审阅记录和敏感数据禁用规则，避免上游更新静默改变工作流。

## 参考资料

- [上游 README / 技能目录与安装方式](https://github.com/ConardLi/garden-skills)
- [上游中文 README](https://github.com/ConardLi/garden-skills/blob/main/README.zh-CN.md)
- [Skills CLI 项目页](https://www.skills.sh/conardli/garden-skills)
- [GitHub API 元数据](https://api.github.com/repos/ConardLi/garden-skills)
- [GitHub Trending](https://github.com/trending)
