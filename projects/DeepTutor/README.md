<!-- markdownlint-disable MD013 -->

# DeepTutor：知识、练习与长期学习共用的 Agent 工作区

- 主上游：[HKUDS/DeepTutor](https://github.com/HKUDS/DeepTutor)；repository ID `1124219907`。
- 采样日期：2026-10-28（Asia/Shanghai）；分类：AI 学习与教育资源。
- API 累计快照：45,771 stars / 5,745 forks / 217 open issues（含 PR 口径），与榜单日增分开。
- 默认分支 `main`；主线依据固定在 `a31d82624c27d75f4e771d4fcb78dce16470b383`。发行 API 首项 [v1.6.15](https://github.com/HKUDS/DeepTutor/releases/tag/v1.6.15)，UTC 2026-10-18T20:13:23Z，正式发行标记。
- 核验层级：一手文档、元数据和所列部分实现的静态阅读；未安装运行、调用模型、复现基准或验证真实用户效果。

## 定位

DeepTutor 将问答、求解、出题、研究、可视化、掌握路径、沉浸阅读和音频概览接入同一学习工作区。它还能连接知识库、书籍、笔记、记忆和外部 Agent。本页在原有 2026-04-11 建档基础上更新，替换旧安装 / 架构状态；历史观察仍可从仓库版本历史追溯。

## 用法

当前主线全应用 PyPI 安装要求 Python 3.11–3.14 与 Node.js 20+，源码开发建议 Node.js 22 LTS。以下在专用环境 / 运行目录执行，先配置低额度模型与合成资料：

```bash
python -m pip install -U deeptutor
deeptutor init
deeptutor start
```

前端默认 3782、后端默认 8001，以启动输出为准；初始设置包含 LLM、可选 embedding 和搜索。主线还提供 Docker 与源码安装，CLI-only 包目前应从 `packaging/deeptutor-cli` 源码安装，不能把完整应用和 CLI-only 的分发状态混写。滚动安装不固定版本；复现时应选择并锁定发行 / 依赖。本文未安装或配置账号。

## 原理

统一 capability runtime 与 session context 调度不同学习任务；知识库提供可检索材料，L1 traces、L2 摘要与 L3 synthesis 组成可查看的记忆层。RAG 有多种可选引擎，工具、MCP、CLI Apps 和社区 skills 扩展执行能力；每个接入的模型、索引与工具仍有独立的数据和授权边界。

## 价值

适合研究跨会话学习资料复用、练习与反馈，以及 Web / CLI 共用的能力架构。引用、记忆图和掌握路径有助于审阅学习过程；这些机制本身不能证明解释正确、评分公平或教学效果优于现有方法。

## 风险边界

- 工作区隔离文档区分“材料 / 会话 / 进度随 workspace”与“memory、credentials、account settings、workspace registry 保持全局”。文档自述曾完成上游测试不等于本库本轮重验，也不能将工作区切换视为清空全局信息。
- Office skills 会运行模型生成的代码。README 描述优先 runner sidecar，再选 Linux bubblewrap，最后在允许时使用受限 subprocess；`sandbox_allow_subprocess` 默认 true。文件作用域、账号隔离和 OS 执行隔离是不同控制。
- 可选 fastapi-guard 默认关闭；开启后也不扫描请求 body / prompt，不处理 WebSocket handshake，SSRF 模式另被禁用；不能把它当作 prompt injection 或所有网络路径的防护。
- 外部模型、搜索、文档解析、远程 RAG 与 IM Partners 都可能发送数据；社区技能入口的扫描 / provenance 不替代人工审查和宿主最小权限。
- v1.6.15 是本轮发行 API 首项，main 还在变动；学习者 / 监护人策略、插件与迁移功能需按部署版本实测。Apache-2.0 不覆盖所有接入服务条款。

## 补充建议

先用同一份公开教材构建可核答案与引用的测试集，逐个验收检索、求解、题目评分和失败恢复。多用户部署再检查跨账号 / 工作区访问、全局记忆、导出 / 迁移与执行后端；教学试验另记录前后测与人工评价。

## 参考资料

- [README.md](https://github.com/HKUDS/DeepTutor/blob/a31d82624c27d75f4e771d4fcb78dce16470b383/README.md)。
- [docs-for-user/SECURITY_GUARD.md](https://github.com/HKUDS/DeepTutor/blob/a31d82624c27d75f4e771d4fcb78dce16470b383/docs-for-user/SECURITY_GUARD.md)。
- [docs-for-user/workspace-isolation-implementation.md](https://github.com/HKUDS/DeepTutor/blob/a31d82624c27d75f4e771d4fcb78dce16470b383/docs-for-user/workspace-isolation-implementation.md)。
- [pyproject.toml](https://github.com/HKUDS/DeepTutor/blob/a31d82624c27d75f4e771d4fcb78dce16470b383/pyproject.toml)。
- [LICENSE](https://github.com/HKUDS/DeepTutor/blob/a31d82624c27d75f4e771d4fcb78dce16470b383/LICENSE)。
- [仓库 API](https://api.github.com/repos/HKUDS/DeepTutor)、[发行 API](https://api.github.com/repos/HKUDS/DeepTutor/releases?per_page=1)；动态字段只代表本轮采样。
- 事实依据为以上一手材料；价值、风险推论与补充建议为本库工程分析。
