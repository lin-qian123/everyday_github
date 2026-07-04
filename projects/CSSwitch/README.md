# CSSwitch

- GitHub：<https://github.com/SuperJJ007/CSSwitch>
- 抓取时间：2026-07-05（Asia/Shanghai）
- 今日信号：GitHub API 显示该仓库创建于 2026-07-02，抓取时约
  `218 stars / 31 forks`，README 定位为 Claude Science 的第三方模型接入切换工具。

## 定位

`CSSwitch` 是一个 macOS Apple Silicon 菜单栏应用，用本地代理和隔离环境
让 Claude Science 使用用户自己的第三方模型 API。项目作者把它类比为
Claude Science 版本的 CC Switch：不是替代 Science，而是接管推理请求出口。

它属于科研 AI 工作台周边工具，核心价值是把闭源平台的模型入口改造成更可控、
更低成本或更本地化的 provider 选择。

## 用法

README 给出的使用方式是：

1. 安装 Claude Science。
2. 下载 CSSwitch release 中的 DMG。
3. 新建第三方配置，填入 API key 和模型。
4. 点击一键开始，由 CSSwitch 启动本地代理和隔离环境。
5. Science 通过 `ANTHROPIC_BASE_URL` 指向本地代理，再由代理转发到 DeepSeek、
   Qwen、GLM、Kimi、MiniMax、小米 MiMo、硅基流动、OpenRouter 或自定义端点。

项目强调 API key 保存在本机 `~/.csswitch`，代理只监听回环地址，并用路径 secret 验证请求。

## 原理

它的基本链路是：

```text
Claude Science（隔离环境，本地登录）
  -> ANTHROPIC_BASE_URL=http://127.0.0.1:<port>/<secret>
  -> csswitch_proxy.py
  -> 第三方 Anthropic / OpenAI 兼容端点
```

代理会移除 Science 自带 OAuth 信息，注入用户配置的第三方 key，并在需要时做协议转换。
隔离环境用于让 Science 启动，不读取或修改真实 `~/.claude-science` 登录状态。

## 价值

- 对科研 AI 用户：降低被单一模型订阅绑定的程度，方便比较不同模型。
- 对本地隐私：隔离真实 Science 数据目录，key 只存在本机，降低误操作风险。
- 对 AI 工具生态：说明“provider switcher”正在从 Claude Code 扩展到科研 agent 平台。

## 风险边界

- 该工具依赖 Claude Science 的环境变量、启动方式和请求格式，平台更新可能导致失效。
- 使用第三方模型并不等于能力等价，tool use、thinking、长上下文和多模态支持可能存在差异。
- 本地代理处理 API key 和请求内容，运行前应审查源码、release 来源和权限。
- 当前 README 要求系统中有 `python3`，与本仓库日常默认 `python` 习惯不同，使用时应按项目要求执行。

## 补充建议

- 与 `open-science` 一起观察：一个是开源科研工作台愿景，一个是现有闭源平台的 provider 切换层。
- 与 `CC Switch`、`CSSwitch`、各类 OpenAI-compatible proxy 横向比较，关注协议转换对工具调用的损耗。
- 后续关注 notarization、自动更新、日志脱敏和更多本地模型来源支持。

## 参考资料

- GitHub 仓库：<https://github.com/SuperJJ007/CSSwitch>
- README：<https://github.com/SuperJJ007/CSSwitch#readme>
- CC Switch：<https://github.com/farion1231/cc-switch>
