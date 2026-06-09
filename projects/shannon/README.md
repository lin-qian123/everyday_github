# Shannon（KeygraphHQ/shannon）

> GitHub: https://github.com/KeygraphHQ/shannon  
> 定位：用于 Web 应用与 API 的自治式白盒 AI 渗透测试工具（Shannon Lite）

## 1. 项目是什么
Shannon 是 Keygraph 开源的 AI 渗透测试框架。它不是只做静态规则匹配的扫描器，而是会结合源码理解 + 动态攻击执行，最终只输出“可复现 PoC”的漏洞结论。

根据仓库说明，Shannon Lite 在 hint-free、source-aware 变体的 XBOW benchmark 上达到 `96.15%（100/104 exploits）` 的结果，并且支持在一次命令中自动完成登录、探测、攻击验证、报告生成。

## 2. 核心原理（它为什么和传统扫描器不同）
Shannon 的工作流本质是“代码感知驱动的动态验证”：

1. 读取目标项目源码（白盒前提）。
2. 基于代码结构定位潜在攻击面（输入源、鉴权边界、敏感调用等）。
3. 通过浏览器自动化与命令行安全工具执行真实攻击尝试。
4. 仅保留可被真实利用的漏洞，并附上可复现 PoC。

官方特性中明确提到其会覆盖 Injection、XSS、SSRF、鉴权问题，并整合 Nmap、Subfinder、WhatWeb、Schemathesis 等工具进行侦察与验证。

## 3. 快速使用

### 3.1 前置条件
- 你有可测试目标的授权（必须合法授权）。
- 目标项目源码可访问（Shannon Lite 是白盒模式）。
- 本机具备 Docker/容器运行环境（项目默认容器化流程）。
- 已配置模型凭据（如 `ANTHROPIC_API_KEY` 或 `CLAUDE_CODE_OAUTH_TOKEN`）。

### 3.2 最小可跑流程
```bash
git clone https://github.com/KeygraphHQ/shannon.git
cd shannon

# 任选一种方式提供凭据
export ANTHROPIC_API_KEY="your-api-key"
export CLAUDE_CODE_MAX_OUTPUT_TOKENS=64000

# 将被测仓库放在 repos 目录下
# 例如：git clone https://github.com/your-org/your-repo.git ./repos/your-repo

# 启动一次测试
./shannon start URL=https://your-app.com REPO=your-repo
```

### 3.3 运行中常用命令
```bash
# 实时日志
./shannon logs

# 查询某次工作流进度
./shannon query ID=shannon-1234567890

# 停止（保留数据）
./shannon stop

# 全清理
./shannon stop CLEAN=true
```

### 3.4 断点续跑（Workspace）
Shannon 支持使用 `WORKSPACE=` 复用先前任务状态，跳过已完成阶段，适合长时扫描或失败后恢复。

## 4. 适用场景
- CI/CD 前的高频安全闸门（替代“年检式”渗透测试空窗期）。
- 安全团队做漏洞 PoC 快速确认，减少误报 triage 成本。
- 研发团队自测 API 与 Web 业务逻辑的可利用风险。

## 5. 边界与风险
- `仅白盒`：没有源码时，Shannon Lite 能力受限。
- `必须授权`：任何越权渗透测试都可能违法。
- `自动攻击工具`：需在隔离环境、最小权限、审计留痕下使用。
- `结果仍需复核`：PoC 有效不代表风险分级、业务影响评估可完全自动化。

## 6. 今天为什么值得关注
在 2026-03-06 抓取的 GitHub Trending（日榜）中，`KeygraphHQ/shannon` 位居前排，显示 `31k+` 总 stars、`1.8k+ stars today`（抓取快照）。

这反映了两个趋势：
- AI Agent 正从“写代码”向“攻防验证”迁移。
- 安全工具的评估标准从“发现疑似问题”转向“能否给出可复现利用链”。

## 7. 参考链接
- GitHub Repo: https://github.com/KeygraphHQ/shannon
- GitHub Trending: https://github.com/trending
- Keygraph 官网: https://keygraph.io
