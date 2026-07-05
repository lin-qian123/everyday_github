# tupper

## 1. 定位

`tupper` 是一个面向 AI agents 的本地开源 sandbox 项目，目标是在用户自己的机器上
运行不可信或 AI 生成的代码，同时提供接近 E2B 的 TypeScript SDK 体验。它当前重点
支持 macOS 上的 Apple Containers，并规划 Linux Firecracker 与 Windows WSL 后端。

它适合归入 `Agent 框架与技能生态`，因为 sandbox 已经成为 coding agent、code
interpreter、MCP 工具和本地自动化的基础设施问题。

## 2. 基本用法

Node 或 Bun 项目中可安装 SDK 与后端：

```bash
npm install @tupper/sdk @tupper/container
```

基本调用方式：

```ts
import { Sandbox } from "@tupper/sdk";

const box = await Sandbox.create({ image: "docker.io/library/alpine:latest" });
try {
  await box.files.write("/tmp/hi.txt", "hello");
  const res = await box.commands.run("cat /tmp/hi.txt");
  console.log(res.stdout);
} finally {
  await box.kill();
}
```

项目还提供 CLI、HTTP API、MCP server，以及 deepagents / Mastra 的集成包。

## 3. 核心原理

Tupper 的核心是 backend-agnostic sandbox abstraction：

- `@tupper/core` 定义抽象、类型、schema 和后端解析。
- `@tupper/container` 接 Apple Containers，作为 macOS 后端。
- `@tupper/firecracker` 面向 Linux microVM，仍处实验阶段。
- `@tupper/sdk` 提供 E2B-style `Sandbox` facade。
- `@tupper/mcp` 把 sandbox 能力暴露给 MCP client。

它将不同平台的隔离方式隐藏在同一 API 后面，让 agent framework 可以把“运行命令、
写文件、读结果”视为统一能力。

## 4. 工程价值

agent 执行代码时最危险的部分不是 LLM 推理，而是 shell、文件系统、网络和凭据。
Tupper 把这一层独立出来，给本地 agent 提供更可控的执行边界。

与托管 sandbox 相比，本地 sandbox 的优势是数据不必离开机器，延迟和成本也更可控。
代价是平台能力、镜像管理、资源限制和安全补丁都需要用户或团队自己承担。

## 5. 风险边界

项目仍处早期，README 明确提示 API 可能在 1.0 前变化。当前 macOS 默认依赖 Apple
Containers 和 macOS 26+，实际可用性受系统版本限制。

本地 sandbox 也不是万能隔离。使用者仍需配置网络访问、挂载目录、资源限制、镜像来源
和日志清理策略，不能把它当作可以安全运行任意恶意代码的完整防线。

## 6. 补充建议

- 从最小镜像和只读输入开始，逐步开放文件与网络能力。
- 将 Tupper 接入 MCP 前先为每个工具定义清晰的命令白名单和资源上限。
- 对比 E2B、Daytona、Modal、OpenSandbox，区分本地隔离、托管隔离和浏览器/WASM
  隔离的适用边界。
- 持续观察 Firecracker / WSL 后端是否落地，决定它能否成为跨平台 agent sandbox。

## 7. 参考资料

- GitHub 仓库：<https://github.com/lightbearco/tupper>
- npm 包：`@tupper/sdk`、`@tupper/container`、`@tupper/mcp`
- 许可证：MIT
