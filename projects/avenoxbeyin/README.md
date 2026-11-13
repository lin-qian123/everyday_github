<!-- markdownlint-disable MD013 -->

# AvenoxBeyin：以 Markdown 为源的跨客户端第二大脑

- 上游：[`avenoxai/avenoxbeyin`](https://github.com/avenoxai/avenoxbeyin)；仓库 ID：`1284449744`。
- 核读：2026-11-14（Asia/Shanghai）；主线固定于 [`db1b17c2a09f`](https://github.com/avenoxai/avenoxbeyin/tree/db1b17c2a09fb99d0cf5e32b1ab57dec62e1fe9d)。
- 热度快照：445 stars / 75 forks / 38 open issues（含 PR）；来自 [GitHub API](https://api.github.com/repos/avenoxai/avenoxbeyin)，不代表采用量或质量。

## 定位

AvenoxBeyin（İkinci Beyin，土耳其语“第二大脑”）用本地 Markdown 保存笔记、任务、决定和工作结果，以本地索引向不同 AI 客户端提供来源上下文；Obsidian 可选。它不是模型，也不会自动将全部聊天变成已核知识。

Python daily +46；稳定 [v3.13.0](https://github.com/avenoxai/avenoxbeyin/releases/tag/v3.13.0) 于 UTC 11-12 发布，增加可选 Yakala → Claude / Codex 交接、Pi / OpenCode 接入与本地 Web。

## 用法

需要 Python 3.11+ 与已配置客户端。按 release 下载 `beyin-v3-X.Y.Z.zip` 及旁边 SHA-256 文件，核对后解压；README 明确不使用 GitHub Source code 压缩包。在解压的正式包目录执行：

```bash
python scripts/install_v3.py --vault "/absolute/path/to/vault"
```

安装会写 runtime、skills 与客户端 hook / 配置；先备份、审阅目标和 hook，再开新会话。用合成决定做“保存 → 检查源 Markdown → 新会话检索并打开来源”验证，本轮未安装。

`python beyin.py doctor` 查连接，`python beyin.py update --check` 查版本。Yakala 捕获、全局 bridge 和 Web 是独立可选入口；Web 可先用 `python beyin.py web ac --read-only`。

## 原理

Markdown 是权威源，词法索引、短 hook、队列和 receipt 组织刷新与检索；任务更新检查 revision / source hash。receipt 是 Agent 对工作的历史声明，不是独立验收。V3 不默认使用 embedding、Mem0 或后台模型知识编译器。

基础安装仅接 vault 内会话；可选 bridge 将明确选择的项目根目录接到记忆。Yakala 默认 Enter 只保存卡片，另开 Agent 模式后才用 Ctrl+Enter 交接，捕获与执行是两步。

## 价值

适合跨客户端保留可编辑、可追溯决定和任务；切换宿主后仍能直接查源文件。哈希和冲突信息利于发现过时上下文，但词法命中不能保证语义召回。

## 风险边界

- 本地记忆描述存储与检索；选中上下文会交给 AI 客户端，模型与账号条件仍适用。private 标记约束工具注入 / Web 过滤，不能阻止已有文件权限的其他 Agent 读取。
- bridge 会改用户级 hook / 插件，`--project-root` 包含子目录；先审阅具体写入、范围和卸载路径，避免把整个 home / 磁盘纳入。
- 上游真实客户端检查是有限、历史合成场景；明确记录 Codex CLI 控制成功，而 Desktop app-host 自动 hook 未交付，不能写成全部客户端自动注入已验证。
- Web 显式开启、仅绑定 127.0.0.1、30 分钟空闲关闭；文档说明 token、cookie 与 CSRF，也承认 cookie 不隔离端口，同机其他本地 server 仍在信任面内。
- Yakala 涉及剪贴板、浏览器、文件和可选截图；OS 权限、外部内容注入与后续模型发送须分别检查，安装监听器与保存卡片不是同一权限动作。
- 基础检查不调用模型，版本提示每天最多查一次 GitHub，Jev 顾问默认关闭；可选捕获、下载和 Agent 交接的数据出口另算。
- MIT 项目许可不替代客户端条款；checksum 检查包对应性，不能独立证明来源或执行安全。

## 补充建议

从合成 vault 开始，准备普通、private、过期与冲突笔记，逐客户端核查新会话返回的来源和状态。将 hook 自动注入、显式 skill、任务写入与 Web 分别验收；先确认备份、update / rollback 冲突处理，再用真实资料或多机同步。

本页为静态文档核读；未安装 runtime、改用户 hooks、采集剪贴板、接模型、启动 Web 或迁移笔记。

## 参考资料

- [定位、安装与本地边界](https://github.com/avenoxai/avenoxbeyin/blob/db1b17c2a09fb99d0cf5e32b1ab57dec62e1fe9d/README.md)。
- [V3 架构与验证](https://github.com/avenoxai/avenoxbeyin/blob/db1b17c2a09fb99d0cf5e32b1ab57dec62e1fe9d/docs/v3/README.md)。
- [客户端与 Desktop hook 缺口](https://github.com/avenoxai/avenoxbeyin/blob/db1b17c2a09fb99d0cf5e32b1ab57dec62e1fe9d/docs/v3/LIVE-CLIENTS.md)。
- [全局桥接](https://github.com/avenoxai/avenoxbeyin/blob/db1b17c2a09fb99d0cf5e32b1ab57dec62e1fe9d/docs/v3/GLOBAL-BRIDGE.md)。
- [Web 本机信任边界](https://github.com/avenoxai/avenoxbeyin/blob/db1b17c2a09fb99d0cf5e32b1ab57dec62e1fe9d/docs/v3/WEB.md)。
- [捕获与交接](https://github.com/avenoxai/avenoxbeyin/blob/db1b17c2a09fb99d0cf5e32b1ab57dec62e1fe9d/docs/v3/YAKALA.md)。
- [MIT 许可](https://github.com/avenoxai/avenoxbeyin/blob/db1b17c2a09fb99d0cf5e32b1ab57dec62e1fe9d/LICENSE)。
