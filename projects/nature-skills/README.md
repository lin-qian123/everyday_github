<!-- markdownlint-disable MD013 -->

# nature-skills：面向论文阅读、写作与科研图件的技能库

- 上游：[Yuan1z0825/nature-skills](https://github.com/Yuan1z0825/nature-skills)；分类：Agent 框架与技能生态。
- 更新：2026-11-04（Asia/Shanghai）；固定 main SHA：`69817e4dad8bfc52fa4e59a9d8355e4264a4d3a7`。
- 热度：Python daily +167；API 52,035 stars / 2,712 forks / 5 open issues（含 PR）。发行列表为空；根许可 Apache-2.0。
- 证据范围：官方榜单、API、完整目录树、固定 README、安装脚本和抽样技能 / 评估文档；未安装技能、提交论文、生成图件或调用服务。

## 定位

围绕 SKILL.md、参考资料、脚本和资产组织科研工作流，覆盖阅读、润色、写作、图件、引用核验、审稿回复及 Office 产物。当前树有 24 个顶层 SKILL.md，其中 nature-shared 是共享支持包，README 将其余 23 项列为技能；Stable / Beta / Draft 是作者状态标记。

项目名称和 Nature 风格定位不构成期刊官方背书。README 的机构关注 / 借鉴叙述属于作者自述，本轮没有独立证据支持其因果或认可关系。

## 用法

先 clone 并固定提交，按任务检查一个完整技能目录及其共享依赖：

```sh
git clone https://github.com/Yuan1z0825/nature-skills
cd nature-skills
git checkout 69817e4dad8bfc52fa4e59a9d8355e4264a4d3a7
```

例如阅读与部分写作技能需要保留 nature-shared，不能只复制 SKILL.md。上游另提供 npx skills 按需安装，以及 `scripts/update-codex-skills.sh` 全量同步；后者默认目标是用户技能目录，支持 --dest 和 --check。先在独立目标目录检查文件差异，不要把安装脚本当作仅查看命令。

Python / R、浏览器、MCP 和模型 API 依赖按技能单独配置。nature-figure 区分数据绘图、可编辑矢量示意图与 OpenRouter AI 生图；三条路线的依赖、数据出口和验收方式不同。

## 原理

- 技能入口规定任务触发、证据契约和交付步骤，按需读取 references / static / manifest / scripts。
- 共享包复用写作、期刊格式和来源规则；具体技能串联检索、解析、代码生成和文件输出。
- figure 路线包含面板对齐、PDF 文字、碰撞检查与实际渲染目检要求；脚本检查覆盖有限，不能代替数值和科学含义复核。
- 安装脚本逐目录同步并校验差异；--prune 只处理历史清单记录且上游已删除的目录。自动更新 hook 是另一个需要主动启用的机制。

## 价值

可把来源、主张上限、素材和产物验收写入可复用流程，减少论文与图件任务重复描述。适合先裁剪为个人实验室的小范围模板；是否保留原始数据、可编辑对象与正确引用，仍应检查最终文件。

## 风险边界

- 技能会影响宿主 Agent 的文件、脚本和联网行为，安装不构成对后续模型调用、账号登录、付费或外部写入的统一授权。
- 全量同步、可选自动拉取和 --prune 会改变已安装文件；固定源 SHA、目标与更新策略，并保留个人修改。
- 未发表论文、数据、图片和凭据的出口随模型 / MCP / 网页服务而变；README 同时有商业服务入口，开源技能许可不能代替服务条款与隐私判断。
- 作者 2026-09-06 smoke evaluation 使用五个隔离上下文、六个合成短任务，仅观察明确调用后的范围遵守；文档明确不是自动路由、前后对照、跨模型或完整论文 / PPT 质量验证。
- Nature 风格、模拟审稿、自动图件或检查通过不能证明发表适配、科学正确或真实审稿结论；AI 示意图与实验数据图须保留清晰来源边界。

## 补充建议

1. 先选一个非敏感短任务，固定输入、模型、技能 SHA 和预期产物，检查内容与来源是否对应。
2. 绘图同时核数据、单位、统计口径、导出文件和最终尺寸目检；Office 产物实际重开核验。
3. 对隐式技能选择、长文、引用真实性和跨模型行为建立独立样例，不从六个 smoke 任务外推。

## 参考资料

- [README 与技能索引](https://github.com/Yuan1z0825/nature-skills/blob/69817e4dad8bfc52fa4e59a9d8355e4264a4d3a7/README.md)。
- [figure 入口](https://github.com/Yuan1z0825/nature-skills/blob/69817e4dad8bfc52fa4e59a9d8355e4264a4d3a7/skills/nature-figure/SKILL.md)、[范围 smoke evaluation](https://github.com/Yuan1z0825/nature-skills/blob/69817e4dad8bfc52fa4e59a9d8355e4264a4d3a7/docs/skill-scope-smoke-evaluation.md)。
- [同步脚本](https://github.com/Yuan1z0825/nature-skills/blob/69817e4dad8bfc52fa4e59a9d8355e4264a4d3a7/scripts/update-codex-skills.sh)、[LICENSE](https://github.com/Yuan1z0825/nature-skills/blob/69817e4dad8bfc52fa4e59a9d8355e4264a4d3a7/LICENSE)、[API](https://api.github.com/repos/Yuan1z0825/nature-skills)。
