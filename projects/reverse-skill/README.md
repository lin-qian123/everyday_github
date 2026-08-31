<!-- markdownlint-disable MD013 MD034 -->

# reverse-skill：面向授权安全任务的 AI 技能路由包

## 项目概览

- 上游仓库：https://github.com/zhaoxuya520/reverse-skill
- GitHub API 快照（2026-09-01）：33,077 stars、4,489 forks、19 个开放 issue
- 当前 release：`v1.0.1`
- 主要形态：PowerShell / Bash 路由脚本、Agent Skills、场景 playbook、证据日志
- 许可证：MIT

## 定位

reverse-skill 为 Claude Code、Codex、Cursor、Cline 等客户端提供逆向工程、CTF、取证和授权渗透测试的技能路由。它试图先判断 APK、ELF、前端 JS、PCAP 等任务类型，再选择方法、工具和记录格式，避免 agent 直接猜命令。

## 用法

上游建议让兼容客户端先读取 `README_AI.md`，再通过 `MASTER-ROUTING.md` 或 `master-route.ps1` 进入场景。典型链路是：

```text
用户任务
  -> 规则与主路由
  -> case-init / scope.md
  -> 场景 skill 与工具检查
  -> timeline / evidence / finding
  -> 报告与 field journal
```

任何真实目标都应先写明授权主体、测试范围、允许的网络行为、数据处理和停止条件。没有书面授权时，只应在自建靶场、公开 CTF 或离线样本中使用。

## 原理

项目把安全任务拆成“主路由 + 场景模块 + 工具自举 + 操作契约 + 证据链”。路由规则决定进入哪类 playbook；初始化阶段生成 scope；执行阶段把观察、命令、工件与 finding 关联起来；field journal 用于积累可复用经验。

这种架构能改善过程一致性，但不会自动证明漏洞存在、利用可控或报告没有误报。工具输出、agent 推理和最终 finding 都需要专业人员复核。

## 价值

- 把分散的逆向/取证工具选择转成显式路由和可审阅流程。
- 用 scope、timeline 和证据关联减少“只给结论、不留复现材料”的问题。
- 对多平台客户端保持相对中立，可作为安全实验室的流程模板。
- 大量场景模块适合教学、CTF 复盘和方法库维护。

## 风险边界

- 同一命令在自建靶场与第三方系统上的法律性质完全不同；skill 不能替代授权。
- 自动下载工具、MCP 或脚本会引入供应链、管理员权限和网络出口风险。
- “自进化知识库”可能沉淀凭据、目标数据、恶意样本路径或未经复核的方法。
- 成功执行 exploit 或 payload 可能造成服务中断、数据损坏或横向移动。
- README 中的规则数、benchmark 数和 CI 状态是上游自述，本页未独立复现其检出率或安全性。

## 补充建议

1. 在无外网、可快照的隔离靶场中固定仓库 commit 与工具哈希。
2. 默认关闭主动扫描、利用、持久化和凭据读取，按单项授权逐步开启。
3. 将 agent 输出分为 observation、hypothesis、verified finding，并保留失败尝试。
4. 对 journal 做脱敏、访问控制和定期清理，不把客户数据变成长期训练材料。
5. 用已知答案的 CTF/样本回归路由正确率、误报率和证据完整性。

## 参考资料

- 仓库与 README：https://github.com/zhaoxuya520/reverse-skill
- AI 启动说明：https://github.com/zhaoxuya520/reverse-skill/blob/main/README_AI.md
- 主路由：https://github.com/zhaoxuya520/reverse-skill/blob/main/skills/MASTER-ROUTING.md
- 路由矩阵：https://github.com/zhaoxuya520/reverse-skill/blob/main/skills/routing.md
- 在线教程：https://reverse.apivix.com/docs/
