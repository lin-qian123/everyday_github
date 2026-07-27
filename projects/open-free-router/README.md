# open-free-router

## 定位

`open-free-router` 是本地 LLM 路由器、代理和同步工具：它跟踪多个上游的免费模型目录，按模型 ID 转发请求，并提供本机 Web UI 与定时刷新。

截至 2026-07-28，GitHub API 显示其创建于 2026-07-27，约 10 stars、2 forks；属于早期开发者信号。

## 用法

先从源码阅读配置与安装脚本，再为每个上游单独配置最小权限 API key。默认代理绑定 `127.0.0.1`；在将任何端口暴露到局域网或公网前，应自行补齐认证和网络隔离。

```bash
open-free-router add openrouter --base-url https://openrouter.ai/api/v1
open-free-router serve
```

## 原理

项目维护 provider/model 注册表；刷新进程轮询上游目录，代理根据请求中的模型标识选择目标 provider，UI 展示配置与状态。它是路由层，不改变上游模型能力或服务条款。

## 价值

- 将多个兼容 API 的模型目录和本机入口集中，方便原型阶段比较可用模型。
- 本机 loopback 默认值降低了“开箱即公网暴露”的风险。

## 风险边界

- “免费”模型的额度、可用性、数据政策与速率限制随上游变化，不能用于成本或可用性承诺。
- 代理会接触 API key 和请求内容；日志、配置文件和 UI 都必须按敏感数据处理。
- 一键 curl 安装会执行远端代码，应固定版本或先审查脚本。

## 补充建议

将生产请求接入显式的 allow-list、审计日志脱敏、超时/重试与每个 provider 的预算上限；部署前以非敏感测试提示验证模型路由和失效降级。

## 参考资料

- GitHub：<https://github.com/NoelJudeNoel/open-free-router>
- GitHub API 快照：<https://api.github.com/repos/NoelJudeNoel/open-free-router>
