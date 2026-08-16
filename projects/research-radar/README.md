<!-- markdownlint-disable MD013 -->

# Research Radar

## 定位

[`researchradar/research-radar`](https://github.com/researchradar/research-radar) 是一个自托管、workspace-first 的技术研究情报工具。它针对用户配置的研究者、主题和来源收集新材料，做身份与 URL 规范化、去重、透明排序，并生成本地可浏览的 Today、Reading、Search、Archive、Following 页面。当前上游标注为 v0.1 alpha，适合作为个人或小团队的可审计研究订阅原型，而非已经验证的全面情报平台。

## 用法

```bash
git clone https://github.com/researchradar/research-radar.git
cd research-radar
python -m pip install -e .

research-radar init ~/my-radar
research-radar collect --workspace ~/my-radar
research-radar build-site --workspace ~/my-radar
research-radar serve --workspace ~/my-radar
```

先在新建、非敏感 workspace 配置 `people.yaml`、`topics.yaml`、`sources.yaml`、`scoring.yaml` 和 `feedback.yaml`。上游还提供不访问网络的合成 fixture smoke test，适合先验证本地安装；服务默认绑定 `127.0.0.1:8765`，不要在未经认证和反向代理审计前公开暴露。

## 原理

- 收集器目前支持 arXiv 查询与 RSS/Atom；材料进入 workspace 后，按规范化身份与 URL 去重，再按关注人物、主题、来源优先级、时效和显式反馈等可见信号排序。
- 用户的真实订阅、阅读、反馈与收集数据放在源代码仓库外的 workspace；这降低误提交私密 watchlist 的风险，但备份、磁盘权限和同步目标仍由部署者负责。
- 对 RSS URL，项目说明会检查私网、loopback、link-local、保留和 multicast 地址并跟随重定向检查；这是一层抓取防护，不替代网络出口规则、代理策略、依赖审计或内容可信度验证。

## 价值

- 把“订阅—去重—排序—检索—归档”拆成可检查的本地管线，适合处理主题明确、来源可控的技术跟踪任务。
- 排名特征和 feedback 文件可见，便于将结果当作可调整的阅读队列，而非不可解释的推荐黑箱。
- GitHub API 于 2026-08-17 的快照显示该仓库创建于 2026-08-16、约 5 stars、0 forks、MIT。它是极早期开发者信号，不能据此推断稳定性、覆盖率、搜索质量或长期维护能力。

## 风险边界

- 排名只能反映配置与当前规则，不证明论文、RSS 内容、作者身份、元数据或引用结论真实可靠；重要研究结论仍须回到原始来源核验。
- workspace 可包含个人关注主题、阅读反馈与采集历史；须以私有目录权限、加密备份和明确保留/删除规则保护，避免同步到公开仓库。
- 即使项目实现了部分 SSRF 过滤，外部 feed 仍可能失效、投毒、重定向或产生高频请求；应设置网络 allowlist、请求限额、超时和失败审计。
- MIT 仅覆盖仓库代码；arXiv、RSS 内容、网页快照和后续加入的模型/API 各有许可证与使用限制。

## 补充建议

1. 先运行合成 offline fixture，随后仅接入 2--3 个可信公开源，人工检查采集、去重、排序与归档输出。
2. 为每一个排名结果保留来源 URL、抓取时间、命中规则和分数解释；不要让自动排序直接驱动投稿、投资或实验决策。
3. 将 workspace 置于受备份和权限控制的位置，提交 Git 前用 ignore 规则与密钥扫描确认不会泄露 `config/`、数据或令牌。
4. 在扩大订阅前做 RSS 重定向、异常输入、重复链接、网络失败和跨平台编码测试，并记录版本与配置快照。

## 参考资料

- [GitHub 仓库](https://github.com/researchradar/research-radar)
- [上游 README / Quickstart](https://github.com/researchradar/research-radar#quick-start)
- [项目安全说明](https://github.com/researchradar/research-radar#your-data-stays-yours)
- [GitHub REST API 元数据快照](https://api.github.com/repos/researchradar/research-radar)
