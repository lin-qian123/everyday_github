# zhixin-companion

## 定位

`zhixin-companion` 是用于个人记录、复盘和认知梳理的一份伙伴型提示词/agent 配置。其核心约束是区分事实、感受和解释，在共情时保留现实检验；项目明确声明不替代医疗、心理治疗、法律或财务专业服务。

截至 2026-07-30，GitHub API 显示仓库创建于 2026-07-29，约 39 stars、5 forks；项目为 source-available，采用 CC BY-NC-SA 4.0，而非 OSI 开源许可证。它是早期开发者信号。

## 用法

可把 `prompt/知心伙伴.md` 全文放进支持 system prompt/custom instructions 的工具；在 Claude Code 中可直接克隆仓库，根目录的 `CLAUDE.md` 与 `AGENTS.md` 提供等价入口。个人记录默认应留在已忽略的本地路径，不要强制提交到公开仓库。

```bash
git clone https://github.com/LotusDecoder/zhixin-companion.git
cd zhixin-companion
claude
```

## 原理

提示词要求用户提供具体情境、想法、情绪和第一手细节，再用分层问题把可观察事实与解释性结论拆开。它把模型定位为模式归纳助手，而不授予模型对个人经历的最终解释权。

## 价值

- 为日记/复盘类 AI 使用提供较清晰的输入组织与现实检验框架。
- 将隐私、危机与专业支持边界直接写入 agent 工作流，适合个人本地记录试用。

## 风险边界

- 模型仍会遗漏上下文、迎合用户或强化不准确叙事；任何健康、安全、关系与金钱决定都应回到原始事实并寻求合格专业支持。
- 私人记录可能含第三方隐私、医疗资料与身份信息，须控制同步、日志、备份和模型提供方的数据处理路径。
- 非商业、署名与相同方式共享等许可条件会限制复用方式；部署前应读 LICENSE 与 NOTICE。

## 补充建议

把它用于低风险的自我反思，并定期导出到用户掌握的加密本地存储。对于情绪危机，产品应展示本地紧急资源与真人求助入口，而不是尝试由 agent 接管判断。

## 参考资料

- GitHub：<https://github.com/LotusDecoder/zhixin-companion>
- GitHub API 快照：<https://api.github.com/repos/LotusDecoder/zhixin-companion>
