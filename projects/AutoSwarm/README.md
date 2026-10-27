<!-- markdownlint-disable MD013 -->

# AutoSwarm：把已有 Agent 接成可跟踪的协作流程

- 主上游：[HKUDS/AutoSwarm](https://github.com/HKUDS/AutoSwarm)；repository ID `1285974683`。
- 采样日期：2026-10-28（Asia/Shanghai）；分类：Agent 框架与技能生态。
- API 累计快照：2,032 stars / 367 forks / 27 open issues（含 PR 口径），与榜单日增分开。
- 默认分支 `main`；主线依据固定在 `5325b6d98dad7a9a12811c0b5fa0817ffbbc71f9`。发行 API 本轮返回空列表；此状态不代表没有源码标签或其他分发渠道。
- 核验层级：一手文档、元数据和所列部分实现的静态阅读；未安装运行、调用模型、复现基准或验证真实用户效果。

## 定位

AutoSwarm 把已安装的 Codex、Claude Code 等 Agent 接到同一对话的委派流程中，负责选择执行者、传递上下文、跟踪任务与汇总结果。本轮主线包为 `2.0.0.dev0`，仓库保留的 `autoswarm-v1.0.0/` 是历史实现；旧版组织算法与论文介绍不能直接当作当前运行方式。

## 用法

需要 Python 3.10+，以及实际要调用的原生 Agent、模型权限和登录配置。固定 checkout 后，可在专用环境按上游入口安装：

```bash
python -m pip install .
autoswarm setup --host codex
autoswarm doctor --agent codex --probe --cwd /path/to/test-project
```

setup 会安装当前宿主的 Skill、运行副本与集成；更新包之后仍需重新 setup，再按返回路径读取新 Skill。`doctor --probe` 会调用模型并检查原生恢复能力，可能计费；仅发现可执行文件或版本号不能证明 Agent 可用。本轮未执行这些命令。

## 原理

通过各宿主支持的原生通信方式启动执行者，例如 Codex app-server、Claude Code 的流式接口；任务记录与原生会话恢复信息用于后续收取结果、处理交互。`providers.py` 转换部分模型、sandbox 和 approval 参数，并保留其他原生命令参数；它不是统一替代所有宿主权限的执行环境。

## 价值

适合已有多套 Agent 配置、希望减少手动转述和收集结果的工作流。统一委派记录有助于审阅分工与失败原因；并行是否更快、更便宜，仍须把协调、重试、重复上下文和最终验收成本一起计算。

## 风险边界

- 子会话能否使用桌面、浏览器登录态、连接器、定时器或图像工具，取决于实际传输与原生权限；桌面 App 有某项能力，不代表 CLI 子会话继承它。
- 共享上下文可能把文件、提示词与秘密送给多个模型或服务。只传任务所需材料，原生认证与工作区权限仍须逐个核对。
- 本地命令支持与任务记录不构成 OS 隔离；多个执行者同时改相同文件会产生冲突，汇总回答也不是独立正确性检验。
- 发行 API 本轮为空，SECURITY 仅声明支持最新 main；应记录 commit。该文件的漏洞报告链接仍指向 HKUDS/OpenOPC，属于文档路径漂移，报告前需另核当前入口。
- MIT 覆盖本仓库代码，底层 Agent、模型与插件服务各有自己的条款。

## 补充建议

先以两个已有执行者完成一个只读任务，记录来源、上下文范围、原生会话 ID、费用和恢复结果；再试互不重叠的文件任务。以交付物与独立检查评估效果，避免用“全部 verified”替代业务验收。

## 参考资料

- [README.md](https://github.com/HKUDS/AutoSwarm/blob/5325b6d98dad7a9a12811c0b5fa0817ffbbc71f9/README.md)。
- [SECURITY.md](https://github.com/HKUDS/AutoSwarm/blob/5325b6d98dad7a9a12811c0b5fa0817ffbbc71f9/SECURITY.md)。
- [src/autoswarm/assets/references/agent-capabilities.md](https://github.com/HKUDS/AutoSwarm/blob/5325b6d98dad7a9a12811c0b5fa0817ffbbc71f9/src/autoswarm/assets/references/agent-capabilities.md)。
- [pyproject.toml](https://github.com/HKUDS/AutoSwarm/blob/5325b6d98dad7a9a12811c0b5fa0817ffbbc71f9/pyproject.toml)。
- [LICENSE](https://github.com/HKUDS/AutoSwarm/blob/5325b6d98dad7a9a12811c0b5fa0817ffbbc71f9/LICENSE)。
- [src/autoswarm/providers.py](https://github.com/HKUDS/AutoSwarm/blob/5325b6d98dad7a9a12811c0b5fa0817ffbbc71f9/src/autoswarm/providers.py)。
- [仓库 API](https://api.github.com/repos/HKUDS/AutoSwarm)、[发行 API](https://api.github.com/repos/HKUDS/AutoSwarm/releases?per_page=1)；动态字段只代表本轮采样。
- 事实依据为以上一手材料；价值、风险推论与补充建议为本库工程分析。
