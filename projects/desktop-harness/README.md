<!-- markdownlint-disable MD013 -->

# desktop-harness

- 仓库：[xfreeze2/desktop-harness](https://github.com/xfreeze2/desktop-harness)
- 快照：2026-08-11 抓取；GitHub API 显示其创建于 2026-08-10，约 10 stars、3 forks，MIT。数字会随时间变化。
- 分类：Coding Agents 与终端助手

## 定位

面向 macOS 的本地 CLI 与 agent skill，给 Grok Build、Codex、Claude Code 等能执行 shell 的 agent 提供桌面控制。它优先读取 Accessibility（AX）树，以 AXPress/设值完成交互，必要时才退回截图与真实鼠标键盘事件。

## 用法

克隆仓库后运行 `./install.sh`，再按文档在系统设置中为终端或 agent host 授予辅助功能权限；若需截图，还要授予屏幕录制权限。安装后先执行 `desktop-harness selftest` 和 `--doctor`，再在非敏感窗口中用 `labels()` 等只读能力验证可见控件；skill 安装路径和更完整命令见项目 README。

## 原理

工具先判断任务能否由 shell 解决；GUI 场景优先消费系统 AX 语义树和动作接口，因此不必让视觉模型反复从像素猜坐标。AX 信息不足时才用窗口截图及 `CGEvent` 输入；可选常驻 daemon 减少多步任务中 Python/pyobjc 的启动成本。

## 价值

对标准 macOS 控件，语义优先路径更可检查、延迟更低，也比纯视觉点击更容易写确定性 smoke test。它为“agent 控制桌面”提供了明确的命令边界，而非隐藏在 GUI 宏中。

## 风险边界

辅助功能和屏幕录制权限可让运行该 CLI 的 host 读取窗口内容并代表用户点击、输入；恶意提示、错误窗口焦点或无障碍树不完整均可能造成误操作。项目不提供 OS 级安全边界，安装脚本与每次更新都应审阅；不可向 agent 交出密码、金融、发布或生产运维界面。

## 补充建议

用专用 macOS 账户、最小权限 app 白名单和独立浏览器 profile 试用。把窗口标题/应用 bundle ID 断言、破坏性动作二次确认和操作日志设为默认，并在升级前重新运行自测；优先调用目标应用的 API 而非 GUI 自动化。

## 参考资料

- [项目 README 与安装文档](https://github.com/xfreeze2/desktop-harness)
- [GitHub API 元数据快照](https://api.github.com/repos/xfreeze2/desktop-harness)
