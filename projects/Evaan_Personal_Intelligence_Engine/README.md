<!-- markdownlint-disable MD013 -->

# Evaan_Personal_Intelligence_Engine

> 上游仓库：[Tahirpathan-AiLab/Evaan_Personal_Intelligence_Engine](https://github.com/Tahirpathan-AiLab/Evaan_Personal_Intelligence_Engine) · 归类：记忆层与个人 AI 基础设施 · 本页基于 2026-08-25 的上游 README、仓库目录与 GitHub API 快照整理。

## 定位

`Evaan_Personal_Intelligence_Engine`（上游将助手称作 Evaan）是一个单机、CPU 优先的个人陪伴式聊天机器人示例。它用 Python、PyTorch、Transformers 和 Qwen2.5-0.5B-Instruct，把系统提示词、规则式语气检测及 JSON 会话文件组合成可跨重启保留近端对话的终端程序；首次下载模型后，日常推理不要求 API key 或网络。

API 快照：10 stars、0 forks、0 个开放 issue；创建于 2026-08-24；API 未声明 SPDX 许可证。它是早期公开开发者信号，既非 GitHub Trending 排名，也不能验证“CPU 轻量”“隐私友好”或陪伴质量等上游主张。

## 用法

先在隔离目录、非敏感账户和受控的本地模型缓存中检查代码与依赖，再运行上游的主脚本。上游 README 未提供锁定的安装清单，以下命令是基于其说明的最小起点，实际版本应自行锁定：

```sh
git clone https://github.com/Tahirpathan-AiLab/Evaan_Personal_Intelligence_Engine.git
cd Evaan_Personal_Intelligence_Engine
python -m venv .venv
source .venv/bin/activate
python -m pip install torch transformers
python evaan_chat.py
```

程序的 `/save`、`/history`、`/mood`、`/clear` 及 `quit` / `exit` 命令会操作本地会话状态。首次模型下载、模型许可、磁盘占用和实际 CPU 内存需在目标机器上记录；不要将含私人对话的 `evaan_memory.json` 提交、同步或用于训练。

## 原理

- 启动时加载 JSON 中保存的会话、心情和计数器，再读取 Qwen2.5-0.5B-Instruct tokenizer 与权重；每轮把最近最多 20 条消息和 persona system prompt 送入生成器。
- 正则规则检测英文与 Hindi/Hinglish 的斥责或道歉词，并据此更新 mood 指令；这不是情感识别模型，也不能从少量关键词可靠判断用户状态。
- 对“你是谁 / 谁创建你”等固定身份问题，代码以硬编码回答绕过模型；其他回答使用温度、top-p、重复惩罚和最多 50 个新 token 的采样生成。
- 每轮将裁剪后的上下文写回 JSON。该机制提供的是本地、明文、近期历史的持久化，而不是检索增强、长期事实记忆、加密存储或多用户隔离。

## 价值

- 将 persona、状态、上下文裁剪和本地推理放在一个小型可读实现中，适合学习“提示词加状态”如何形成连续对话体验。
- 不依赖云端 API 的日常调用，便于在离线实验机上观察小模型、采样参数和上下文窗口之间的取舍。
- 明确将保存的会话文件作为程序工件，便于另行加入加密、过期策略、摘要或评测，而不是把“有记忆”当作黑箱能力。

## 风险边界

- API 未声明许可证；在复制、分发、修改或把代码接入产品前，必须以仓库实际文件和权利人说明独立确认许可，不能仅按“公开仓库”处理。
- JSON 会话是明文敏感数据，且项目没有显示加密、访问控制、删除验证、备份隔离或多用户边界；本地运行不自动等于隐私合规。
- 规则式语气检测和 persona prompt 不能提供心理健康判断、身份真实性、事实准确性或安全保障；陪伴型输出也不应替代专业支持。
- 小模型在 CPU 上的速度、内存、输出质量和语言覆盖依赖硬件、模型 revision、依赖版本与 prompt；README 自述不能替代基准或对抗测试。

## 补充建议

1. 用虚构对话建立最小回归集，分别测试重启恢复、`/clear`、损坏 JSON、上下文裁剪和身份问题分流；验证删除后没有残留副本再处理真实数据。
2. 将模型 revision、哈希、Transformers/PyTorch 版本、CPU、内存和每轮延迟记录为实验元数据，并固定采样参数比较质量。
3. 为敏感主题加明显的人工转介、危机提示和数据告知；不要用 regex 结果推断情绪、风险或用户意图。
4. 若需长期记忆，先设计数据最小化、加密、访问控制、导出/删除和注入防护，再考虑摘要或检索层。

## 参考资料

- [上游 README / 工作流与功能说明](https://github.com/Tahirpathan-AiLab/Evaan_Personal_Intelligence_Engine)
- [GitHub API 元数据](https://api.github.com/repos/Tahirpathan-AiLab/Evaan_Personal_Intelligence_Engine)
- [Hugging Face Transformers 文档](https://huggingface.co/docs/transformers/)
- [Qwen2.5-0.5B-Instruct 模型页](https://huggingface.co/Qwen/Qwen2.5-0.5B-Instruct)
