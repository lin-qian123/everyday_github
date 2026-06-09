# harness

## 项目定位
harness 是一个“元技能（meta-skill）”项目：先分析业务域，再自动设计 Agent 团队结构，并生成对应技能与协作编排。

- GitHub: https://github.com/revfactory/harness

## 用法

### 1. 通过插件市场安装
```bash
/plugin marketplace add revfactory/harness
/plugin install harness@harness-marketplace
```

### 2. 作为全局技能安装
```bash
cp -r skills/harness ~/.claude/skills/harness
```

### 3. 按流程执行
- Domain Analysis（领域分析）
- Team Architecture Design（团队/子代理架构）
- Agent Definition Generation
- Skill Generation
- Integration & Orchestration
- Validation & Testing

## 原理
- 将“任务分解”前置为结构化步骤，先定义角色边界，再生成技能与执行链路。
- 把传统人工搭 Agent 流程转为可重复模板，降低复杂多代理系统的设计门槛。

## 价值
- 适合复杂任务（研发、分析、运营）中的多角色协同。
- 让团队从“Prompt 手工拼接”转向“架构化代理设计”。
- 有助于形成可迁移的 Agent 组织知识。

## 风险边界
- 自动生成的团队结构不一定贴合真实组织流程，仍需人工校准。
- 过度依赖模板可能导致场景适配不足。
- 需要明确“何时使用子代理、何时直接执行”的成本边界。

## 补充建议
- 先选一个业务流程做小规模试点，验证拆分质量再推广。
- 记录每轮生成后的人工作业修改点，沉淀为本地规则。
- 建立最小化评估指标：正确率、响应时间、维护成本。

## 参考资料
- GitHub Trending（2026-05-29）: https://github.com/trending
- 仓库 README: https://github.com/revfactory/harness
