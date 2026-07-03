# open-science

- GitHub：<https://github.com/aipoch/open-science>
- 抓取时间：2026-07-04（Asia/Shanghai）
- 今日信号：GitHub API 显示该仓库创建于 2026-07-03，抓取时约
  `31 stars / 0 forks`，README 标注状态为 `Vision / Pre-Alpha`，
  定位为 model-agnostic AI workbench for scientific discovery。

## 定位

`open-science` 是一个面向科研发现的开源 AI 工作台愿景仓库。它明确对标
Anthropic 的 Claude Science 这类闭源科研 AI 工作台，但主张用开源、
模型无关、可本地部署、可审计的方式服务科研流程。

当前阶段需要谨慎理解：README 明确说明还没有可工作的软件，现阶段主要是架构愿景、设计原则、路线图和社区招募。

## 用法

截至本次抓取，项目尚未提供可运行应用。可用方式主要是：

- 阅读 README，理解它计划覆盖的科研工作流。
- 参与 GitHub Discussions 或 Discord，讨论架构、数据源、计算环境和
  模型接入。
- 关注路线图中关于 notebook、数据库、HPC、参考文献、审稿 agent 和 provenance 的设计。

如果要在真实科研项目中使用，当前还不能把它当作生产工具，只能作为早期社区与架构方向观察对象。

## 原理

项目设想中的工作台会把科研日常的分散工具接起来：

1. 文献管理、Jupyter / R / notebook、HPC、数据库、统计工具和写作环境共享上下文。
2. 用 agent 协调专门子任务，例如 genomics、proteomics、structural biology、cheminformatics 等。
3. 保留可追溯 provenance，让分析、数据来源、计算步骤和结论可以被复查。
4. 支持不同模型和部署方式，避免被单一闭源供应商绑定。

## 价值

- 对科研团队：提出了开放科研 AI 工作台的架构议题，尤其是可审计、可复现、可本地化。
- 对 AI agent 生态：把 agent 从代码和办公扩展到严肃科研工作流，
  强调工具、数据、计算和引用的长链路治理。
- 对本仓库：补充“科学发现工作台”方向，与 `scientific-agent-skills`、
  `academic-research-skills`、`open-notebook` 可形成观察线。

## 风险边界

- 目前是 pre-alpha 愿景仓库，没有可运行软件，不能用 stars 或 README 叙事替代技术成熟度判断。
- 科研场景涉及数据许可、患者隐私、实验可复现、模型幻觉和引用准确性，远高于普通知识库问答风险。
- model-agnostic 和本地部署是目标，不代表当前已经实现。
- 如果后续接入第三方模型或数据库，需要单独审查数据处理协议和合规边界。

## 补充建议

- 短期把它当作趋势信号，而不是工具选型候选。
- 后续优先关注是否出现可运行 prototype、插件接口、数据 provenance
  格式和真实科研 demo。
- 可与 Claude Science、open-notebook、Jupyter agent、科研 skill 项目
  横向比较，判断科研 AI 会先落在文献、数据分析、HPC 调度还是审稿校验。

## 参考资料

- GitHub 仓库：<https://github.com/aipoch/open-science>
- 项目 X：<https://x.com/aipoch_ai>
- Anthropic Claude Science 新闻：<https://www.anthropic.com/news/claude-science-ai-workbench>
