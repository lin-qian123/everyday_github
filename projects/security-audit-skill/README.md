<!-- markdownlint-disable MD013 -->

# security-audit-skill（Cloudflare 审计技能）

- 更新：2026-11-07（Asia/Shanghai）；官方 综合 daily +2,524，为读取快照，不是自然日结算。
- GitHub API：63,885 stars / 4,140 forks / 115 open issues（含 PR）；仓库 ID `1273427276`。
- 核读基线：`c1c8a8c1471069fb0e188eeaff69b8e8db6564a8`；仅文档与抽样实现核验，未安装运行或独立评测。

## 定位

这是让支持工具与子 Agent 的 coding agent 执行代码安全审阅的技能包。当前模式区分普通安全问答 / 聚焦审阅的 guidance，与明确要求完整代码审计 / 渗透测试或报告产物的 full audit；加载技能不代表获得执行完整审计或新建文件的授权。本页仅研究上游设计，未将其作为本仓库审计指令执行。[README](https://github.com/cloudflare/security-audit-skill/blob/c1c8a8c1471069fb0e188eeaff69b8e8db6564a8/README.md)、[技能定义](https://github.com/cloudflare/security-audit-skill/blob/c1c8a8c1471069fb0e188eeaff69b8e8db6564a8/skills/security-audit/SKILL.md)

## 用法

无 GitHub Release，需按固定源码使用；根代码为 MIT。上游安装示例为：

```bash
npx skills add https://github.com/cloudflare/security-audit-skill \
  --skill security-audit
```

安装后，明确目标仓库、源码版本、范围和输出位置。完整模式默认输出到目标仓库外的 `~/security-audit-skill/<repo>/run-<N>`，仅在用户显式指定且确认被版本控制忽略时写入目标内。需支持工具 / 子 Agent 的模型及 Node.js；本轮没有安装、启动审计或运行上游校验器。

## 原理

当前六阶段顺序为：

1. 侦察：形成 architecture.md 与 coverage-ledger.json，标出边界、输入面和覆盖单元。
2. 按覆盖账本寻找候选，并以 coverage critic 查遗漏。
3. 独立验证每个候选，尝试推翻源路径、前提和影响。
4. 写 confirmed / needs_validation / rejected 三态 findings.json，执行结构与语义校验。
5. 独立核对最终记录；重要替换还需再次独立核验。
6. 从已核记录和覆盖账本生成 REPORT、详细发现和待验证报告。

这修正旧页将报告先于结构化 / 最终复核的次序。重复运行会重核当前源码与历史记录，不把旧 same-source、未解决或范围外工作自动视作本轮已覆盖。quick / standard / deep 改变广度与冗余，不降低证据门槛。[验证与报告](https://github.com/cloudflare/security-audit-skill/blob/c1c8a8c1471069fb0e188eeaff69b8e8db6564a8/skills/security-audit/VALIDATION-AND-REPORTING.md)

## 价值

将安全发现的来源、当前版本、被推翻理由、待验证事实和覆盖缺口留下可追溯记录。它的工程价值在于更严格的记录契约和复核分工，不是已被独立证明的漏洞发现率或“没有遗漏”保证。

## 风险边界

- full audit 要求对目标控制的构建 / 测试 / fixture 使用 OS 强制 sandbox：禁外网、空环境 allowlist、目标与工具只读、仅 scratch 可写、资源和时限受控。做不到时应保留具体 needs_validation，不执行目标代码；提示词本身不会创建 sandbox。
- confirmed 需完整来源链与有限观察结果；needs_validation 必须写精确阻塞且不带 severity；rejected 保留被证伪原因。未完成候选验证也不能为了收尾塞成 needs_validation。
- 抽样 validate-findings.cjs 检查 schema、字段、路径 / 记录约束和语义一致性；填写 observed_result 能通过结构门，不证明实际观察为真，更不等同漏洞复现或部署安全。
- 并行、覆盖 critic 和验证会消耗 token / 时间；strict budget 不足时需缩小范围或报告不完整。普通提示词工作流无法自动保证所有执行器遵循这些门控。
- 报告、轨迹和附件可能含私有源码或漏洞细节，输出可见性与保留期限需单独管理。[校验器](https://github.com/cloudflare/security-audit-skill/blob/c1c8a8c1471069fb0e188eeaff69b8e8db6564a8/skills/security-audit/validate-findings.cjs)、[三态 schema](https://github.com/cloudflare/security-audit-skill/blob/c1c8a8c1471069fb0e188eeaff69b8e8db6564a8/skills/security-audit/report-schema.json)

## 补充建议

在明确授权的可丢弃样本上检查三态记录、候选被拒、预算耗尽与复跑源码变化；逐项确认真实 sandbox，而非只检查说明文本。把最终引用、有限本地观察和人工复核作为独立验收项，保留未覆盖单元。需要动态证明时先给出最小安全实验计划；本次更新没有执行漏洞挖掘或攻击测试。

## 参考资料

- [仓库](https://github.com/cloudflare/security-audit-skill)、[发行列表（本轮为空）](https://github.com/cloudflare/security-audit-skill/releases)。
- [README](https://github.com/cloudflare/security-audit-skill/blob/c1c8a8c1471069fb0e188eeaff69b8e8db6564a8/README.md)、[MIT 许可](https://github.com/cloudflare/security-audit-skill/blob/c1c8a8c1471069fb0e188eeaff69b8e8db6564a8/LICENSE)、[模式 / sandbox / 覆盖 / 预算](https://github.com/cloudflare/security-audit-skill/blob/c1c8a8c1471069fb0e188eeaff69b8e8db6564a8/skills/security-audit/SKILL.md)。
- [验证和输出](https://github.com/cloudflare/security-audit-skill/blob/c1c8a8c1471069fb0e188eeaff69b8e8db6564a8/skills/security-audit/VALIDATION-AND-REPORTING.md)、[结构校验器](https://github.com/cloudflare/security-audit-skill/blob/c1c8a8c1471069fb0e188eeaff69b8e8db6564a8/skills/security-audit/validate-findings.cjs)、[schema](https://github.com/cloudflare/security-audit-skill/blob/c1c8a8c1471069fb0e188eeaff69b8e8db6564a8/skills/security-audit/report-schema.json)。
