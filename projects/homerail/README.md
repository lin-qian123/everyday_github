# homerail

<!-- markdownlint-disable MD013 -->

## 定位

`homerail` 是一个 TypeScript 本地 agent 编排 runtime，强调把一次性聊天变成可审计、可复用的 DAG 工作流。它的长期愿景是“家用/个人数据中心 agent”：用户用语音输入，系统生成当下需要的界面，背后由多个 agent 沿着显式 DAG 节点执行。

截至 2026-07-11，GitHub API 显示该仓库约 407 stars，创建于 2026-07-07，许可证为 MIT。它的热度说明 agent 控制面正在从“终端会话”扩展到“语音入口 + DAG + 本地 worker + 生成式 UI”。

## 用法

README 的快速启动要求 Node.js 20+、npm 10+、Docker，以及 Claude Agent SDK-compatible 模型端点。典型流程：

```bash
npm run install:all
npm run build
cd homerail_cli && npm link && cd ..
hr start
hr doctor
hr run assets/orchestrations/public-two-node.yaml.template \
  --profile offline-deterministic \
  --prompt "Draft a short checklist for a backend release"
```

核心 CLI 包括 `start`、`doctor`、`run`、`dag supervise`、`scorecard`、`eval-run`、`replay` 等。

## 原理

HomeRail 把 agent 执行拆成显式 DAG：每个节点可以有独立 worker、workspace、handoff、scorecard 和 run evaluation。Manager 和 Node 作为本地服务运行，Node 用 Docker 为 DAG 节点启动 worker 容器，同一次 run 共享 workspace。

语音层提供 ASR / TTS / VAD contract，中文为默认方向之一。生成式 UI 仍处于探索阶段，目标是不把日志和 JSON 直接丢给用户，而是生成更适合浏览的结构化视图。

## 价值

- 把 agent 任务从黑盒聊天转成可监督、可回放、可评分的 DAG。
- 本地优先，适合 homelab、NAS 或个人服务器场景。
- 语音入口降低了非工程用户操作 agent 的成本。
- CLI 和离线 deterministic profile 让拓扑检查不依赖模型端点。

## 风险边界

- 项目仍处在早期，生成式 UI contract 和 widget set 会变化。
- live agent run 依赖模型端点，成本、隐私和稳定性要单独评估。
- Docker worker 能执行代码，必须限制工作目录、网络和凭据。
- 本地服务若绑定 `0.0.0.0` 可能暴露到局域网，应默认保持 localhost。

## 补充建议

- 与 `agent-chief`、`open-connector`、`OpenTag` 一起观察：它们分别处理注意力、连接器和团队入口，HomeRail 偏本地 DAG runtime。
- 如果用于家庭自动化，应先从只读/模拟任务开始，逐步增加审批和权限边界。
- 建议后续关注 voice surface 是否能稳定处理中文、多轮澄清和误触发。

## 参考资料

- GitHub 仓库：<https://github.com/xiaotianfotos/homerail>
- HomeRail 中文 README：<https://github.com/xiaotianfotos/homerail/blob/main/README.zh-CN.md>
- agent-chief：<https://github.com/SmileLikeYe/agent-chief>
- OpenTag：<https://github.com/linxidnju/OpenTag>
