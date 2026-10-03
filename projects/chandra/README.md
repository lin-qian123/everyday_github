<!-- markdownlint-disable MD013 -->

# Chandra OCR 2（datalab-to/chandra）

> 上游仓库：<https://github.com/datalab-to/chandra> · 归类：RAG、检索与知识处理 · 本页基于 2026-10-04 的 GitHub API、README、benchmark 表、manifest、model card、Release 与 LICENSE 静态整理，未上传文档到托管平台、下载权重、运行 H100 / vLLM 或复测 OCR 准确率。

- 抓取快照：12,400 stars、1,250 forks、61 open issues。
- 热度信号：GitHub Python Trending 抓取时约 +20 当日 stars。
- 版本与许可：代码 Apache-2.0，Release / tag / Python manifest 为 `v0.2.0` / `0.2.0`；模型权重采用修改版 OpenRAIL-M，并带商业用途限制。

## 定位

Chandra OCR 2 是把图片和 PDF 转成带布局的 HTML、Markdown 或 JSON 的文档理解模型，重点处理表格、公式、手写体、表单、图像 / 图注与 90+ 语言。它同时提供本地 Hugging Face 与 vLLM server 两种推理路径，Datalab 另有准确率更高的托管版本。

## 用法

安装 `chandra-ocr` 后可用 `chandra_vllm` 启动服务，再用 `chandra input.pdf ./output` 批量导出 Markdown、HTML、metadata 与抽取图像；`chandra-ocr[hf]` 可直接本地推理，`chandra-ocr[app]` 提供 Streamlit。页码、最大输出 token、并发、图片与页眉页脚均可配置。

## 原理

输入页先被渲染为图像，再由视觉语言 OCR 模型生成结构化文档标记和布局关系；后处理写出多格式文件并抽取图像。vLLM 路径把模型服务与批处理客户端解耦以提高并发，Hugging Face 路径则把推理留在单机进程。模型基于 Qwen 3.5 相关组件，输出上限和并发会直接影响长页完整性。

## 价值

相较纯文本 OCR，它试图同时保留阅读顺序、表格、公式、表单和图像信息，更适合作为 RAG / 文档 ETL 的结构化入口。CLI、Python 包、两种推理后端和样例输出也便于把识别、人工抽查与后续索引拆成可复现步骤。

## 风险边界

- README 的综合、多语言与 throughput 表主要来自作者测试；H100 80GB 上 `1.44 pages/s`、估计真实场景 `2 pages/s` 不能外推到其他 GPU、文档域或批量设置。
- 代码 Apache-2.0 不等于权重可自由商用；修改版 OpenRAIL-M 仅对研究、个人和低于特定融资 / 收入门槛的 startup 免费，并限制与 Datalab API 竞争的用途。
- OCR / VLM 可能漏字、幻觉、错表格、错公式、错阅读顺序或截断长页；医疗、法律、财务、档案与无障碍输出必须逐页回到原件核验。
- 托管 Datalab 平台与本地开源权重不是同一能力 / 数据边界；“零保留”等平台声明需回到当前服务条款、区域与实际配置验证。
- 抽取后的文档可能含网页指令、隐藏文本或恶意 prompt；进入 Agent / RAG 前仍需把内容视为不可信数据，不可直接提升为系统指令。
- 本轮未复测 90 种语言、手写、图表 caption、PDF 渲染、并发失败和长页 token 上限。

## 补充建议

固定 `v0.2.0` 代码、容器与 model revision，在自有多语言金标上分字段计算文字、表格、公式、顺序和漏页率；保留原 PDF 页码、区域坐标、输出哈希和人工修订记录。商业落地先书面确认权重许可；敏感文档优先本地路径，并对进入 RAG 的提取文本做 prompt-injection 隔离与来源回链。

## 参考资料

- [GitHub 仓库](https://github.com/datalab-to/chandra)
- [GitHub REST API](https://api.github.com/repos/datalab-to/chandra)
- [README、用法与 benchmark](https://github.com/datalab-to/chandra/blob/master/README.md)
- [完整多语言 benchmark](https://github.com/datalab-to/chandra/blob/master/FULL_BENCHMARKS.md)
- [Python manifest](https://github.com/datalab-to/chandra/blob/master/pyproject.toml)
- [Hugging Face model card](https://huggingface.co/datalab-to/chandra-ocr-2)
- [v0.2.0 Release](https://github.com/datalab-to/chandra/releases/tag/v0.2.0)
- [代码 LICENSE](https://github.com/datalab-to/chandra/blob/master/LICENSE)
