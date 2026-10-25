<!-- markdownlint-disable MD013 -->

# llama-swap：按请求切换本地推理服务的模型代理

- 主上游：[mostlygeek/llama-swap](https://github.com/mostlygeek/llama-swap)；repository ID `867433720`。
- 采样日期：2026-10-26（Asia/Shanghai）；分类：模型、训练与推理基础设施。
- API 累计快照：6,079 stars / 521 forks / 114 open issues（含 PR 口径）；与榜单日增分开。
- 默认分支 `main`，本页静态依据固定在 `f803258d1c538d3374827d436f2ca90ddcd85d9e`。发行 API 首项 [v266](https://github.com/mostlygeek/llama-swap/releases/tag/v266)，UTC 2026-10-22T20:11:07Z，正式发行。
- 核验层级：读取上游文档、许可、元数据及所列部分实现；未安装运行上游、调用模型或复现实验。

## 定位

llama-swap 是用 Go 编写的推理服务代理与进程管理器，根据请求中的 model 启动或切换对应后端。它能对接 OpenAI / Anthropic 兼容接口及部分音频、图像服务；模型权重、推理引擎与 GPU 驱动仍由用户准备，不是下载一个二进制就具备所有模型能力。

## 用法

安装已选定版本的二进制，准备自己的后端和配置。上游 Homebrew 方式如下，本轮未执行：

```bash
brew tap mostlygeek/llama-swap
brew install llama-swap
llama-swap --config path/to/config.yaml --listen localhost:8080
```

最小配置按模型 ID 指定 llama-server 命令、模型文件和自动端口。多人或远端客户端接入前配置真实 apiKeys 与网络访问边界；不要使用示例 key。容器内部绑定 0.0.0.0 才能通过端口映射访问，而宿主发布地址仍需另限本机或可信网络。

## 原理

代理读出模型 ID，查配置、健康检查并把请求转发给对应进程；基础配置同一时刻保留一个模型，matrix 可显式允许多模型并存，ttl 可在空闲后卸载。别名、profiles 和参数过滤调整路由及请求，cmd / cmdStop 管理后端生命周期。它通过换进程减少常驻模型占用，不能让超出单机容量的模型自动适配，也不能消除装载与排队延迟。

## 价值

适合显存有限、需要在代码、嵌入、视觉或语音后端之间切换的个人工作站：客户端可保留统一 API 入口，后端单独升级。评估时应同时看冷启动、首 token、并发排队、卸载失败和显存峰值，不能只比较热模型吞吐。

## 风险边界

- **默认无认证。** apiKeys 为等权访问 key，没有每 key 速率限制、账号、角色或细粒度权限；也覆盖 Web UI 与 /api/。bearer key 不能替代防火墙，配置中的命令会启动真实主机进程。
- 文档中的 captureBuffer 默认分配 10 MB 保存请求 / 响应捕获，设 0 可关闭；示例值是 15 MB，不能误当默认。日志、有效配置、模型路径和环境宏可能包含敏感信息，分享前要检查。
- /api/mcp 默认可用，提供文档、构建时源码及脱敏后的运行配置；helpagent.disable 可同时关闭 Help 与该端点。其文档注明仅支持 MCP 2026-07-28，本轮只核上游实现契约，未验证客户端兼容或脱敏完备性。
- 容器镜像的权限、设备和目录挂载需要独立收敛。默认镜像以 root 运行，统一镜像包含额外推理引擎；“无外部依赖”描述的是代理二进制分发，不代表模型服务和 CUDA 等依赖消失。
- main 与 v266、nightly 容器不必一致；模型及第三方引擎有独立许可，代理代码为 MIT。接入远端 peers 时，请求数据也会离开本机。

## 补充建议

从两个可在本机容纳的小模型开始，固定后端路径、权重哈希与代理版本，测交替请求、超时、流式取消及退出后显存释放。关闭不需要的捕获 / Help，配置环境宏而非明文 key；用无 secret 的 fixture 验证错误日志和 MCP 有效配置脱敏，再扩大网络可达范围。

## 参考资料

- [README.md](https://github.com/mostlygeek/llama-swap/blob/f803258d1c538d3374827d436f2ca90ddcd85d9e/README.md)。
- [LICENSE.md](https://github.com/mostlygeek/llama-swap/blob/f803258d1c538d3374827d436f2ca90ddcd85d9e/LICENSE.md)。
- [docs/config.example.yaml](https://github.com/mostlygeek/llama-swap/blob/f803258d1c538d3374827d436f2ca90ddcd85d9e/docs/config.example.yaml)。
- [docs/kb/guides/api-integration/api-keys-and-auth.md](https://github.com/mostlygeek/llama-swap/blob/f803258d1c538d3374827d436f2ca90ddcd85d9e/docs/kb/guides/api-integration/api-keys-and-auth.md)。
- [docs/kb/guides/api-integration/mcp-endpoint.md](https://github.com/mostlygeek/llama-swap/blob/f803258d1c538d3374827d436f2ca90ddcd85d9e/docs/kb/guides/api-integration/mcp-endpoint.md)。
- [docs/kb/guides/operations/container-security.md](https://github.com/mostlygeek/llama-swap/blob/f803258d1c538d3374827d436f2ca90ddcd85d9e/docs/kb/guides/operations/container-security.md)。
- [仓库 API](https://api.github.com/repos/mostlygeek/llama-swap)、[发行 API](https://api.github.com/repos/mostlygeek/llama-swap/releases?per_page=1)；动态元数据仅代表本轮采样。
- 事实来源为以上一手材料；价值、风险评估和建议为本库工程判断，未当作上游实测结果。
