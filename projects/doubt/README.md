# doubt

## 定位

`doubt` 是零依赖 Node.js CLI 与 agent skill，用可交互证据图而非单篇结论文本表示争议问题：主张、支持、反驳、限定与缺失证据均须链接到可定位来源。截至 2026-08-01 的 GitHub API 快照，它创建于 2026-07-31，约 2 stars、0 forks、MIT。

## 用法

使用 Node.js 18+ 运行 `npx doubt-ai demo --out doubt-demo.html` 查看样例；对自己的 `.doubt.json` 先执行 `npx doubt-ai validate decision.doubt.json`，再用 `npx doubt-ai map decision.doubt.json --out decision.html` 生成可离线审阅的 HTML。也可按宿主说明安装其 skill。

## 原理

数据模型将一个可证伪问题、暂定立场、原子主张和来源观察拆开，使用带类型的边表示支持、矛盾、限定和缺口。每个证据节点要求 URL 或本地路径、抓取日期及章节/页码/时间戳/行号定位；渲染和校验在本地执行。

## 价值

- 迫使结论与反例、未知项和精确定位同时出现，降低“引用看似相关即已证实”的误判。
- JSON 与单文件 HTML 便于版本控制、离线分享和审计。

## 风险边界

- 工具校验证据结构，不校验网页真实性、样本代表性、来源偏见或推理正确性。
- 本地路径、URL fragment 和导出 HTML 仍可能泄露敏感材料；分享前应脱敏并检查访问权。
- 图形化结构会带来确定性错觉，医疗、法律、金融或人员判断仍须合格专家复核。

## 补充建议

将其用于 ADR、模型选型、事故复盘等可追溯决策；建立来源评级、失效日期和反对意见审查规则。对远程页面保留抓取快照或哈希，但不要以哈希取代人工阅读。

## 参考资料

- GitHub：<https://github.com/alsoleg89/doubt>
- 在线演示：<https://alsoleg89.github.io/doubt/playground/>
- GitHub API 快照：<https://api.github.com/repos/alsoleg89/doubt>
