# gemini-cli（google-gemini/gemini-cli）

- GitHub: https://github.com/google-gemini/gemini-cli
- 记录日期: 2026-04-26 (Asia/Shanghai)

## 这是什么

`gemini-cli` 是 Google 开源的终端 AI Agent。它把模型能力直接带到命令行，内置文件操作、Shell、网页抓取与搜索增强，同时支持 MCP 扩展，定位是“终端优先的可执行助手”。

## 热度信号

1. OSSInsight AI Trending Top 50（2026-04-26 抓取）中位列第 15，约 `54,014 stars`，近 28 天增长 `+688`。
2. GitHub 仓库抓取快照显示 `13.2k forks`、`2.4k issues`、`502 PRs`，处于高活跃迭代区间。

## 怎么用（最短路径）

### 1) 直接运行

```bash
npx @google/gemini-cli
```

### 2) 全局安装

```bash
npm install -g @google/gemini-cli
# 或
brew install gemini-cli
```

### 3) 先跑一个安全最小任务

1. 仅在测试目录执行只读分析。
2. 再开启文件编辑能力。
3. 最后按需接入 MCP 工具。

## 核心原理

1. 终端执行回路：用户指令 -> 计划 -> 工具调用 -> 结果反馈。
2. 工具化扩展：内置工具 + MCP 组合，扩展外部系统访问能力。
3. 长上下文协作：利用大上下文窗口维持项目级上下文连续性。

## 适用场景

1. 代码库巡检、批量重构、脚本化开发任务。
2. 需要“命令行自动化 + LLM 推理”一体化的工程团队。
3. 希望在 CI 或半自动流程中引入 Agent 能力。

## 价值与风险

价值：
- 终端路径短，适合高频工程动作。
- 支持 MCP 后可快速接入团队现有工具链。

风险：
- 工具权限配置不当会放大误操作范围。
- 在不可信仓库执行自动命令存在供应链风险。

## 我认为有价值的补充材料

1. 默认采用 `read-only` profile，逐步放开写权限。
2. 对写操作增加审批闸门（尤其是 Git 与生产环境命令）。
3. 为常用任务建立模板提示词与回滚脚本，提升稳定性。

## 参考来源

- https://github.com/google-gemini/gemini-cli
- https://google-gemini.github.io/gemini-cli/
- https://ossinsight.io/trending/ai
