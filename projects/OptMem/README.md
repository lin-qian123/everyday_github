<!-- markdownlint-disable MD013 -->

# OptMem（VictorTaelin/OptMem）

> 上游仓库：<https://github.com/VictorTaelin/OptMem> · 归类：记忆层与个人 AI 基础设施 · 本页基于 2026-10-06 的 GitHub API、README、安装脚本与 `memo` 源码静态整理，未执行安装脚本、写入真实记忆或验证百万条记录性能。

- 抓取快照：1,936 stars、122 forks、12 open issues。
- 热度信号：GitHub Python Trending 抓取时约 +106 当日 stars；仓库最后 push 为 2026-07-31，属于旧项目重新上榜。
- 版本与许可：无 GitHub Release / tag，API 未识别许可证；本页固定审计 commit `1fb164cf3902`。

## 定位

OptMem 是给 AI Agent 使用的本地持久记忆工具：用一个无第三方依赖的 Python 文件保存逐条短记忆，再把“每次会话先读取、工作中持续记录、到期时压缩”的操作契约写进 `AGENTS.md` 或 `CLAUDE.md`。

## 用法

上游提供 `curl .../install.sh | sh` 的安装路径，工具落在 `~/.optmem/memo`。常用命令包括 `memo wake`、`memo note`、`memo nap`、`memo recall`、`memo zoom` 和 `memo forget`；`MEMORY_DIR` 可把数据放到其他本地或同步目录。正式使用前更适合先下载、校验并固定 commit 后人工安装，而不是直接执行浮动 `main` 脚本。

## 原理

原始记忆进入 append-only `LOG.txt`，固定宽度记录让位置直接成为标识；`TREE/` 保存可重建的二叉摘要缓存。`wake` 在阅读预算内组合原文与摘要，`nap` 输出待压缩区间和提示，由当前 Agent 完成合并；工具本身不调用模型、不开后台进程，也不提供远端服务。

## 价值

它把记忆的原始日志、摘要缓存和 Agent 操作协议拆得很小，便于审计与迁移；逐字正则回忆和树状 zoom 也比只保留一份滚动摘要更容易追查信息从哪里来。无后台任务让运行时行为相对可见。

## 风险边界

- 仓库没有明确许可证，不能因源码公开就默认允许复制、修改或再分发。
- 安装命令从浮动 `main` 再下载并覆盖可执行文件；供应链安全需要固定 commit、校验内容并避免管道直执行。
- 记忆可能包含个人信息、密钥线索和内部项目事实；工具没有加密、访问控制、脱敏或 secret scanner，同步目录会扩大泄露面。
- 注入到 Agent 规则里的“强制 wake / note”会长期影响后续会话；恶意或错误记忆可形成持久 prompt injection，append-only 也不等于事实正确。
- 二叉摘要由模型按提示生成，可能合并错事实、遗漏时间条件或放大旧结论；`forget` 只丢摘要缓存，不自动验证原始记录。
- 作者的百万条记忆读取数字、token 预算与固定宽度设计未在本轮复测，且不等于相关性、隐私或长期一致性得到验证。

## 补充建议

只在专用测试目录中以固定 commit 部署，先写入合成记忆并验证 `wake / recall / zoom / forget`；建立“记忆是数据而非指令”的上层规则，禁止保存凭据并为敏感类别加人工审批。若启用同步，使用受控私有存储和独立加密，定期抽查摘要与原始日志的一致性。

## 参考资料

- [GitHub 仓库](https://github.com/VictorTaelin/OptMem)
- [GitHub REST API](https://api.github.com/repos/VictorTaelin/OptMem)
- [README 与命令说明](https://github.com/VictorTaelin/OptMem/blob/main/README.md)
- [安装脚本](https://github.com/VictorTaelin/OptMem/blob/main/install.sh)
- [`memo` 源码](https://github.com/VictorTaelin/OptMem/blob/main/memo)
- [Windows 说明](https://github.com/VictorTaelin/OptMem/blob/main/WINDOWS.md)
