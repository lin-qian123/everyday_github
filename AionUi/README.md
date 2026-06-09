# AionUi（iOfficeAI/AionUi）项目速览与上手指南

- GitHub: https://github.com/iOfficeAI/AionUi
- 更新日期: 2026-03-30（Asia/Shanghai）

## 1. 为什么今天值得跟踪

`AionUi` 是一个把主流 Agent CLI（Gemini CLI、Claude Code、Codex、Qwen Code 等）统一到图形化界面的开源工具，近期持续出现在 GitHub Trending 讨论中，属于“AI 编程工作台”这一高热赛道。

- 热度信号（抓取快照）:
  - GitHub 仓库页快照: `2.9k stars`、`220 forks`
  - zdoc Trending 快照（同类赛道）显示 AI Agent / 协作类项目持续高增星（如 `deer-flow` 单日 `2,394 stars today`）

## 2. 项目在做什么（核心定位）

官方定位是：把命令行 AI 助手升级为可视化、多会话、多模型、多 Agent 的“本地优先”工作台。

核心能力：

1. 多 Agent / 多模型统一入口
- 一套界面接入 Gemini CLI、Claude Code、Codex、Qwen Code 等。
- 适合把“不同模型做不同任务”的工作流落地。

2. 本地优先 + WebUI 远程访问
- 本机运行，数据尽量留在本地。
- 提供 WebUI 场景，便于跨设备访问。

3. 多会话并行与上下文隔离
- 支持多任务并行对话，减少单线程切换成本。

4. 扩展到办公与文件处理
- README 明确强调文件整理、表格辅助、图像生成/编辑等工作流入口。

## 3. 怎么用（快速上手）

## 3.1 普通用户安装

1. 打开 Releases 页面下载对应系统安装包：
- https://github.com/iOfficeAI/AionUi/releases

2. 安装后配置模型供应方式：
- 登录方式（例如 Gemini 账号）或
- API Key 方式（OpenAI/Anthropic/其他聚合服务）

3. 启动并创建会话：
- 建议先建 2-3 个固定会话（编码、文档、检索），观察上下文隔离效果。

## 3.2 开发者本地开发

```bash
git clone https://github.com/iOfficeAI/AionUi.git
cd AionUi
npm install
npm start
```

可选端口覆盖（README 给出的环境变量）：

```bash
AIONUI_DEV_PORT=3100 \
AIONUI_LOGGER_PORT=9100 \
npm start
```

## 4. 原理是什么（工程视角）

`AionUi` 的实质不是“再造一个模型”，而是一个“调度与交互层”：

1. Agent 抽象层
- 把不同 CLI Agent 统一成可视会话与操作面板，降低切换成本。

2. 会话状态层
- 多会话的上下文独立管理，避免任务互相污染。

3. 模型路由层
- 同一任务链可按子任务路由到不同模型（例如：检索/推理/代码分工）。

4. 本地运行与远程访问并存
- 兼顾隐私（本地）与可达性（WebUI）。

## 5. 适用场景

- 希望把“终端里的 Agent”变成可管理的团队工作台。
- 需要对比多个模型/Agent 在同一任务上的表现。
- 想搭建长期运行的个人 AI 协作环境（研发、文档、运营混合场景）。

## 6. 风险与边界

1. 聚合并不等于质量保证
- UI 统一后，输出质量仍由底层模型和提示工程决定。

2. 成本与配额复杂度上升
- 多模型并行会显著增加 Token 预算管理难度。

3. 安全治理需前置
- 建议将 API Key、MCP 工具权限、文件系统访问权限做最小化配置。

## 7. 信息来源

- GitHub 仓库（功能、快速开始、发布信息）:
  - https://github.com/iOfficeAI/AionUi
- GitHub Trending 快照（AI 项目单日增星）:
  - https://www.zdoc.app/en/trending
- AIToolly 对 Trending 事件转述（AionUi 上榜背景）:
  - https://aitoolly.com/ai-news/article/2026-02-11-aionui-free-local-open-source-247-collaborative-office-and-openclaw-for-gemini-cli-claude-code-and-m
