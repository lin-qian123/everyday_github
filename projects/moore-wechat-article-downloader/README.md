<!-- markdownlint-disable MD013 -->

# moore-wechat-article-downloader

## 定位

`Moore-developers/moore-wechat-article-downloader` 是一个本地优先的微信公众号内容研究助手。它把公众号文章、图片、精选评论和互动数据归档为本地资料库，供内容创作者、产品研究者和 Codex/Claude Code 做长期内容分析。

## 用法

README 提供 Codex 与 Claude Code 安装方式。典型工作流是在微信桌面客户端打开文章后，将当前正文、已加载评论和页面数据保存到本地，再输出 Markdown、CSV 和 SQLite 结构化资料。

## 原理

项目通过本地同步和导出，把分散在微信阅读场景中的文章、图片、评论和互动字段沉淀到本机文件与数据库中。它不是云端采集平台，而是面向个人和小团队的本地内容情报库。

## 价值

- 把中文内容研究里最常见但最难长期复用的公众号阅读转成结构化资产。
- Markdown、CSV、SQLite 都适合交给 agent 做选题拆解、标题分析、竞品研究和复盘。
- 本地优先降低了把内容和凭据交给第三方服务的风险。
- 对中文内容生产 skill 生态是有代表性的垂直工具。

## 风险边界

- 微信文章和评论数据涉及平台规则、版权和作者权益，使用时应遵守授权与合理使用边界。
- 页面实际可见数据受登录态、会话有效期和平台返回影响，不保证完整。
- 本地凭据、文章库和评论数据仍需加密、备份和访问控制。
- AI 分析只能辅助选题和复盘，不能替代事实核查和原创判断。

## 补充建议

- 用于竞品研究时保留原文链接、抓取时间和可见字段，避免把缺失数据误解为不存在。
- 对个人资料库设置同步边界，不要把包含评论和互动数据的 SQLite 直接上传公共仓库。
- 可与 `gzh-design-skill`、`speak-human-tw`、`kill-ai-slop` 形成中文内容生产链路。

## 参考资料

- GitHub: <https://github.com/Moore-developers/moore-wechat-article-downloader>
