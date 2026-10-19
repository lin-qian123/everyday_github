<!-- markdownlint-disable MD013 -->

# Fabric

> 更新：2026-10-20（Asia/Shanghai）。分类：Agent 框架与技能生态。上游 `danielmiessler/Fabric`；快照 `a7ef0a1c3b8d`（main）。本文基于官方榜单、认证 API 与上游文件静态研究；热度、版本时间与跨平台证据见[当日日报](../../daily/2026-10-20/ai-hotspots.md)。

## 定位

围绕可复用 prompts（patterns）组织常见 AI 任务的开源框架 / CLI，例如摘要、内容提取与分析；可单独采用 pattern 文件，也可用 Go CLI、provider 集成和 REST API。它让任务模板进入命令行管道，不是训练出的专用模型。[README.md](https://github.com/danielmiessler/Fabric/blob/a7ef0a1c3b8d05d13da5298e01344fff0f5751a6/README.md)

## 用法

macOS 可用 `brew install fabric-ai`；包管理器提供的命令可能名为 `fabric-ai`，上游建议按需设置 `fabric` alias。配置模型后，可从低敏感测试文本开始：[README.md](https://github.com/danielmiessler/Fabric/blob/a7ef0a1c3b8d05d13da5298e01344fff0f5751a6/README.md)

```bash
fabric --setup
fabric --listpatterns
cat sample.txt | fabric --pattern summarize
```

二进制应从官方 Release 核对 checksum；一行在线安装脚本要先下载审查。provider、pattern 与上下文保存路径需确认，再处理真实资料。本轮未安装、登录 provider 或运行推理。

## 原理

patterns 主要以任务提示词和输入约定描述输出，CLI 将 stdin / 上下文与选定 pattern 组合后调用 provider。自定义同名 pattern 优先于内置项，可形成个人任务库；可选 REST 服务进一步暴露 patterns、contexts、sessions 与 chat 等管理 / 推理端点。[README.md](https://github.com/danielmiessler/Fabric/blob/a7ef0a1c3b8d05d13da5298e01344fff0f5751a6/README.md)[internal/server/serve.go](https://github.com/danielmiessler/Fabric/blob/a7ef0a1c3b8d05d13da5298e01344fff0f5751a6/internal/server/serve.go)

## 价值

适合将经常重复的个人工作变成可版本化、可比较的命令，方便记录 prompt、模型、输入和结果。无需安装全部框架也能研究 patterns；模板的传播量和 stars 不能证明事实可靠或适用于专业决策。

## 风险边界

- 本地 CLI 不代表本地推理。内容会送往所选 provider；custom patterns 和外部内容可引入 prompt injection，输出需要来源校对。`~/.config/fabric/.env` 包含 API key / 部分 OAuth token，文档称写为 0600，备份和日志仍需保护。[docs/SECURITY.md](https://github.com/danielmiessler/Fabric/blob/a7ef0a1c3b8d05d13da5298e01344fff0f5751a6/docs/SECURITY.md)
- 当前 REST 源码拒绝没有 API key 的非 loopback bind；无 key 的 loopback 模式另有 Host / Origin guard，不能说服务默认任意公网开放。启用 key 时 Swagger 路径豁免，源码注明错误 key 无次数限制，强 key、TLS 和代理限流仍需自行配置。[internal/server/auth.go](https://github.com/danielmiessler/Fabric/blob/a7ef0a1c3b8d05d13da5298e01344fff0f5751a6/internal/server/auth.go)[internal/server/serve.go](https://github.com/danielmiessler/Fabric/blob/a7ef0a1c3b8d05d13da5298e01344fff0f5751a6/internal/server/serve.go)
- server 初始化设 `NoSystemPlugins=true`，限制可读环境 / 文件、取 URL 或执行扩展的 pattern 插件；这个限制不能外推到普通 CLI、额外脚本或全部外部工具。[internal/server/serve.go](https://github.com/danielmiessler/Fabric/blob/a7ef0a1c3b8d05d13da5298e01344fff0f5751a6/internal/server/serve.go)
- 自定义 pattern 可覆盖内置名，审查时要核实际解析文件；代码 MIT，provider / 外链内容和服务另有条款。采样 latest Release 为 `v1.4.528`，本文源码为 main 快照，升级后要重核相关行为。[README.md](https://github.com/danielmiessler/Fabric/blob/a7ef0a1c3b8d05d13da5298e01344fff0f5751a6/README.md)[LICENSE](https://github.com/danielmiessler/Fabric/blob/a7ef0a1c3b8d05d13da5298e01344fff0f5751a6/LICENSE)

## 补充建议

对摘要、提取和评审各准备少量有答案的样本，固定 pattern hash / 模型 / 参数并比较事实错漏、格式失败、延迟和费用。启用 REST 前验证匿名、错 key、跨 Origin、超大 body 与配置读取；不要把能输出 Markdown 作为任务正确验收。

## 参考资料

- [README.md](https://github.com/danielmiessler/Fabric/blob/a7ef0a1c3b8d05d13da5298e01344fff0f5751a6/README.md)
- [LICENSE](https://github.com/danielmiessler/Fabric/blob/a7ef0a1c3b8d05d13da5298e01344fff0f5751a6/LICENSE)
- [docs/SECURITY.md](https://github.com/danielmiessler/Fabric/blob/a7ef0a1c3b8d05d13da5298e01344fff0f5751a6/docs/SECURITY.md)
- [internal/server/auth.go](https://github.com/danielmiessler/Fabric/blob/a7ef0a1c3b8d05d13da5298e01344fff0f5751a6/internal/server/auth.go)
- [internal/server/serve.go](https://github.com/danielmiessler/Fabric/blob/a7ef0a1c3b8d05d13da5298e01344fff0f5751a6/internal/server/serve.go)
- [仓库 API](https://api.github.com/repos/danielmiessler/Fabric)
- [v1.4.528 Release](https://github.com/danielmiessler/Fabric/releases/tag/v1.4.528)
