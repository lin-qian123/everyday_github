<!-- markdownlint-disable MD013 -->

# AI Native Call Center（rasonyang/ai-native-callcenter）中文解读

> 上游仓库：<https://github.com/rasonyang/ai-native-callcenter> · 归类：办公、商业与行业应用 · 本页基于 2026-10-14 的 README、部署 / flow / design 文档、Release、许可证与 GitHub REST API 静态整理；未接入号码、SIP、真实客户、语音 provider 或录音存储。

## 定位

AI Native Call Center 是自托管、API-first 的 AI 呼叫中心。FreeSWITCH 接入电话，speech-to-speech provider 默认应答，flow engine 控制阶段和工具；需要人工时转入 `mod_callcenter` queue，浏览器 agent desktop 与配套 Chrome SIP phone 接管，并把 bot 与人工阶段合并为一条 CDR、transcript 和 recording。

## 用法

上游可用 installer 部署 Go 单体、PostgreSQL 与 FreeSWITCH，并在首次安装选择 OpenAI、Qwen、Doubao、Gemini 或自建 Realtime gateway。默认 demo seed 会生成账号、号码、队列与历史；正式环境应使用 `--no-demo`、独立管理员、TLS reverse proxy、专用号码和最小化 provider key。

## 原理

- FreeSWITCH 处理 SIP / queue / agent leg，应用内 SIP UAS 把 caller audio 接到实时语音 provider。
- flow 以 phase、instruction、tool 与 transition 约束对话；每个 live call 由单 goroutine actor 管理状态。
- REST + SSE 驱动 agent desktop、wallboard 和 screen pop；OpenAPI 是 server / client contract 源。
- transcript、recording、party events 与 transfer 共享 call ID，避免把一次通话拆成不连贯记录。

## 价值

- 把 AI 应答、人工队列、转接、录音、CDR 与 supervisor surface 放在同一可审计数据模型中。
- provider adapter 与 declarative flow 分离，便于比较不同实时语音服务而不重写整套电话系统。
- 文档明确写出模型会误记 slot、provider 指令更新差异、DTMF 限制与 live verification 范围，证据边界较诚实。

## 风险边界

- 电话录音、transcript、号码、客户事实与 agent 行为均为高敏感数据；合法录音告知、跨境传输、保留期、访问和删除要求取决于司法辖区。
- 文档明确警告 DTMF 数字会经过模型、transcript 和日志，不能用于收集 PIN 或银行卡号。
- flow prompt 与 tool schema 不能阻止模型误记、越权承诺或 prompt injection；所有 backend write 需幂等、鉴权、预算与人工升级。
- installer 会拉取脚本 / 镜像并生成高权限 secret；demo 账号共享生成密码，只适合隔离演示，不能直接暴露公网。

## 补充建议

- 用内部测试号码、合成客户和不可消费的 mock backend 做端到端演练，覆盖中断、沉默、噪声、错转、provider 断线与人工接管。
- 建立显式 consent、录音 / transcript 分级、短保留期、PCI / 健康信息禁采和 DSAR 删除流程。
- 对每个 flow 做确定性 simulator、live provider A/B 与人工抽检；将模型成功率、电话接通率、业务正确率和客户体验分开统计。

## 参考资料

- GitHub 仓库：<https://github.com/rasonyang/ai-native-callcenter>
- GitHub REST API：<https://api.github.com/repos/rasonyang/ai-native-callcenter>
- `v0.4.0` Release：<https://github.com/rasonyang/ai-native-callcenter/releases/tag/v0.4.0>
- Design overview：<https://github.com/rasonyang/ai-native-callcenter/blob/main/docs/design/00-overview.md>
- Flow authoring：<https://github.com/rasonyang/ai-native-callcenter/blob/main/docs/flow-authoring.md>
- One-line installer：<https://github.com/rasonyang/ai-native-callcenter/blob/main/deploy/one-line-installer.md>
- LICENSE：<https://github.com/rasonyang/ai-native-callcenter/blob/main/LICENSE>
