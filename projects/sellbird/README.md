<!-- markdownlint-disable MD013 -->

# sellbird

## 定位

Sellbird 是从公司发现、联系人整理、邮箱验证到邮件草拟、发送和回复处理的销售外联工作流。程序在本机保存配置与数据库，通过已有 Claude / ChatGPT 订阅对应的 CLI 调用模型；本机运行不等于离线，也不等于无需邮箱和外部服务。

- 上游：[ethanplusai/sellbird](https://github.com/ethanplusai/sellbird)，仓库 ID `1179388779`；旧 `ethanplusai/harvey` API 返回迁移到同一 ID。这里的 Harvey 与同名法律 AI 产品不能混为一谈。
- 2026-11-19 07 时段：官方 Python daily **+358**；stars / forks / open issues（含 PR）为 **6,486 / 1,337 / 60**。[API](https://api.github.com/repos/ethanplusai/sellbird)
- 核到的最新非预发行版为 [v0.4.0](https://github.com/ethanplusai/sellbird/releases/tag/v0.4.0)，UTC 11-06；当前包也标为 0.4.0。本页抽读 main `b212385259da92246a56311d790d936e75dd70dd`，不将同版本号视为制品与主线完全一致。
- 分类：`办公、商业与行业应用`。本轮核过 `projects/` 及旧名链接，没有已有的同一上游档案。

## 用法

需要 Python **3.11+**、已登录且可用的模型 CLI，以及后续明确授权的邮箱。以下只是安装参考；本轮没有安装、读取登录凭据、搜集联系人或发送邮件。

```bash
git clone https://github.com/ethanplusai/sellbird.git
cd sellbird
git checkout b212385259da92246a56311d790d936e75dd70dd
python -m venv .venv
source .venv/bin/activate
python -m pip install -e .
cp .env.example .env
```

按文档填写最小配置，先用虚构公司和测试邮箱核验：`sellbird train <你的公司网址>` 会联网并写本地配置；`signals --confirm free` 确认线索；`discover` 检索公司；`dashboard` 打开本地控制台；`run` 启动循环。初次接入应保留默认审批，逐封核对事实后再决定外发；`sellbird sending pause` 是暂停入口。主 README 的快速开始会写数据和调用服务，不是只读演示。[README](https://github.com/ethanplusai/sellbird/blob/b212385259da92246a56311d790d936e75dd70dd/README.md)、[包与命令入口](https://github.com/ethanplusai/sellbird/blob/b212385259da92246a56311d790d936e75dd70dd/pyproject.toml)

## 原理

- **确定性编排**：默认约每 15 分钟检查预算与待办，优先处理回复、发送、写草稿，再找客户。网页读取、邮箱验证和邮件操作由程序负责，模型主要返回文本。
- **模型调用边界**：上游文档声明 Claude 以 safe-mode、无工具和空临时目录运行；Codex 使用临时 home / workspace 的 app-server，并在发送提示前核配置、账号和工具状态。本文核读的是实现说明与相关发送代码，没有实际验证 CLI 隔离。[工作原理](https://github.com/ethanplusai/sellbird/blob/b212385259da92246a56311d790d936e75dd70dd/docs/how-it-works.md)、[Codex 接入契约](https://github.com/ethanplusai/sellbird/blob/b212385259da92246a56311d790d936e75dd70dd/docs/codex.md)
- **Outbox 审批**：发送端先生成逐封 outbox 记录；copilot 状态待审核，autopilot 可自动批准。发送前再做收件人对应、地址可投递性、模板残留、长度和链接等确定性检查；切回审批模式会把尚未发出的自动批准项送回审核队列。[发送代码](https://github.com/ethanplusai/sellbird/blob/b212385259da92246a56311d790d936e75dd70dd/sellbird/agents/sender.py)、[模式切换](https://github.com/ethanplusai/sellbird/blob/b212385259da92246a56311d790d936e75dd70dd/sellbird/sending_mode.py)

## 价值

将调查、写作、审批和发送状态放进一个可查看的工作流，便于从半自动草稿开始，而不用立即开放自动发送。也可停在验证阶段导出 CSV。是否提高有效回复率，必须和原有人工流程对照，计入退信、退订、错误陈述及人审时间；stars、演示 GIF 和模型输出不能证明销售收益。

## 风险边界

- **默认审批可以改变。** 上游提供 `--approve-all` 和 autopilot；前置规则也不能判断每个商业事实。程序对“网站没有预约”等信号的判断可能因异步组件、其他页面而出错；审批人必须核事实。[审批与发送](https://github.com/ethanplusai/sellbird/blob/b212385259da92246a56311d790d936e75dd70dd/docs/approval-and-sending.md)
- **无模型 API key 不等于免费或不外发。** 提示和回复仍到所选模型服务，邮箱、验证、付费线索源可产生费用；订阅限额读不到时文档写会回退到每日调用预算。不能将上游价格表当作当前供应商报价或无限额度。
- **登录材料与本机数据敏感。** Codex 文档要求文件型登录存储，并把去掉 refresh token 的副本交给临时运行环境；不支持 OS keyring。文档验证的 CLI 版本为 0.159.3，这不代表任意新版都已兼容。真正部署须核 CLI 协议、登录续期和凭据清理，不能仅依赖 README 的隔离承诺。
- **控制台并非普通看板。** 文档写它可改邮件配置、批准邮件和启动流程，使用 loopback、Bearer token 及 Host / 跨站校验。token 位于本地数据目录；同一 OS 用户的程序仍可读 token、`.env` 和数据库。不要因 localhost 就放宽本机权限或把服务直接暴露公网。[控制台](https://github.com/ethanplusai/sellbird/blob/b212385259da92246a56311d790d936e75dd70dd/docs/dashboard.md)、[安全边界](https://github.com/ethanplusai/sellbird/blob/b212385259da92246a56311d790d936e75dd70dd/SECURITY.md)
- **数据、送达和权利分别核。** 联系人处理和外联应有相应授权及退订机制；发送重试、服务商已接受但本机未落库等异常仍需测试。当前代码声明 `AGPL-3.0-only`，0.3.x 及以前的历史 MIT 与当前条款分开；托管产品另行评估。[LICENSE](https://github.com/ethanplusai/sellbird/blob/b212385259da92246a56311d790d936e75dd70dd/LICENSE)

## 补充建议

用 `.test` 虚构数据先测草稿事实、审批模式切换、暂停、退订、重复回复和发送结果未知等路径。把公司发现、模型调用、邮箱连接和实际发送分阶段授权；建立“待审 / 已批 / 已提交服务商 / 结果未知 / 退信”的日志对账。旧 Harvey 升级前停止旧进程、备份配置与 SQLite，再核文件迁移；本轮没有执行迁移、外联或隔离测试。

## 参考资料

- [v0.4.0 改名及许可变化](https://github.com/ethanplusai/sellbird/releases/tag/v0.4.0)
- [发行列表](https://github.com/ethanplusai/sellbird/releases)；其余固定 SHA 资料按用途链接于各节。
