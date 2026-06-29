# agency-agents（msitarzewski/agency-agents）

> GitHub: https://github.com/msitarzewski/agency-agents  
> 定位：把“多角色 AI 协作团队”做成可直接复用的 Agent 角色库（工程、设计、营销、产品、测试等）。

## 0. 2026-06-30 更新

`agency-agents` 在 2026-06-30 的 GitHub Trending daily 榜单中再次进入前排，GitHub API 抓取时约为 `118.8k stars / 19.4k forks`。项目已经从早期“Claude Code 角色文件集合”扩展到更明确的跨工具 agent roster：

- 新增原生桌面安装器 `agency-agents-app`，支持 macOS、Linux、Windows。
- 官方 README 说明可一键安装到 Claude Code、Cursor、Codex、Gemini CLI、OpenCode、Qwen、Osaurus、Hermes 等工具。
- 仓库提供 `scripts/convert.sh` 与 `scripts/install.sh`，可以按 tool、division、agent 子集生成和安装集成文件。
- 角色数量和 division 扩张后，项目价值不再只是“prompt 收藏”，而是越来越接近跨 agent harness 的角色分发层。

这也带来新的风险：角色越多，越需要对权限、工具边界、输出验收和上下文污染做治理；不能把“角色名字很专业”等同于“产出一定可靠”。

## 1. 项目是什么
`agency-agents` 本质是一个“AI 团队角色模板仓库”。它不是单一模型或单一 agent，而是把不同岗位的职责、语气、流程、交付标准，固化成可直接调用的 agent persona。

从仓库 README 看，项目核心主张是：
- 每个 agent 都是“专业角色”（不是通用 prompt）
- 每个角色都有可交付目标（deliverable-focused）
- 直接适配 Claude Code 的 `~/.claude/agents/` 工作流

在 2026-03-07 抓取快照中，仓库已到 `9.7k stars / 1.5k forks`（GitHub 页面可见），并在第三方趋势站点保持高位（Trendshift 显示约 `7k stars / 1.1k forks`，数据同步有延迟）。

## 2. 核心原理（为什么会火）

## 2.1 把“提示词”升级成“组织结构”
传统做法是给一个模型塞长 prompt；`agency-agents` 的做法是把组织分工显式化：
- Engineering Division（前端、后端、AI 工程、DevOps、原型）
- Design Division（UI、UX、品牌、视觉叙事）
- Marketing Division（内容、增长、Reddit/TikTok/Instagram 等）
- Product / PM / Testing 等

这样做的好处是：
- 任务边界更清晰，减少“一个 agent 做所有事”导致的漂移
- 输出风格可控（不同角色不同沟通与交付格式）
- 更适合团队协作时的责任拆分

## 2.2 角色文件 = 可执行 SOP
每个 agent 文件一般包含：
- 身份与语气
- 工作流程
- 输出模板/代码交付标准
- 成功指标（success metrics）

这相当于给 AI 加上一层“岗位 SOP”，比一次性 prompt 更稳定。

## 3. 怎么用（最小可跑）

## 3.1 快速接入桌面安装器

官方现在推荐通过 `agency-agents-app` 安装，它提供跨平台桌面界面，并把角色安装到多种 AI coding 工具：

```bash
brew install --cask msitarzewski/agency-agents/agency-agents
```

也可以从 release 页面下载：

```text
https://github.com/msitarzewski/agency-agents-app/releases/latest
```

## 3.2 快速接入 Claude Code
```bash
git clone https://github.com/msitarzewski/agency-agents.git
cd agency-agents
./scripts/install.sh --tool claude-code
```

然后在会话里按角色调用，例如：
- “activate Frontend Developer mode …”
- “switch to Growth Hacker …”

## 3.3 接入其他工具

仓库提供转换和安装脚本，可面向不同工具生成角色文件：

```bash
./scripts/convert.sh
./scripts/install.sh --tool codex
./scripts/install.sh --tool opencode --division engineering --dry-run
```

如果目标工具有角色数量限制，应优先按 division 或 agent 子集安装。

## 3.4 当作角色素材库使用
不直接复制到 `~/.claude/agents/` 也可以：
- 按任务选角色文件
- 抽取其流程与交付规范
- 合并到你自己的 agent/系统提示词

## 3.3 推荐实践
- 一次任务先固定 `1-2` 个主角色，避免多角色串话。
- 先让“产品/项目管理角色”定义验收标准，再让工程/设计角色执行。
- 用“测试角色”做最后验证，减少返工。

## 4. 适合场景
- 小团队：快速模拟“一个迷你数字团队”
- 内容团队：多平台内容生产（X、YouTube、Instagram、Reddit）
- 独立开发者：从需求拆解到实现、测试的一条龙执行
- AI 工作流实验：比较“单 agent vs 多角色 agent”产出差异

## 5. 局限与风险
- 角色越多，编排复杂度越高，成本与延迟会上升。
- Persona 质量不等于结果质量，仍依赖模型能力和上下文输入。
- 某些角色的行业假设可能不适配你的业务，需要二次改写。
- 若直接把营销/舆情角色用于外部发布，仍需人工审核合规与事实性。

## 6. 今天为什么值得跟进
- 热点从“单模型参数战”转向“可落地的团队协作流程”。
- `agency-agents` 的增长说明：大家更关注“如何把 AI 变成稳定生产力”，而不只是“跑分”。
- 对个人开发者来说，它提供了一个低成本验证“AI 组织化协作”的现成样板。

## 7. 参考链接
- GitHub Repo: https://github.com/msitarzewski/agency-agents
- Agency Agents App Repo: https://github.com/msitarzewski/agency-agents-app
- Agency Agents App Release: https://github.com/msitarzewski/agency-agents-app/releases/latest
- Trendshift（趋势快照）: https://trendshift.io/repositories/22315
- GitHub Trending 频道转发（样例）: https://t.me/s/githubtrending/15530
