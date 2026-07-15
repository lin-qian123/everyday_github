<!-- markdownlint-disable MD013 -->

# openscience

## 定位

`synthetic-sciences/openscience` 是一个面向科学研究的开源 AI workbench。它把文献检索、假设形成、代码编写、实验运行、数据分析和报告撰写放在同一个浏览器工作区里，目标是让 agent 像研究合作者一样完成可追踪的科研循环。

它与仓库中已有的 `open-science` 目录不是同一个上游项目；本页使用 `openscience` 目录名，专门跟踪 Synthetic Sciences 的实现。

## 用法

项目提供 npm 包和 CLI：

```bash
npm install -g @synsci/openscience
openscience
```

也可以用 `npx synsci` 启动。首次运行会引导配置模型来源，支持 Anthropic、OpenAI、Google 和开放权重模型等多种 provider，也支持使用 Synthetic Sciences 的 Atlas 托管模型服务。

## 原理

OpenScience 本地运行一个 server，承载浏览器 UI、agent runtime 和工具层。agent 可以调用 shell、编辑器、LSP、MCP server、科学数据库连接器和技能包，并把过程流式回传到工作区。README 中明确列出默认 `research` agent，以及 biology、physics、ml 等专家 agent 和 critique / literature-review sub-agent。

其关键设计不是单次问答，而是把科研 loop 拆成持续会话：读论文、形成假设、写代码、跑实验、查数据库、输出结果，并在本地保存 session、artifact 和 provenance。

## 价值

- 把科研 agent 从“聊天窗口”推进到可运行工作区。
- 覆盖机器学习、生物、物理、化学等领域，并接入 arXiv、OpenAlex、Semantic Scholar、PubChem、PDB、UniProt 等数据库。
- 支持 BYOK 和多模型路由，降低单一模型或单一平台锁定。
- 对高校、实验室和个人研究者来说，比闭源科研 AI workbench 更容易审计和扩展。

## 风险边界

- 科研结论不能直接采信，代码、实验、引用和统计结果都需要人工复核。
- 多 provider 和外部数据库接入会带来密钥、数据合规和成本管理问题。
- 290+ skills 的广覆盖不等于每个 skill 都经过同等质量验证。
- 若使用 Atlas 托管模型或云计算资源，需要额外评估数据路径和账单风险。

## 补充建议

- 先在非敏感公开数据上跑通完整科研 loop，再接入真实课题。
- 对每个实验要求留下 artifact、环境、随机种子、命令和结果摘要。
- 将其与 Jupyter、DVC、MLflow、实验室已有代码库做边界划分，避免重复记录。
- 重点关注后续是否补齐 benchmark、失败案例和第三方复现实验。

## 参考资料

- GitHub: <https://github.com/synthetic-sciences/openscience>
- Docs: <https://openscience.sh/docs>
- Homepage: <https://openscience.sh>
- MarkTechPost 介绍: <https://www.marktechpost.com/2026/07/05/synthetic-sciences-releases-openscience-an-open-source-model-agnostic-ai-workbench-for-machine-learning-biology-physics-and-chemistry-research/>
