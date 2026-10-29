<!-- markdownlint-disable MD013 -->

# QwenPaw

## 定位

QwenPaw 是 AgentScope 团队的个人 / 团队 Agent 工作站，结合文件工作区、ReMe 记忆、插件 / Skills、定时任务、多聊天渠道和本地或云模型。主线采用 Python 后端与 Web / 桌面入口；本地部署是否保留数据在本机，取决于模型、插件、渠道和遥测配置。

2026-10-30 快照：TypeScript daily +116 stars；API 累计 36,882 stars / 3,236 forks / 1,119 open issues（含 PR）。核读 main `5d4f8fd9ea1b`；发行 API 首项 [v2.3.0-beta.1](https://github.com/agentscope-ai/QwenPaw/releases/tag/v2.3.0-beta.1)，2026-10-27 UTC，预发行。以下为文档与有限源码核读，未安装运行。

## 用法

主线要求 Python >=3.11、<3.14。在专用虚拟环境中选择已审阅版本安装，然后用交互初始化检查选择：

```bash
python -m pip install qwenpaw
qwenpaw init
qwenpaw app
```

打开 `http://127.0.0.1:8088/`，在 Settings → Models 选择模型。README 提供 QwenPaw Local、Ollama、LM Studio 和云 provider；先只接本地模型与测试目录。这里使用交互 init，因为上游说明 --defaults 会自动接受遥测。命令未执行，实际包版本需另锁定；本轮发行首项为预发行。

## 原理

工作记忆、完整会话和可编辑 Markdown 知识库构成三层记忆；Skills / 插件与 MCP 扩展工具。文档列出 Sandbox、Tool Guard、File Guard、Skill Scanner、Access Policy 五层，分别处理执行隔离、调用规则、文件范围、技能扫描和能力授权；不同层的开关和宿主实现应分别核对。

## 价值

适合将个人知识、文件处理和消息渠道接成常驻助手。相比单次聊天，多渠道和定时任务能提供持续入口，同时提高对身份、工作区隔离、任务生命周期和备份的要求。

## 风险边界

- 根 Apache-2.0 不覆盖所有内置材料的再利用判断。实际核读 docx-en/LICENSE.txt，载有 Anthropic 服务协议及复制 / 分发等限制；其他 Office 技能目录也各有 LICENSE.txt，使用或打包前逐项核清。
- README 遥测段只介绍每版本 init 收集；主线 daily_telemetry.py 另定义 runtime_active 发送器，含持久 runtime UUID、UTC activity_date、环境信息和 deployment_mode。该文件是静态证据，本轮未追完所有触发调用或抓包，不能声称实测发送频率。
- telemetry.py 支持 QWENPAW_TELEMETRY_DISABLED 进程开关和保存的 opted_out；daily sender 也检查该退出逻辑。应检查所用发行包是否包含相同实现。
- 模型 key、聊天渠道、浏览器和 MCP 能形成不同出口；“本地部署”不能替代逐条数据流检查。
- Tool Guard 有 STRICT / SMART / AUTO / OFF 等级；安全层存在不保证所有平台、工具和绕过输入都被覆盖。
- 桌面版本仍标 beta；v2.3.0-beta.1 不是稳定发行。不要将主线能力直接归给 stable 镜像或任意 PyPI 包。

## 补充建议

先建两个隔离用户 / 工作区，用假 key、恶意技能 fixture 和授权测试消息检验记忆串读、文件拒绝、工具审批、定时任务取消及恢复。对固定包观察 init 与运行期网络，核对 opt-out 后行为；Office 技能许可未澄清前避免整体再分发。

## 参考资料

- [上游仓库](https://github.com/agentscope-ai/QwenPaw)、[仓库 API](https://api.github.com/repos/agentscope-ai/QwenPaw)。
- [README.md](https://github.com/agentscope-ai/QwenPaw/blob/5d4f8fd9ea1bb181f3509791dc539a376861ec73/README.md)。
- [src/qwenpaw/utils/telemetry.py](https://github.com/agentscope-ai/QwenPaw/blob/5d4f8fd9ea1bb181f3509791dc539a376861ec73/src/qwenpaw/utils/telemetry.py)。
- [src/qwenpaw/utils/daily_telemetry.py](https://github.com/agentscope-ai/QwenPaw/blob/5d4f8fd9ea1bb181f3509791dc539a376861ec73/src/qwenpaw/utils/daily_telemetry.py)。
- [pyproject.toml](https://github.com/agentscope-ai/QwenPaw/blob/5d4f8fd9ea1bb181f3509791dc539a376861ec73/pyproject.toml)。
- [LICENSE](https://github.com/agentscope-ai/QwenPaw/blob/5d4f8fd9ea1bb181f3509791dc539a376861ec73/LICENSE)。
- [src/qwenpaw/agents/skills/docx-en/LICENSE.txt](https://github.com/agentscope-ai/QwenPaw/blob/5d4f8fd9ea1bb181f3509791dc539a376861ec73/src/qwenpaw/agents/skills/docx-en/LICENSE.txt)。
