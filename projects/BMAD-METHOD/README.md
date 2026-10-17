<!-- markdownlint-disable MD013 -->

# BMad Method（bmad-code-org/BMAD-METHOD）中文解读

> 上游仓库：<https://github.com/bmad-code-org/BMAD-METHOD> · 归类：Agent 框架与技能生态 · 证据快照：2026-10-18（Asia/Shanghai）。认证 API：54,269 stars / 6,098 forks / 61 open issues；稳定 Release `v6.12.4`；main 为 v7 preview alpha；LICENSE 为 MIT 附商标说明，API SPDX 为 `NOASSERTION`。本页为上游材料及所列源码的静态整理，未安装运行、复测 benchmark 或完成全面安全审计。

## 定位

BMad 把需求澄清、产品 / 架构设计、实现、评审和复盘组织为可安装的 Agent 工作流。它提供显式决策与可续接项目上下文，适合已有代码维护和较复杂需求；方法执行依赖宿主 coding agent，不能把流程覆盖率直接等同于软件质量。

## 用法

先选版本线。README 的稳定路径是 `npx bmad-method install`，要求 Node.js 20.12+、Python 3.10+，且两条路径均需 uv；v6.12 文档在独立分支。v7 预览通过 `npx skills add bmad-code-org/BMAD-METHOD` 或上游插件市场安装，随后执行 `bmad setup` 再调用 `bmad-build`。先在项目副本评估一项小变更，记录安装源与版本；本轮没有执行这些命令。

## 原理

工作流以技能、模块与项目上下文共同驱动。main 的 `bmad-build/SKILL.md` 先调用项目 `_bmad/scripts/render_skill.py` 渲染实际工作流，支持 route 与 review 选择；不是读取一个固定提示词就能完整复现。分析、架构、开发等角色提供不同视角，决策和产物继续进入后续阶段。

## 价值

可把隐含假设变成可评审的 brief、规格、架构与验收记录。README 允许小变更直达构建，复杂任务再加深规划，适合按风险调整流程。价值应以遗漏需求、返工时间、验收缺陷与上下文恢复成本衡量，不能用角色数量或生成文档数量替代结果。

## 风险边界

- **稳定版与预览分开**：README 仍称 main 为 preview alpha，虽写过 2026-10-16 的预计 v7 发布日，也不能以日期已过认定正式发布；API 最新稳定 Release 仍是 v6.12.4。
- SECURITY 明确安装模块相当于执行其代码；Markdown 指令会影响 Agent 行为，权限隔离取决于宿主、工具和操作系统配置。渲染脚本 / 插件 / 更新器均属于供应链。
- 源码、需求和生成物可能进入宿主所用模型服务；多角色讨论会扩大成本和上下文暴露面，不保证独立纠错。
- LICENSE 的 MIT 文本包含额外商标说明；API 未识别 SPDX，不宜只根据 badge 或 API 字段概括全部条款。

## 补充建议

用固定版本完成“增加一个可验收功能”的小任务，保存输入、规格、差异、测试与评审意见；和原有流程比较工时与缺陷。v6 与 v7 分开测试，升级前记录项目配置和生成文件变化；先核清 workflow 渲染失败及更新失败时的恢复办法。

## 参考资料

- 上游仓库：<https://github.com/bmad-code-org/BMAD-METHOD>
- GitHub REST API：<https://api.github.com/repos/bmad-code-org/BMAD-METHOD>
- README / 双版本安装：<https://github.com/bmad-code-org/BMAD-METHOD/blob/main/README.md>
- 稳定分支：<https://github.com/bmad-code-org/BMAD-METHOD/tree/V6.12>
- 稳定 Release：<https://github.com/bmad-code-org/BMAD-METHOD/releases/tag/v6.12.4>
- 构建技能入口：<https://github.com/bmad-code-org/BMAD-METHOD/blob/main/skills/bmad-build/SKILL.md>
- 安全模型：<https://github.com/bmad-code-org/BMAD-METHOD/blob/main/SECURITY.md>
- 许可与商标说明：<https://github.com/bmad-code-org/BMAD-METHOD/blob/main/LICENSE>
