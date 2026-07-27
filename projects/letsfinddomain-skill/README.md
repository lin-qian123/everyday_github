# letsfinddomain-skill

## 定位

`letsfinddomain-skill` 是面向 Codex、Claude Code、Cursor 等工具的只读域名筛选 skill：从产品想法生成候选名、批量查询可用性、比较首年与续费价格，并提示潜在品牌冲突。

截至 2026-07-28，GitHub API 显示其创建于 2026-07-27，约 61 stars、4 forks；这只是早期开发者信号，不等同于成熟的域名决策工具。

## 用法

安装后以 slash command 描述产品、目标受众、TLD 和预算；首次使用真实可用性与续费价格数据时，按项目文档配置注册商 API，并只授予查询所需权限。

```bash
npx skills add https://github.com/meepo-it/letsfinddomain-skill \
  --skill letsfinddomain-skill --agent '*' --global --yes
```

## 原理

skill 将命名生成、候选约束和查询任务编排给 agent；可用性查询优先走注册商 API，并对批量请求采用保守限速。没有账户时可用 RDAP 做有限试查，但它不代表实际购买资格或续费价格。

## 价值

- 把命名、可用性和续费成本放进同一轮产品探索，减少只看首年促销价的误判。
- 明确只读边界：不会购买、转移域名或修改 DNS。

## 风险边界

- 可注册不表示不侵权；商标、地域、行业近似性仍需独立检索与法务判断。
- 注册商价格、库存、限额和账户层级会变动，输出只能作为查询当时的候选线索。
- API 凭据与批量查询日志可能含商业计划信息，应避免交给不可信 agent 或写入仓库。

## 补充建议

先用无凭据的少量候选验证流程；进入采购前，复查目标注册商的最终价格、自动续费和转移政策，并为品牌冲突保留人工审核记录。

## 参考资料

- GitHub：<https://github.com/meepo-it/letsfinddomain-skill>
- GitHub API 快照：<https://api.github.com/repos/meepo-it/letsfinddomain-skill>
