# slopsource

## 定位

`slopsource` 是一个持续发布可自托管 AI 应用替代实现的单仓库计划，主张每个子目录用自带模型或 API key 运行，不创建集中式账户。截至 2026-08-01 的 GitHub API 快照，它创建于 2026-07-31，约 1 star、0 forks，API 许可证字段为 `NOASSERTION`；仅是早期项目观察项。

## 用法

克隆仓库后进入具体 drop（例如 `unlovable/`），按其 README 配置 `LLM_BASE_URL`、`LLM_MODEL`、`LLM_API_KEY`，再运行 `docker compose up`。先检查每个子目录自己的依赖、端口、数据卷与许可证，避免将根目录的统一配置误当成安全默认值。

## 原理

项目把若干面向生成、日历、演示和库存等任务的替代实现置于同一仓库，复用 OpenAI-compatible 或本地模型配置。它强调 BYOK 与自托管，仍可能依赖托管模型服务及其配额。

## 价值

- 便于研究 AI 包装应用的最小可运行构成、定价叙事与可迁移实现。
- 统一配置降低试验多个子应用时的启动摩擦，并支持本地模型路线。

## 风险边界

- “替代某产品”“节省订阅费”是项目主张，功能完整度、准确性、安全性和总拥有成本未获独立验证。
- 自托管不自动等于私密：若填入第三方 API key，提示和数据仍会离开本机。
- `NOASSERTION` 许可证状态必须逐目录人工确认；不要将仓库宣传徽章当作法律授权。

## 补充建议

对每个 drop 分别做依赖与容器扫描、端口暴露检查、成本测算和数据流审计。将 `.env` 放在受限权限目录，使用测试密钥，并优先在无敏感数据的环境评估。

## 参考资料

- GitHub：<https://github.com/micahc123/slopsource>
- GitHub API 快照：<https://api.github.com/repos/micahc123/slopsource>
