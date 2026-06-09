# Claude Code（anthropics/claude-code）

- GitHub: https://github.com/anthropics/claude-code
- 官方站点: https://code.claude.com/
- 更新日期: 2026-05-31（Asia/Shanghai）

## 定位

`Claude Code` 是 Anthropic 的终端型 Agent 编码工具，核心定位是让开发者通过自然语言在本地仓库中完成多步工程任务（理解代码、修改文件、解释逻辑、协助 git 流程）。

## 用法

### 1) 安装（官方常用路径）

```bash
# macOS / Linux
curl -fsSL https://claude.ai/install.sh | bash

# Homebrew
brew install --cask claude-code
```

Windows 常见路径：

```powershell
irm https://claude.ai/install.ps1 | iex
# 或
winget install Anthropic.ClaudeCode
```

### 2) 在项目中使用

```bash
cd your-project
claude
```

建议在有测试门禁（lint/typecheck/test）的仓库中使用，降低自动改动风险。

## 原理（工程视角）

1. Agent 闭环：围绕“目标 -> 计划 -> 执行 -> 反馈”进行多轮任务推进，而非单轮问答。
2. 仓库上下文：在终端直接读取工程上下文，支持跨文件修改与重构。
3. 工具协同：把代码解释、文件修改和版本协作动作放进同一工作流。

## 价值

- 提升中大型代码库中的排障与增量改动效率。
- 降低重复性工程动作成本（脚手架、批量改动、重构辅助）。
- 对“人机协同开发”场景具有较高实用性。

## 风险边界

- 自动修改能力越强，误改与越权风险越高。
- 若缺少测试与审查门禁，错误可能更快扩散。
- 涉及企业代码时，应先明确数据与合规边界。

## 补充建议

1. 关键改动默认采用“先计划、后执行”。
2. 变更前后固定运行 `lint/typecheck/test`。
3. 对批量删除、迁移脚本等高风险操作设置人工确认。

## 参考资料

- https://github.com/anthropics/claude-code
- https://code.claude.com/
- https://github.com/trending
