<!-- markdownlint-disable MD013 -->

# oh-my-ai-company

## 定位

`yan5xu/oh-my-ai-company` 是一个持续更新的 AI 公司研究库，覆盖 AI 产品、AI infra、企业 Agent、垂直 AI 公司、创始人、投资机构、融资事件、流量信号和研究笔记。它更像一个 AI company market map，而不是普通收藏夹。

## 用法

可以直接访问在线站点：

```text
https://companies.yan5xu.ai
```

也可以在仓库中查看 `bodies/` 目录下的 company、source、note、traffic、method 等 Markdown 对象，或使用其底层 local-first 知识库产品 Memex 查询结构化关系。

## 原理

底层使用 Memex：SQLite 存 schema、object、link，Markdown 存正文。公开站点通过 manifest 将公开 vault 发布到 Cloudflare D1/R2。设计上将事实证据、结构化关系、增长信号、研究判断和方法沉淀分开，避免把 PR 口径、社区情绪和个人结论混在一起。

## 价值

- 对 AI 公司和产品变化做长期、可追溯、可扩展的对象网络记录。
- 适合研究投资、创业、竞品分析、GTM 和 AI 产品地图。
- 比单篇调研报告更利于持续更新和复用。
- 展示了 local-first 知识库 + 公开站点发布的研究工作流。

## 风险边界

- 公司、融资、流量和社区信号变化快，快照容易过期。
- 研究判断来自维护者，需要和原始来源区分阅读。
- Similarweb、社交平台和媒体信号不一定能代表真实收入或留存。
- 若复用 vault 结构，需要注意敏感信息过滤和发布清单审计。

## 补充建议

- 使用时先看 source 对象，再看 note 判断。
- 对投研结论要求至少两个独立来源交叉验证。
- 可将其作为每日 AI 热点的公司背景索引，而不是单次新闻依据。

## 参考资料

- GitHub: <https://github.com/yan5xu/oh-my-ai-company>
- Online atlas: <https://companies.yan5xu.ai>
- Memex: <https://github.com/yan5xu/memex>
