<!-- markdownlint-disable MD013 -->

# langfuse：Agent 观测、Prompt 管理与评测平台

- 主上游：[langfuse/langfuse](https://github.com/langfuse/langfuse)；repository ID `642497346`。
- 采样日期：2026-10-25（Asia/Shanghai）；分类：模型、训练与推理基础设施。
- API 累计快照：36,370 stars / 4,068 forks / 1,128 open issues（含 PR 口径）；与榜单日增分开。
- 默认分支 `main`，本页静态依据固定在 `ad8d5641486176f9fef4e399bdd85a7b1ecf3842`。发行列表首项 `v4.70.0`，发布于 2026-10-24T12:54:58Z（正式）。
- 核验层级：直接读取上游文档、许可、元数据和下列部分实现；未安装运行、调用模型或复现性能。

## 定位

Langfuse 面向 LLM / Agent 应用的观测、调试、Prompt 版本管理、数据集与评测，支持云端和自托管。它记录模型调用及检索、工具等链路；不会仅因装上观测系统就保证 Agent 正确。本轮发行首项为 v4.70.0，UTC 2026-10-24 发布，不能将主线内容自动归于该发行。

## 用法

自托管先读固定版本 docker-compose.yml 和 README；本地演示入口为：

```bash
git clone https://github.com/langfuse/langfuse.git
cd langfuse
docker compose up
```

启动前替换 CHANGEME 凭据、SALT 和加密 key，检查端口与日志轮转。Compose 包含 web、worker、PostgreSQL、ClickHouse、Redis、MinIO 等组件，并非单容器。随后在测试项目创建凭据，按匹配版本 SDK 接入一段合成 trace；以上示例本轮未运行。

## 原理

应用用 SDK / 集成上报 trace 与 observation，将输入输出、延时、费用、工具链路与会话关联；Prompt、数据集及 experiment 把线上观察接到离线回归。Code evaluator、人工标注与 LLM 裁判提供不同评分来源。模型裁判自身有偏差和费用，因此评价结果必须保留评分定义、数据版本与模型配置。

## 价值

适合定位 Agent 哪一步检索或工具调用失败，并把失败样本加入可重复实验。统一 trace 和数据集有助于比较配置变更；收益仍需用实际故障定位时间、覆盖度、成本和延迟衡量，而不是用仪表盘数量代替效果。

## 风险边界

输入、输出和工具参数可能含个人信息、密钥或内部资料，接入前应脱敏、分项目授权并设置保留期。自托管默认有 PostHog 基础使用统计；README 给 OSS 的关闭方式为 TELEMETRY_ENABLED=false，当前实现的提前返回还要求没有 LANGFUSE_EE_LICENSE_KEY，不能把同一开关概括为所有 EE 场景均完全关闭。该路径不等于完整产品网络审计。根 LICENSE 对多数内容给 MIT，多个 ee 路径另受商业许可，GitHub API 的 NOASSERTION 也不能解释为无许可证。

## 补充建议

先用不含敏感信息的固定小数据集验证 trace 丢失、异步 flush、权限、脱敏、删除及恢复；比较人工与模型评分的一致性。部署应固定镜像摘要和 SDK 版本，监测数据库、对象存储、日志和评测模型费用，并分别核 OSS / EE 与遥测设置。

## 参考资料

- [README.md](https://github.com/langfuse/langfuse/blob/ad8d5641486176f9fef4e399bdd85a7b1ecf3842/README.md)。
- [docker-compose.yml](https://github.com/langfuse/langfuse/blob/ad8d5641486176f9fef4e399bdd85a7b1ecf3842/docker-compose.yml)。
- [web/src/features/telemetry/README.md](https://github.com/langfuse/langfuse/blob/ad8d5641486176f9fef4e399bdd85a7b1ecf3842/web/src/features/telemetry/README.md)。
- [web/src/features/telemetry/index.ts](https://github.com/langfuse/langfuse/blob/ad8d5641486176f9fef4e399bdd85a7b1ecf3842/web/src/features/telemetry/index.ts)。
- [LICENSE](https://github.com/langfuse/langfuse/blob/ad8d5641486176f9fef4e399bdd85a7b1ecf3842/LICENSE)。
- [ee/LICENSE](https://github.com/langfuse/langfuse/blob/ad8d5641486176f9fef4e399bdd85a7b1ecf3842/ee/LICENSE)。
- [仓库 API](https://api.github.com/repos/langfuse/langfuse)、[发行 API](https://api.github.com/repos/langfuse/langfuse/releases?per_page=3)；动态元数据只代表本轮采样。
- 事实来源为以上固定文件；价值、风险评估和验证建议为本库工程判断，未作为上游实测结果。
