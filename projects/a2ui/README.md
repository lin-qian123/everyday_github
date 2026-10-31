<!-- markdownlint-disable MD013 -->

# a2ui

- 上游：[a2ui-project/a2ui](https://github.com/a2ui-project/a2ui)；分类：前端、UI 与 Agent 交互层。
- 核读：2026-11-01（Asia/Shanghai）；固定主线 `825beac2813a6d0ccef3b6fb4124ad6c3c8419f0`。
- [仓库 API](https://api.github.com/repos/a2ui-project/a2ui) 快照：16,914 stars / 1,356 forks / 552 open issues（含 PR）；发行首项 [cli-v0.1.0](https://github.com/a2ui-project/a2ui/releases/tag/cli-v0.1.0)，2026-10-30 UTC。发行与主线分别看。
- 证据：上游文档及指定文件静态核读；本轮未安装运行、调用模型或复现作者实验。

## 定位

A2UI（Agent-to-User Interface）是一套声明式 JSON 消息格式、组件 catalog 与 renderer 实现，让 Agent 返回可更新的表单、卡片等 UI，由应用自己的组件渲染。它位于界面描述层，可经 A2A / AG-UI 等传输，不替代传输协议或业务后端。官方 TypeScript daily 榜本轮显示 +14 stars。

## 用法

固定 README 的 Restaurant Finder 示例需要 Node.js 18+ / Corepack、uv 和 Gemini key：

```bash
git clone https://github.com/a2ui-project/a2ui.git
cd a2ui
git checkout 825beac2813a6d0ccef3b6fb4124ad6c3c8419f0
corepack enable
yarn install
cd samples/client/lit
yarn demo:restaurant
```

运行前在环境配置 `GEMINI_API_KEY`；示例会启动 Python agent 与 Lit 客户端，并向 Gemini 发请求。先用固定 JSON payload 验 renderer，再开模型生成，可把协议问题与模型问题分开。

README 将 v0.9.1 列为当前 production release、v1.0 为 release candidate、v0.8 为 legacy；仓库发行列表首项 `cli-v0.1.0` 是 CLI 组件，不能当作协议当前版本。

## 原理

Agent 发组件与数据更新，客户端按 ID 建立组件关系和绑定，在可信 catalog 中解析实现；用户事件再回到应用 / Agent。v0.9 协议把结构、数据和事件分离，允许逐步创建、更新和删除 surface。消息有状态依赖，必须按序交付并校验 schema / catalog，不能任意重排。

自定义组件可映射既有框架控件或 iframe，但具体可信程度取决于宿主实现、远程资源策略和业务动作处理。声明式 payload 缩小任意代码执行面，并不自动验证内容真实或赋予动作权限。

## 价值

把模型输出限制到可维护的组件词汇，便于统一品牌、可访问性与跨客户端表现；适合动态数据采集、审批面板和远程 Agent 返回 UI。比自由 HTML 更容易做 schema 验证，但仍需真实交互验收。

## 风险边界

- 项目仍标为 early-stage public preview；文档中稳定协议、候选版和各语言包版本并存，renderer 不能仅凭名称假定相互兼容。
- 合法 JSON 仍可能包含误导文字、恶意链接、不合理字段或诱导提交。catalog、URL / 资源规则、事件授权与业务端校验都要由宿主落实。
- 自定义 wrapper / iframe 可以扩大执行面，不能将 README 的安全理念直接当作完整沙箱保证。
- 示例依赖云模型；API key 和业务输入的出口需单独管理。代码主要 Apache-2.0，根 LICENSE 另列 `eval/bin/transcrypt` 的 MIT 例外。

## 补充建议

固定协议 / renderer / catalog 三者版本，建立未知组件、错误绑定、乱序消息、重复提交、恶意 URL 和不完整流的 fixture。用键盘、读屏和手机实际操作表单；只在业务后端授权通过后执行提交，保留模型原始 payload 与渲染错误方便重放。

## 参考资料

- [固定 README / 版本口径](https://github.com/a2ui-project/a2ui/blob/825beac2813a6d0ccef3b6fb4124ad6c3c8419f0/README.md)。
- [Restaurant Finder 示例](https://github.com/a2ui-project/a2ui/blob/825beac2813a6d0ccef3b6fb4124ad6c3c8419f0/docs/public/quickstart.md)。
- [catalog 与验证](https://github.com/a2ui-project/a2ui/blob/825beac2813a6d0ccef3b6fb4124ad6c3c8419f0/docs/public/concepts/catalogs.md)。
- [v0.9 协议与消息顺序](https://github.com/a2ui-project/a2ui/blob/825beac2813a6d0ccef3b6fb4124ad6c3c8419f0/specification/v0_9/docs/a2ui_protocol.md)。
- [Apache-2.0 与 MIT 例外](https://github.com/a2ui-project/a2ui/blob/825beac2813a6d0ccef3b6fb4124ad6c3c8419f0/LICENSE)。
