# omnigent（omnigent-ai/omnigent）

- GitHub: https://github.com/omnigent-ai/omnigent
- 官网: https://omnigent.ai
- 记录日期: 2026-06-17 (Asia/Shanghai)

## 定位

`omnigent` 是一个多 agent 共用的 meta-harness。它试图把 Claude Code、Codex、Pi 和自定义 agent 放到同一个会话、同一套策略和同一层沙箱治理之下，更像“agent supervisor / runtime 层”，而不是又一个单点对话框。

## 热度信号

1. GitHub API 在 2026-06-17 抓取时显示约 `2,797 stars`、`326 forks`。
2. GitHub API 显示仓库在 `2026-06-17` 仍有推送，迭代节奏较快。
3. 官方 README 明确支持浏览器、手机、桌面和本地终端接续同一会话，也支持把多个 agent 放进同一 live session。

## 用法

### 1) 一键安装

```bash
curl -fsSL https://raw.githubusercontent.com/omnigent-ai/omnigent/main/scripts/install_oss.sh | sh
```

如果想手动安装：

```bash
uv tool install omnigent
```

### 2) 启动默认会话

```bash
omnigent
```

它会自动启动本地 Web UI，默认地址是：

```text
http://localhost:6767
```

### 3) 指定特定 harness

```bash
omnigent claude
omnigent codex
omnigent run path/to/agent.yaml
```

## 原理

1. `omnigent` 在上层提供统一会话模型，下层再适配 Claude Code、Codex、Pi 或自定义 agent。
2. 它把多 agent 协作、共享上下文、共享文件和共享策略做成一个统一运行时，而不是靠一堆临时脚本串起来。
3. 支持通过 policy 控制审批、花费上限、工具访问范围，把治理层前置。
4. 还提供云沙箱与本地 host 模式，使“在本机跑”和“在远端隔离环境跑”尽量走同一条操作路径。

## 价值

- 对需要同时比较多个 agent、让不同 agent 互审、或让团队成员共同观察同一执行过程的人很有吸引力。
- 这类中间层能显著降低“换 agent 就要重写一套工作流”的成本。
- 它把多设备接续、共享会话和 agent 治理放进同一个产品里，比单纯的 CLI wrapper 更接近团队级工具。

## 风险边界

- 多 agent 共用会话会放大权限、审计和成本归因问题，尤其在团队场景里更明显。
- 该项目仍处于 alpha 阶段，适合试验与工具链探索，不宜直接假设为稳定生产基座。
- 一旦把多个供应商 agent 接到同一层，凭证管理、数据边界和日志留存策略都要单独设计。

## 补充建议

1. 先拿它做“多 agent 对照实验”和“共享会话观察”，不要一上来就给核心仓库最高权限。
2. 尽量从只读工具和低风险目录开始，逐步验证 policy 是否真能拦住高风险操作。
3. 如果团队已经有成本统计或审计需求，接入前先定义好 session、agent、tool 三个维度的责任边界。

## 参考资料

- https://github.com/omnigent-ai/omnigent
- https://omnigent.ai
- https://omnigent.ai/docs
- https://ossinsight.io/trending
