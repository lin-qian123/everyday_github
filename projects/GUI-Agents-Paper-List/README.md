# GUI-Agents-Paper-List（OSU-NLP-Group/GUI-Agents-Paper-List）

> GitHub: https://github.com/OSU-NLP-Group/GUI-Agents-Paper-List  
> Web: https://osu-nlp-group.github.io/GUI-Agents-Paper-List/  
> 定位：GUI agent 方向的论文、基准、数据集、框架与趋势索引。

## 项目定位

`GUI-Agents-Paper-List` 是一个面向 GUI agent / computer-use agent 的结构化论文库。它覆盖 Web、Desktop、Mobile、General GUI 等环境，围绕 GUI grounding、benchmark、dataset、reinforcement learning、memory、safety、prompt injection 等关键词组织论文。

它不是一个 agent 运行框架，而是 GUI agent 研究和工程选型的知识入口。随着浏览器 agent、桌面 agent、mobile agent 和短视频/动态界面 agent 成为热点，这类索引能帮助工程团队判断：哪些 benchmark 可靠、哪些能力仍是瓶颈、哪些论文已经有代码或数据集。

## 用法

推荐先访问网站版：

```text
https://osu-nlp-group.github.io/GUI-Agents-Paper-List/
```

网站支持全文搜索、按环境筛选、按关键词筛选、论文详情页、BibTeX 复制和统计图。仓库中的 `papers.yaml` 与 `adjacent.yaml` 是结构化数据源，README 和网站由这些数据生成。

如果要本地使用：

```bash
git clone https://github.com/OSU-NLP-Group/GUI-Agents-Paper-List.git
cd GUI-Agents-Paper-List
```

然后直接检索 `papers.yaml` 或查看 README 中的最新论文列表。

## 核心原理

这个项目的核心是把 GUI agent 领域拆成可检索的结构化元数据：

- 环境维度：Web、Desktop、Mobile、General GUI；
- 任务维度：GUI grounding、planning、long-horizon task、workflow、annotation；
- 资源维度：paper、code、dataset、benchmark、publisher、BibTeX；
- 风险维度：safety、security、prompt injection、failure modes；
- 时间维度：按论文日期持续更新，展示领域增长趋势。

相比普通 markdown 列表，它更像一个轻量研究数据库。

## 价值

GUI agent 是 agent 热点中最难落地的一类，因为它同时涉及视觉理解、状态记忆、动作规划、工具/浏览器控制、动态界面变化和安全边界。`GUI-Agents-Paper-List` 的价值在于给这个方向提供可追踪底图：

- 评估 browser-use、UI-TARS、page-agent、OpenSandbox 等项目时可查相关 benchmark；
- 做 computer-use agent 时可快速定位 WebArena、OSWorld、AndroidWorld 等评测语境；
- 研究 GUI grounding 或视觉记忆失败模式时可按关键词检索；
- 为本仓库的 GUI / UI / agent 交互层项目提供论文背景。

## 风险边界

- 论文索引不是论文质量认证，收录不代表结果可复现。
- BibTeX 和元数据由工具生成或社区维护，正式引用前仍需核对原论文。
- GUI agent benchmark 更新很快，榜单结论可能受模型版本、工具环境、提示词和评测脚本影响。
- 研究论文和生产可用性之间存在距离，尤其是涉及真实账号、支付、隐私数据和浏览器权限的场景。

## 补充建议

- 用它给 GUI agent 项目建立“评测对照表”：项目声称解决什么问题，对应哪些 benchmark。
- 对涉及安全、prompt injection、权限边界的论文单独归档，服务后续 agent 安全专题。
- 关注动态界面、长时程 GUI workflow、视觉记忆和观察控制，这些问题会直接影响真实产品可用性。
- 与本仓库 `UI-TARS-desktop`、`browser-use`、`page-agent`、`video-use` 等条目交叉阅读。

## 参考资料

- GitHub 仓库：https://github.com/OSU-NLP-Group/GUI-Agents-Paper-List
- 网站版索引：https://osu-nlp-group.github.io/GUI-Agents-Paper-List/
- 结构化数据：https://github.com/OSU-NLP-Group/GUI-Agents-Paper-List/blob/main/papers.yaml
- GitHub API 元数据：https://api.github.com/repos/OSU-NLP-Group/GUI-Agents-Paper-List
