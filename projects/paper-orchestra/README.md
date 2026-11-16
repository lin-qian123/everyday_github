<!-- markdownlint-disable MD013 -->

# PaperOrchestra（google-research/paper-orchestra）

- GitHub：<https://github.com/google-research/paper-orchestra>
- 核查：2026-11-17（Asia/Shanghai）07 时段；1,430 stars / 236 forks / 33 open issues（含 PR）；仓库 ID `1226691771`。
- 热度：官方综合 / Python daily +306；首次建档，不代表今日发布。
- 固定 main：`d9bae997e793a015ed38bb1605be9eb58c00284f`；本轮 Releases 列表为空，无可指认的稳定发行。
- 许可与证据：Apache-2.0；README 明确不是正式支持的 Google 产品。以下是相关文档与源码静态核读，未生成论文、执行绘图或调用模型。

## 定位

Google Cloud AI Research 作者发布的多 Agent 论文写作框架，把想法、实验日志及已有图整理为大纲、综述、分节正文、修订和 LaTeX / PDF。其“submission-ready”是上游目标，不能代替实验复现、事实核查、作者责任或投稿规则审查。[固定 README](https://github.com/google-research/paper-orchestra/blob/d9bae997e793a015ed38bb1605be9eb58c00284f/README.md)

## 用法

上游建议 Python 3.11 环境，安装 `requirements.txt`，准备模型服务与 Semantic Scholar 相关配置。依赖文件未锁版本；LaTeX 编译另调用 `pdflatex` 和 `bibtex`。先用公开或合成材料在独立输出目录试验，不直接使用唯一的研究资料副本。[依赖](https://github.com/google-research/paper-orchestra/blob/d9bae997e793a015ed38bb1605be9eb58c00284f/requirements.txt)、[PDF / 编译实现](https://github.com/google-research/paper-orchestra/blob/d9bae997e793a015ed38bb1605be9eb58c00284f/utils/pdf_utils.py)

CLI 需要 raw materials 与模板路径；默认素材名为 `idea_sparse.md`、`experimental_log.md`，非绘图路径需要已有 figures。示例（未执行）：

```bash
python paper_writing_cli.py \
  --raw_materials_dir /path/to/materials-copy \
  --latex_template_dir templates/cvpr2025 \
  --output_dir /path/to/new-output \
  --use_plotting false
```

CLI writer / reflection 默认 `gemini-3.1-pro-preview`，绘图默认关闭；模型名是源码默认值，不保证当前账号可用。未给 research cutoff 时 CLI 取当前年月，而底层函数仍有历史默认值，直接调用不能假定和 CLI 一致。[CLI 参数](https://github.com/google-research/paper-orchestra/blob/d9bae997e793a015ed38bb1605be9eb58c00284f/paper_writing_cli.py)、[写作管线](https://github.com/google-research/paper-orchestra/blob/d9bae997e793a015ed38bb1605be9eb58c00284f/methods/paper_writer.py)

## 原理

各 Agent 顺序构造 outline、文献结果与 citation map、草稿、反思修订，再编译。模型路由按名称字符串选择 Gemini 或 OpenAI helper；不是任意 provider 的通用适配保证。PDF 评估路径对 Gemini 传原始 PDF bytes，对 OpenAI 传提取文本，数据出口与信息损失不同。[模型路由](https://github.com/google-research/paper-orchestra/blob/d9bae997e793a015ed38bb1605be9eb58c00284f/utils/llm_backend_utils.py)

可选绘图会生成代码并进入执行 worker；`execute_plot_code_worker()` 从代码块取文本，直接 `exec(code_clean, exec_globals)`。空 globals 没有构成 Python 安全沙箱；可运行代码的权限仍属于宿主。[绘图 worker](https://github.com/google-research/paper-orchestra/blob/d9bae997e793a015ed38bb1605be9eb58c00284f/utils/paper_banana_utils.py)

## 价值

适合把写作步骤拆成可检查的中间文件，比较文献检索、章节构造和修订方法。已有真实实验结果时，可以研究其是否降低整理工作量；本轮没有验证节省时间、科研质量或投稿接受率。README 仍说生成数据集尚未包含、将另行发布，因此仅凭本仓库不能假定论文中的整套评测已经可复现。

## 风险边界

- **输出目录有清理副作用。** CLI 会替换目标目录里的 `raw_materials` 副本，写作入口会删除旧 `latex_writeup` 与 `final_paper.pdf`；不能把续跑理解为保留全部旧产物。见前述 CLI / 写作实现。
- **引用 F1 不等于论断被来源支持。** autorater 提取标题、查 Semantic Scholar ID，按成功识别的唯一 ID 集合求交集；未匹配项和重复引用可能不进入同样的分母。P0 / P1 还来自模型分类，应并报匹配覆盖率与逐条支持关系。[引用评分实现](https://github.com/google-research/paper-orchestra/blob/d9bae997e793a015ed38bb1605be9eb58c00284f/autoraters/citation_f1.py)
- 该评分模块载入时直接打印 `SEMANTIC_SCHOLAR_API_KEY` 变量值；运行前需处理日志暴露面。本轮只读源码，没有加载模块或读取用户密钥。
- 开启绘图会执行生成的 Python；关闭绘图仍有远端模型 / 检索与本地 LaTeX 进程，不代表离线或无副作用。编译 helper 会记录各步返回码，但最终移动 PDF 主要依据文件存在和无 timeout；文件存在本身不是内容验收。
- 想法、日志、论文内容与图像可进入第三方服务；模型费用、重试和授权按实际配置核。README 的可选演示邮件配置不是所有路径必需。
- 前端文档提醒可能留下后台写作进程；离开网页不保证停止任务和计费。[前端进程说明](https://github.com/google-research/paper-orchestra/blob/d9bae997e793a015ed38bb1605be9eb58c00284f/frontend/README.md)

## 补充建议

先关闭自动绘图，固定依赖、模型和 cutoff，用小型公开材料检查引用映射与输出覆盖。需要绘图时使用无敏感凭据的独立执行环境，并把真实数据、坐标单位、拟合、生成概念图与实验结果分开。逐条核对引文、数据、公式和贡献，检查所有编译返回码并实际阅读 PDF；本页不等于论文全文评审。

## 参考资料

- [仓库 API](https://api.github.com/repos/google-research/paper-orchestra)、[Releases](https://github.com/google-research/paper-orchestra/releases)、[Apache-2.0](https://github.com/google-research/paper-orchestra/blob/d9bae997e793a015ed38bb1605be9eb58c00284f/LICENSE)。
- 固定 SHA 的 README、CLI、管线、模型路由、绘图 worker、引用评分、编译与前端说明见对应段落；未审计全仓或复跑研究评测。
