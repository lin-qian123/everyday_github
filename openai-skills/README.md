# openai/skills

## 项目简介
`openai/skills` 是 OpenAI 官方维护的 Codex Skills 示例与技能仓库。Skills（技能）是一组可复用的指令、脚本与资源，帮助 Codex 在特定任务上稳定地产生更高质量的结果，并可作为团队或个人的工作流模板进行共享与迭代。官方在 Codex App 中强调“Skills + Agents”的模式，用技能封装可靠的执行步骤，交给模型按需调用与组合。项目在 GitHub Trending 上排名靠前，反映出开发者对“可复用 AI 工作流”的强烈关注与需求。

## 适合解决什么问题
- **把一次性的提示工程沉淀为可复用技能**：将“如何做”的步骤固化成说明、脚本与资源。
- **提高 AI 产出稳定性**：对任务过程做约束，减少随机性。
- **团队协作**：将共识流程变成技能库，统一风格与质量。

## 工作原理（概念层面）
- **技能=指令+脚本+资源**：Skills 通常以一个目录存在，目录内包含一份清晰的说明文档（SKILL.md），以及可选脚本与资源文件；模型在执行时会读取说明并在需要时调用脚本或资源。
- **Codex 的技能调用机制**：在 Codex App 中，你可以创建/管理 Skills，并在对话中显式要求使用某个技能，也可以让模型在合适时自动调用技能完成任务。
- **可组合与可扩展**：多个技能可以组合使用；随着团队实践积累，技能库会成为“AI 工作标准化”的中心资产。

## 快速上手（怎么用）
1. **安装/获取技能库**
   - 官方仓库提供“可安装技能”，可以用技能安装器同步到本地。
   - 在仓库根目录执行（需先安装 `uv`）：  
     ```bash
     cd skills
     uv run scripts/skill_installer.py
     ```
   - 如需安装实验性技能：  
     ```bash
     uv run scripts/skill_installer.py --experimental
     ```
2. **在 Codex App 中启用与使用**
   - 在 Codex App 的 Skills 管理界面中添加技能目录。
   - 在对话中提示“使用某某技能完成任务”，让 Codex 按技能指令执行。
3. **自己编写技能**
   - 以一个文件夹为单位，写清楚该技能的目标、限制、工作流与可选脚本。
   - 随着实际项目推进，迭代说明与脚本。

## 目录结构示例（概念）
- `skill-name/`
- `SKILL.md`：说明文档（目标、触发条件、操作步骤、工具约束）
- `scripts/`：必要的自动化脚本
- `assets/` 或 `references/`：示例、模板或参考资料

## 参考链接
- openai/skills 仓库（Skills 示例与安装说明）：https://github.com/openai/skills
- Codex App 介绍（Skills 的产品定位与作用）：https://openai.com/index/introducing-codex-app/
