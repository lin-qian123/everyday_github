<!-- markdownlint-disable MD013 -->

# Claude-Red（SnailSploit/Claude-Red）中文解读

> 证据快照：2026-09-13（Asia/Shanghai）。GitHub REST API 显示 3,572 stars、550 forks、12 open issues，最新 release 为 `v0.3.0`，MIT。上游列出 23 类、78 个 offensive-security skills；本文仅做静态资料审查，未加载 skills 或执行任何攻击步骤。

## 定位

Claude-Red 是给 Claude Skills 体系使用的进攻安全方法库。每个 `SKILL.md` 聚焦一个攻击面，例如 Web、身份认证、Active Directory、无线、云、移动端、容器、CI/CD、漏洞利用、权限提升、C2、供应链和 AI 安全。

它不是扫描器或隔离执行环境，而是一组会改变模型行为与方法选择的高风险上下文包。价值和危险来自同一件事：把原本分散的 red-team 知识整理成可按对话触发、低摩擦加载的操作流程。

## 用法

上游给出的完整安装会把仓库放入用户级 Claude skills 目录：

```bash
git clone https://github.com/SnailSploit/claude-red ~/.claude/skills/claude-red
```

也可以 sparse checkout 单个类别，或运行交互式 `install.sh`。安全评估时不应先做全量安装；更稳妥的做法是固定 tag、只取一个明确授权类别，在无生产凭据、无真实目标的实验环境中逐文件审阅后再加载。

## 原理

- 每个 skill 通过 frontmatter、触发描述、方法步骤、工具建议、升级路径和报告要求向模型提供领域上下文。
- Claude 根据对话意图按需加载匹配 skill，因此未触发的材料不占用主要上下文。
- 仓库本身主要分发方法与提示，不替目标做资产授权、身份验证、速率限制或网络隔离。
- 报告、快速检查与分类索引提高流程一致性，但最终命令仍由 agent 或使用者在其现有权限下执行。

## 价值

- 为书面授权的 red team、CTF、漏洞研究和培训提供统一、可版本化的方法清单。
- 按攻击面拆分便于最小化加载范围，也方便针对某一类技术做同行审阅和更新。
- 报告与证据 skill 有助于把发现、复现条件、严重度和修复建议分开记录。
- 作为 skill 供应链样本，可以审查“知识包如何改变高权限 agent 行为”。

## 风险边界

- 仓库包含 EDR 绕过、持久化、凭据提取、数据外传、钓鱼和 exploit-development 等双重用途内容；未经明确书面授权不得用于真实系统或第三方账户。
- Claude 的安全策略、对话声明或 skill 文本不是访问控制。真正边界必须由实验网络、低权限身份、allowlist、时间窗和外部审批执行。
- 全量克隆到用户级目录会扩大所有未来会话的提示供应链；上游更新或恶意提交可改变 agent 行为。
- 方法清单可能过时、产生误报或忽略目标特定防护；MIT 许可不对技术正确性、合法性或安全结果背书。
- 仅生成命令、PoC 或报告不证明漏洞存在；需要受控复现、证据保存和人工确认。

## 补充建议

1. 只在拥有者、目标、时间、允许技术和数据处理方式均书面明确的范围内使用。
2. 固定 `v0.3.0` 或 commit，逐个审查所需 skill；不要把整个仓库自动更新到全局目录。
3. 在隔离靶场使用无生产权限凭据，并通过网络 allowlist、命令审批和完整日志限制 agent。
4. 将“建议方法”“执行记录”“已复现发现”和“修复验证”分成不同证据层级。

## 参考资料

- GitHub：<https://github.com/SnailSploit/Claude-Red>
- GitHub REST API：<https://api.github.com/repos/SnailSploit/Claude-Red>
- Releases：<https://github.com/SnailSploit/Claude-Red/releases>
- Skills 索引：<https://github.com/SnailSploit/Claude-Red#skill-index>
- 贡献规范：<https://github.com/SnailSploit/Claude-Red/blob/main/CONTRIBUTING.md>
- LICENSE：<https://github.com/SnailSploit/Claude-Red/blob/main/LICENSE>
