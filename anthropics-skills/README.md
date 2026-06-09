# anthropics/skills

## 项目简介
anthropics/skills 是一个面向 AI 开发者与应用团队的 “Agent Skills” 工具库与协议示例仓库。它希望把“可复用的工具能力”以统一结构沉淀下来（技能/skill），让不同应用、IDE 或 agent 运行时可以复用同一套能力定义，减少重复集成成本。仓库包含技能结构约定、示例技能与脚本（例如 `skills.sh`），并指向 skills marketplace（SkillHub）与 Agent Skills 标准。citeturn1view0turn1search3

## 为什么值得关注
- 出现在 GitHub 日榜/热度榜单（2/26 日榜分析中进入前列），热度和传播速度快。citeturn1search1
- Agent 能力复用是 2026 年趋势之一：从“单点工具集成”转向“跨应用共享能力”。citeturn1view0turn1search3

## 核心理念（它解决什么问题）
1. **能力标准化**：用统一协议描述技能，便于跨工具共享。citeturn1view0turn1search3
2. **渐进式引导**：技能文档强调“逐步展开”的说明方式，让使用门槛更低。citeturn1search3
3. **可分发/可市场化**：通过 SkillHub 进行发布与安装，降低分发成本。citeturn1view0

## 主要内容
- **技能协议与结构**：技能以目录形式组织，强调可发现性与可执行性。citeturn1view0
- **示例技能**：仓库内提供示例技能，便于模仿与扩展。citeturn1view0
- **安装与运行脚本**：提供 `skills.sh` 等工具用于安装与运行技能。citeturn1view0
- **技能市场入口**：与 SkillHub 连接，支持技能分发与安装。citeturn1view0

## 基本原理（工作流视角）
1. **定义技能**：为每个技能写清描述、用途、输入输出与执行方式。
2. **打包与发布**：遵循技能结构标准，推送到技能市场或共享仓库。citeturn1view0turn1search3
3. **安装与调用**：在支持 Agent Skills 的环境（如 Claude Code）中安装技能，并在会话中调用。citeturn1view0

## 快速上手
### 方式一：使用 Claude Code 的插件市场安装（推荐）
```bash
# 在 Claude Code 中安装技能市场
/plugin marketplace add

# 安装本地仓库中的示例技能
/plugin install /path/to/skills
```
citeturn1view0

### 方式二：使用仓库脚本运行示例技能
```bash
./skills.sh
```
citeturn1view0

## 适用场景
- 团队内部共用一套“工具能力”清单（抓取、结构化解析、代码审查等）。
- 构建 IDE/终端内的 agent 插件生态，快速扩展功能。
- 将成熟能力打包成可分发组件，降低复用成本。

## 参考链接
- GitHub: https://github.com/anthropics/skills
- Agent Skills 标准与说明: https://www.agentskills.io
- SkillHub: https://skillhub.ai
