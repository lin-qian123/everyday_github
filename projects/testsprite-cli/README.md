# testsprite-cli

## 1. 项目定位

`testsprite-cli` 是 TestSprite 官方 CLI，定位为 agentic coding 时代的验证层。它让 coding agent 通过终端创建、运行、复盘前端或后端测试，并把失败截图、DOM 线索、步骤和结果打包成 agent 可以直接读取的失败 bundle。

它不是单纯的测试运行器，而是把测试平台能力封装成可被 Claude Code、Codex、Cursor、Cline、Antigravity 等 coding agent 调用的验证循环。

## 2. 基本用法

项目要求 Node.js 20 及以上，官方 README 给出的入口是：

```bash
npm install -g @testsprite/testsprite-cli
testsprite setup
```

`testsprite setup` 会配置 API key、验证认证状态，并为指定 coding agent 安装验证 skill。CI 或批量初始化可使用环境变量和非交互参数：

```bash
TESTSPRITE_API_KEY=sk-... testsprite setup --from-env --yes --agent claude
```

典型 agent 循环是：创建测试并运行，拉取失败 bundle，修复代码，再重跑测试。

## 3. 核心原理

`testsprite-cli` 的重点是把“测试失败”整理成 agent 可消费的结构化输入，而不是只给人类一个 dashboard。

- `test create` / `test create-batch` 创建测试计划。
- `test run` / `test rerun` 触发执行并可等待终态。
- `test failure get` 下载单个自洽失败 bundle，包含定位、截图、步骤、DOM 线索和运行信息。
- `agent install` 把验证能力接入本地 coding agent。
- CLI 同时覆盖 project、test、result、artifact、auth 等命令，适合人类和 agent 共用。

## 4. 工程价值

近期 coding agent 的主要短板不是“能不能生成代码”，而是“能不能稳定证明改动真的工作”。`testsprite-cli` 把验证循环显式接入 agent 工作流，有助于减少模型自信但未验证的提交。

对团队而言，它提供了一条更可审计的路径：需求描述、测试计划、执行结果、失败 bundle、修复记录和重跑结果都可以沉淀下来，而不是只保留聊天记录。

## 5. 风险边界

- CLI 依赖 TestSprite 平台和 API key，不是完全离线工具。
- 自动生成测试仍可能遗漏业务关键路径，需要和人工验收标准、现有单测/E2E 测试结合。
- 失败 bundle 能帮助 agent 修复问题，但也可能包含页面内容、DOM、截图或业务数据，应注意敏感信息边界。
- 把 agent 接进测试平台前，应明确测试环境、账号权限、数据隔离和费用控制。

## 6. 补充建议

- 在已有 Playwright/Cypress 流程外先做旁路验证，不要立即替换成熟 CI。
- 对 agent 使用时，强制要求失败后读取 bundle，再修改代码，再重跑同一测试。
- 关注它和 `awesome-harness-engineering`、`ponytail`、`guard-skills` 这类“验证/质量门”项目的分工。
- 适合放入本仓库的 `Agent 框架与技能生态` 分类，因为它的核心价值是给 coding agent 增加可执行验证能力。

## 7. 参考资料

- GitHub 仓库：https://github.com/TestSprite/testsprite-cli
- 官方网站：https://www.testsprite.com
- CLI 文档：https://docs.testsprite.com/cli/getting-started/overview
- npm 包：`@testsprite/testsprite-cli`

