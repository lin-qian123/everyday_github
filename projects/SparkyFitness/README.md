<!-- markdownlint-disable MD013 MD034 -->

# SparkyFitness：自托管家庭健康记录与可选 AI 助手

> 上游仓库：https://github.com/CodeWithCJ/SparkyFitness · 归类：办公、商业与行业应用 · 本页基于 2026-09-16 的 README、release、LICENSE、文档与 GitHub REST API 静态整理；项目明确是非商业 source-available，不应写成 OSI 开源；本页未处理任何真实健康数据。

## 定位

SparkyFitness 是一个自托管的家庭健康与健身记录平台，覆盖饮食、训练、饮水、睡眠、禁食、情绪、经期、药物和身体指标，并提供多用户、细粒度共享、设备/服务同步、报表和可选的 SparkyAI 对话入口。

2026-09-16 的 GitHub 官方 TypeScript Trending 抓取显示约 `+55 stars today`；REST API 快照为 `6,002 stars / 367 forks / 154 open issues`，API 许可证为 `NOASSERTION`。最新 release 是 2026-09-14 的 `v1.7.1`，main 最近 push 为 2026-09-15。

## 用法

上游推荐从 release 资产下载 compose 和环境变量模板：

```sh
mkdir sparkyfitness && cd sparkyfitness
curl -L -o docker-compose.yml \
  https://github.com/CodeWithCJ/SparkyFitness/releases/latest/download/docker-compose.prod.yml
curl -L -o .env \
  https://github.com/CodeWithCJ/SparkyFitness/releases/latest/download/default.env.example
docker compose pull && docker compose up -d
```

默认入口为 `http://localhost:8080`。启用同步、移动端或 SparkyAI 前，应逐项配置 provider、回调地址、用户权限和数据保留策略；升级前按 release 提示备份数据库与环境配置。

## 原理

- 后端 API 和数据库保存健康记录，Web 前端与 iOS/Android 客户端提供录入、图表、家庭共享和同步。
- 连接 Apple Health、Health Connect、Garmin、Fitbit、Oura、Withings、Strava、食物数据库等来源，统一为本地账户下的时间序列与日志。
- OIDC、TOTP、Passkey 与 MFA 用于登录；家庭功能用多种权限拆分可见/可写范围。
- SparkyAI 处于 beta，可通过对话记录饮食、运动、身体数据和步数，也可上传食物图片并保留对话历史。
- `v1.7.1` release 主要修复数据库 migration 与认证初始化顺序，不是 AI 质量或医疗安全版本认证。

## 价值

- 把多个健康领域放进一个自托管数据层，便于家庭成员保留导出、备份和长期趋势控制权。
- 设备同步、手工录入与报表可以相互校验，比只依赖某个厂商账户更可迁移。
- 可选 AI 是附加入口而不是系统成立的前提；不开启 AI 也能使用核心记录能力。
- 上游明确承认比较表由项目自己编写、部分数据可能过时，这种披露有助于避免把营销表当独立评测。

## 风险边界

- LICENSE 只允许非商业使用，并要求衍生作品继续采用同样非商业条款，还包含 contributor assignment；它是 source-available，不是 OSI 开源，商业、组织或收费场景需先取得许可。
- 健康、经期、药物、体重、图片和家庭关系是高敏感数据；self-hosted 仍需 TLS、访问控制、加密备份、最小共享和删除审计。
- SparkyAI 为 beta，模型可能误记分量、药物、周期或身体指标；对话建议不是诊断、治疗或营养处方，写入前必须确认字段和单位。
- 第三方同步会把 token 与健康数据经过外部服务；README 还标注 Yazio 使用非官方 API、Strava 仅部分测试，兼容和账号风险需逐项接受。
- 家庭共享和移动端扩大越权、丢机、推送与错误归属风险；“七种权限”不等于完成了租户隔离审计。
- 本页未部署 `v1.7.1`，没有验证 migration、认证、同步准确性、AI 图像识别、备份恢复或隐私合规。

## 补充建议

1. 先确认许可证是否覆盖家庭、学校、诊所、公司福利或付费托管场景；不确定时向作者取得书面许可。
2. 用合成账号和假健康记录测试 OIDC/MFA、家庭越权、导出、删除、备份恢复和升级 migration，再迁入真实数据。
3. 对每个设备/服务记录 source、同步时间、单位、去重规则和冲突策略；医疗决定只回到原始设备与专业人员。
4. AI 写入采用“提取草稿 → 用户确认字段/单位 → 保存 → 可撤销”的流程，敏感图片优先使用明确的数据保留策略或本地模型。

## 参考资料

- 上游 README：https://github.com/CodeWithCJ/SparkyFitness
- 文档站：https://codewithcj.github.io/SparkyFitness/
- `v1.7.1` release：https://github.com/CodeWithCJ/SparkyFitness/releases/tag/v1.7.1
- 自定义非商业 LICENSE：https://github.com/CodeWithCJ/SparkyFitness/blob/main/LICENSE
- GitHub REST API：https://api.github.com/repos/CodeWithCJ/SparkyFitness
- 上游安装视频：https://www.youtube.com/watch?v=B13IiL2DeQc
