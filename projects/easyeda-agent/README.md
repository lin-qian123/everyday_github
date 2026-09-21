<!-- markdownlint-disable MD013 MD034 -->

# easyeda-agent：通过 typed actions 驱动 EasyEDA Pro 的电子设计 Agent

> 上游仓库：https://github.com/zhoushoujianwork/easyeda-agent · 归类：办公、商业与行业应用 · 本页基于 2026-09-22 的 README、架构 / 功能文档、release、LICENSE / NOTICE 与 REST API 静态整理；未安装连接器、打开工程、运行 DRC 或制作实物 PCB。

## 定位

`easyeda-agent` 把 Agent Skill、本地 CLI / daemon 与 EasyEDA Pro 内的 Connector 串起来，用官方 `eda.*` API执行建库、原理图、PCB、丝印、检查和交付动作。其重点不是让模型盲点坐标，而是为工程对象提供有类型的输入输出、写前守卫、写后回读和审计资产。

2026-09-22 的 GitHub 官方 Go Trending 抓取显示约 `+13 stars today`；REST API 快照为 `499 stars / 67 forks / 15 open issues`，API 未识别 SPDX，但根目录 LICENSE 为 MIT，`extension/src/beautify/` 保留 Apache-2.0 与 NOTICE；最新 release 为 `v1.5.2`（9 月 20 日）。

## 用法

macOS / Linux 的上游安装入口如下；生产环境建议先下载、审查脚本和 checksum 再执行：

```sh
curl -fsSL https://raw.githubusercontent.com/zhoushoujianwork/easyeda-agent/main/install.sh | bash
easyeda daemon start
easyeda health
```

随后在 EasyEDA Pro 安装 `easyeda-agent-connector.eext`，打开目标工程并显式允许外部交互。可从读取当前工程、离线 `dryRun` 与只读检查开始，再逐步开放写入、保存与制造文件导出。

## 原理

- Agent 通过 Skill 把自然语言任务拆成 `easyeda` CLI 的 typed actions。
- 本地 daemon 与 EasyEDA 内 Connector 通信，由 Connector 调官方 `eda.*` API 读写真实工程对象。
- 原理图流程可执行 layout lint、连接检查、bridge check 与 DRC；PCB 流程结合板框、网络、规则、铺铜和制造检查。
- 修改前核对工程、页面、器件身份与源证据；修改后回读 pin / pad、网络、几何、对象绑定与保存状态。
- 安装资产提供 SHA-256 对账；PCB beautify 的第三方代码在 NOTICE 中单独保留来源与许可。

## 价值

- 相比截图点击，typed action 与回读结果更适合重试、审计和发现部分成功。
- 能把 datasheet 型号、证据页、symbol、footprint、device 和 pin↔pad 映射纳入一条可检查链路。
- CLI、Skill、stdio MCP 三种入口可被不同 harness 复用，且输出可进入版本化工程记录。
- 能明确报告 API 不可得数据、自动路由范围和需要人工决策的器件差异。

## 风险边界

- EasyEDA 扩展 API 不提供通用编程式 undo；保存 checkpoint、回读与 DRC 只能降低风险，不能保证恢复每次错误写入。
- DRC / DFM 通过不等于电路功能、安规、EMC、热设计、信号完整性、可制造性或实物装配验证通过。
- 受控阻抗所需介质厚度、Er、铜厚不能从当前 API 完整读取；Agent 不应自动声称阻抗合格。
- PDF OCR、封装后缀、推荐焊盘与 LCSC 匹配一旦错误，会把看似一致的结构化结果带进生产文件。
- Connector 获得工程写权限；远程 MCP、供应链脚本与 Agent prompt 都需按高权限 CAD 工具治理。

## 补充建议

1. 在工程副本、独立个人库和测试 EasyEDA 账号上启用，先验证 read / dry-run / diff / save 流程。
2. 对 datasheet 页码、完整料号、封装图、pin↔pad 与 LCSC C 号设置人工确认 gate。
3. 每次关键写入前导出版本或项目副本；完成后除软件检查外，再做 ERC、原理审查、Gerber / BOM / pick-and-place 人工复核。
4. 实物投板前由有资质工程师核查电气额定值、安规间距、EMC / SI / PI、热与制造能力。

## 参考资料

- 上游 README：https://github.com/zhoushoujianwork/easyeda-agent
- 快速开始：https://github.com/zhoushoujianwork/easyeda-agent/blob/main/docs/quick-start.md
- 架构：https://github.com/zhoushoujianwork/easyeda-agent/blob/main/docs/architecture.md
- 功能与边界：https://github.com/zhoushoujianwork/easyeda-agent/blob/main/docs/FEATURES.md
- `v1.5.2` release：https://github.com/zhoushoujianwork/easyeda-agent/releases/tag/v1.5.2
- GitHub REST API：https://api.github.com/repos/zhoushoujianwork/easyeda-agent
- LICENSE / NOTICE：https://github.com/zhoushoujianwork/easyeda-agent/blob/main/LICENSE · https://github.com/zhoushoujianwork/easyeda-agent/blob/main/NOTICE
