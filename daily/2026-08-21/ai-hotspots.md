<!-- markdownlint-disable MD013 -->

# 2026-08-21 AI 热点日报

> 抓取时间：2026-08-21（Asia/Shanghai）。stars、forks、issue、许可证、创建/更新时间来自 GitHub REST API 快照，之后会变化；GitHub Trending 的“今日 stars”只代表短期公开关注，不能推导质量、安全性、生产成熟度或任何平台的社媒传播。X、Instagram、YouTube 本轮没有取得可独立核验的同项目原帖与互动量，故不填写互动量，也不拿 GitHub 指标替代社媒热度。

## 今日判断

- GitHub Trending 的 AI 相关信号分成两端：`obsidian-skills` 将 agent 的操作能力收敛到本地知识库的格式和 CLI 约定；`modly` 则把图像/提示词到 3D 的本地生成、工作流和 CLI 合并进桌面应用。二者都降低了“接入门槛”，但并未自动解决数据、供应链、权限或生成质量问题。
- 当日 Trending 同时出现的 `holaOS`、`LTX-2`、`Switchyard`、`agency-agents` 已在 `projects/` 有档案，未重复建目录。去重以当前 `projects/` 为准，避免把同一仓库反复上榜误报为每日新增。
- `obsidian-skills` 的 API 快照约 46.9k stars、3.4k forks、64 个开放 issue，许可证 MIT；`modly` 约 7.0k stars、671 forks、61 个开放 issue，但 API 返回 `NOASSERTION`，与 README 的 MIT 表述存在需独立核验的差异。

## GitHub 热点项目

| 项目 | 可核验信号 | 分类 | 评价 |
| --- | --- | --- | --- |
| [`obsidian-skills`](../../projects/obsidian-skills/README.md) | API 快照约 46.9k stars、3.4k forks、64 个开放 issue；创建于 2026-01-02；许可证 MIT。Trending 页面显示约 +292 当日 stars。 | Agent 框架与技能生态 | 将 Obsidian Markdown、Bases、JSON Canvas、CLI 与网页抽取规则组织为跨宿主 skills；需把 vault 权限、写入范围、provider 数据流与供应链单独管住。 |
| [`modly`](../../projects/modly/README.md) | API 快照约 7.0k stars、671 forks、61 个开放 issue；创建于 2026-03-17，2026-08-20 有上游推送；API 许可证为 `NOASSERTION`。Trending 页面显示约 +118 当日 stars。 | 语音、视频与多模态 | 本地 GPU 图像/提示词到 3D mesh 工作台，含工作流、扩展与 CLI；扩展执行、模型许可、输入权利及网格质量都必须独立验收。 |

候选来自 [GitHub Trending](https://github.com/trending?since=daily)、[`obsidian-skills` API](https://api.github.com/repos/kepano/obsidian-skills)、[`Modly` API](https://api.github.com/repos/lightningpixel/modly) 与各自的上游 README。数值只表示抓取时的公开元数据或短期关注，不能据此推导性能、协议安全、许可使用权或社媒热度。

## X、Instagram 与 YouTube 观察

| 平台 | 可追溯入口与状态 | 本轮可得信号 | 讨论与边界 |
| --- | --- | --- | --- |
| X | [`obsidian-skills` 搜索入口](https://x.com/search?q=%22obsidian-skills%22&src=typed_query)、[`Modly` 搜索入口](https://x.com/search?q=%22modly%22%20AI&src=typed_query)。未取得可独立核验的同日项目级原帖。 | 未核验项目级互动量。 | 搜索入口仅供观察，不把搜索结果、README badge 或 GitHub stars 当作 X 热传证据。 |
| Instagram | [AI 3D 标签入口](https://www.instagram.com/explore/tags/ai3d/)、[Obsidian 标签入口](https://www.instagram.com/explore/tags/obsidianmd/)。未取得可独立核验的同项目贴文。 | 未核验项目级互动量。 | 标签只代表主题观察入口，不能证明和上述仓库直接相关。 |
| YouTube | [`obsidian-skills` 搜索入口](https://www.youtube.com/results?search_query=obsidian-skills)、[`Modly` 搜索入口](https://www.youtube.com/results?search_query=Modly+AI+3D)。未逐条核验发布者、发布时间或观看量。 | 未核验项目级观看/互动指标。 | 搜索可能混入旧视频、第三方演示或同名内容；项目关联和数据必须逐条回到视频页核验。 |
| GitHub | [Trending](https://github.com/trending?since=daily) 与上列 REST API。 | Trending 分别显示约 +292、+118 当日 stars；API 可复核仓库元数据。 | 本轮唯一量化的项目级公开信号；不把 stars、forks 或提交时间等同于质量或社媒热度。 |

## 后续跟踪

- 在复制 vault 中比较启用前后的链接、properties、Canvas JSON 与 CLI 操作正确率，并保留可回滚的 Git 历史；不要直接让 agent 写生产笔记库。
- 用同一批有权使用的图像测量 `modly` 的拓扑、尺度、导出兼容性、GPU 占用和失败恢复；先审计每一个扩展的 `manifest.json`、脚本与模型许可。
- 若后续能直接打开 X、Instagram 或 YouTube 的相关原帖/视频，再补充发布时间、互动指标和项目关联依据；此前保持“未独立核验”。
