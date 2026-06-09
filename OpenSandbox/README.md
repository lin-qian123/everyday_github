# OpenSandbox

- GitHub: https://github.com/alibaba/OpenSandbox
- 官方文档: https://open-sandbox.ai/
- 记录时间: 2026-03-05

## 这是什么
OpenSandbox 是阿里开源的通用 Sandbox 平台，核心目标是给 AI Agent 提供“可控、可隔离、可观测”的执行环境。它提供统一 API、跨语言 SDK，以及 Docker/Kubernetes 运行时，适用于代码执行、浏览器自动化、桌面 Agent、评测和训练等场景。

从 GitHub Trending（daily）可见，它在今日榜单前列，且单日星标增长明显。

## 为什么它最近热
- Agent 进入“要执行真实任务”的阶段后，必须解决执行隔离、网络权限、文件系统、安全审计问题。
- OpenSandbox 把这些能力做成标准化平台，降低了“每个团队重复造 sandbox”的成本。
- 官方示例覆盖 Claude Code、Codex CLI、Gemini CLI、Playwright、VNC Desktop 等，落地感很强。

## 怎么用（最小可跑）

### 1) 安装并初始化服务
```bash
uv pip install opensandbox-server
opensandbox-server init-config ~/.sandbox.toml --example docker
opensandbox-server
```

### 2) 安装 Code Interpreter SDK
```bash
uv pip install opensandbox-code-interpreter
```

### 3) 创建 sandbox 并执行命令（Python）
```python
import asyncio
from datetime import timedelta
from opensandbox import Sandbox

async def main():
    sandbox = await Sandbox.create(
        "opensandbox/code-interpreter:v1.0.1",
        entrypoint=["/opt/opensandbox/code-interpreter.sh"],
        timeout=timedelta(minutes=10),
    )
    async with sandbox:
        execution = await sandbox.commands.run("echo 'Hello OpenSandbox!'")
        print(execution.logs.stdout[0].text)
        await sandbox.kill()

asyncio.run(main())
```

## 原理（架构拆解）

### 1) 协议层：统一 Sandbox Protocol
OpenSandbox 定义了生命周期管理 API 和执行 API，把“创建实例、执行命令、文件读写、网络控制”抽象成统一接口。上层 Agent 不需要关心底层是 Docker 还是 Kubernetes。

### 2) 运行时层：Docker + Kubernetes 双栈
- 本地快速开发可走 Docker。
- 生产与高并发调度可走 Kubernetes（高性能 runtime）。

### 3) 能力层：命令/文件/代码解释器
默认内建命令执行、文件系统操作、代码解释器（Code Interpreter）等能力，方便 Agent 直接做“执行-读写-回传”闭环。

### 4) 网络层：Ingress + Egress 控制
- Ingress 网关统一接入策略。
- Egress 做每个 sandbox 的出网控制，限制数据外泄和越权访问。

## 典型场景
- Coding Agent 安全执行 PR 修复脚本。
- Browser Agent 在隔离浏览器中做抓取/测试。
- 多租户 AI 平台为每个任务分配独立运行空间。
- RL/评测环境复现可控执行轨迹。

## 与同类方案的差异（实用视角）
- 不只是“容器工具”，而是面向 Agent 的完整执行平台。
- SDK 和示例齐全，接入门槛低。
- 既支持本地，也支持大规模集群调度。

## 风险与注意事项
- 仍需做好镜像供应链安全和依赖审计。
- Egress 白名单策略要默认收紧，不要全开。
- 对“可执行用户代码”场景，需要叠加配额、审计日志与超时熔断。

## 参考
- https://github.com/alibaba/OpenSandbox
- https://open-sandbox.ai/
- https://raw.githubusercontent.com/alibaba/OpenSandbox/main/README.md
