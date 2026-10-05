<!-- markdownlint-disable MD013 -->

# Brewery AI（empero-org/brewery-ai）

> 上游仓库：<https://github.com/empero-org/brewery-ai> · 归类：模型、训练与推理基础设施 · 本页基于 2026-10-06 的 GitHub API、README、architecture / ETF / model 文档、manifest 与许可证静态整理，未安装控制面、租用 GPU、传输数据、训练模型或发布到 Hugging Face。

- 抓取快照：184 stars、23 forks、0 open issues；仓库创建于 2026-10-04 22:16 UTC。
- 热度信号：GitHub Search 按新建仓库 stars 排序的早期开发者信号；不是 GitHub Trending 或社媒互动量。
- 版本与许可：tag `v0.2.1`，无 GitHub latest Release；manifest 标记 Alpha，并采用带月收入门槛的 `LicenseRef-Brewery` 自定义许可证，GitHub API 显示 `NOASSERTION`。

## 定位

Brewery 是引导用户微调语言与图像模型的终端 Agent。用户与 “brewmaster” 对话，工具协助选择基础模型、整理数据、估算显存 / 时间 / 成本、配置 CPT / SFT / DPO 或 LoRA、在本机或 SSH GPU 上训练、比较结果，并生成 model card 后上传 Hugging Face。

## 用法

上游建议从 Git 安装 `brewery-ai`，运行 `brewery` 选择 Claude、OpenAI-compatible 或本地 guiding model。项目可在本机 GPU 执行，也可让用户先自行租用 Runpod / Vast.ai，再粘贴 SSH 命令由 Brewery 准备环境、上传数据并后台训练；涉及费用、安装、外发、SSH key 与发布的操作会在 UI 中请求确认。

## 原理

控制面包含 Agent loop、分阶段 tool schema、provider backend、数据处理、model profile、显存估算和 SSH job manager；GPU worker 独立运行 CPT / SFT / DPO、图像 LoRA、测试与导出。ETF 用统一 JSONL 表示对话、reasoning、tool call、RAG 文档、偏好与图像，再按模型 chat template 渲染训练样本；job 会固化 profile 快照与训练参数。

## 价值

它把模型、数据、许可、硬件、训练阶段和发布 checklist 放进一个可恢复项目目录，适合第一次建立微调实验的人理解完整链路。可视化 checkpoint、显存 / 成本估算和 model card 生成，也能减少只看到 loss 而忽略数据与制品记录的情况。

## 风险边界

- “guardrails” 是参数范围与交互确认，不是对模型训练正确性、SSH 主机、供应链、恶意数据或远端命令的隔离保证。
- 控制面可安装软件、生成 SSH key、传输数据、启动付费 GPU、合并权重并上传模型；每项都需要独立账户、预算、网络和制品权限边界。
- prompt、训练数据、合成样本与 guiding-model 对话可能进入 Anthropic、OpenAI-compatible、OpenRouter 或其他 provider；本地模式也可能下载模型与数据。
- 基础模型、dataset、合成数据、图像、adapter 与最终 merged model 的许可不能由代码许可证代替；自动 model card 仍需人工核对来源和商用条件。
- Brewery License 不是标准 MIT：超过每月 200 万美元平均总收入门槛的组织需要商业许可，采用前须做法务确认。
- 本轮未复跑 demo、显存 / 费用估算、DPO reference pass、远端断点恢复、token 处理或 `v0.2.1` 的训练质量。

## 补充建议

先在无敏感数据的 2B 级公开模型和小型固定数据集上做离线 trial，记录 commit、模型 / 数据 revision、GPU image、provider、实际费用与 eval；SSH 使用短期低权限账号、受控出站和独立 volume。所有上传、合并、公开发布继续保留人工 gate，并让法务核对自定义许可证与模型 / 数据条款。

## 参考资料

- [GitHub 仓库](https://github.com/empero-org/brewery-ai)
- [GitHub REST API](https://api.github.com/repos/empero-org/brewery-ai)
- [README 与训练流程](https://github.com/empero-org/brewery-ai/blob/main/README.md)
- [Architecture](https://github.com/empero-org/brewery-ai/blob/main/docs/architecture.md)
- [Empero Trace Format](https://github.com/empero-org/brewery-ai/blob/main/docs/etf.md)
- [支持模型与参数说明](https://github.com/empero-org/brewery-ai/blob/main/docs/models.md)
- [Python manifest](https://github.com/empero-org/brewery-ai/blob/main/pyproject.toml)
- [`v0.2.1` tag](https://github.com/empero-org/brewery-ai/tree/v0.2.1)
- [Brewery License](https://github.com/empero-org/brewery-ai/blob/main/LICENSE)
