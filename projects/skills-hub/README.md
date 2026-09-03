<!-- markdownlint-disable MD013 MD034 -->

# Skills Hub：集中安装并同步多种 Coding-Agent Skills 的桌面管理器

## 项目概览

- 上游仓库：https://github.com/qufei1993/skills-hub
- GitHub API 快照（2026-09-04）：1,562 stars、172 forks、5 个开放 issue
- 当前 release：`v0.9.1`
- 主要技术：Tauri 2 / Rust、React、中央 skills 仓库、symlink/junction/copy、多工具适配
- 许可证：MIT

## 定位

Skills Hub 把分散在 Claude Code、Codex、Cursor、OpenCode、Antigravity 等工具目录中的 Agent Skills 收进一个中央库，再按全局或项目范围同步到多个宿主。

它解决的是 skills 的发现、来源、版本和部署状态管理，不会判断 skill 是否安全、事实正确或适合当前任务。

## 用法

桌面端可从 Explore、Git 仓库、本地目录或已有工具目录导入 skill，默认中央仓库位于 `~/.skillshub`。选定 tags、scope 和目标工具后，应用优先用 symlink/junction，同步受限时回退到 copy。

源码开发要求 Node.js 18+、Rust stable 与 Tauri 系统依赖：

```bash
npm install
npm run tauri:dev
```

macOS README 明示当前构建可能未签名/未 notarize；不应把 `xattr -cr` 当作常规安全建议，首次使用宜从源码或受控 release 做独立核验。

## 原理

中央库保存每个 skill 的内容、来源、标签、作用域和目标工具。tool adapter 维护各宿主的全局/项目 skills 路径；同步层选择链接或复制，并支持批量启停、导入、Git/local source 更新和系统级定时任务。

这种模型减少重复副本，但中央源被污染或自动更新失控时，也可能同时影响多个 agent 宿主。

## 价值

- 统一查看 47 个内置工具适配器与自定义目录的 skills 状态。
- 中央存储、来源信息和批量操作降低手工复制与版本漂移。
- 支持项目级和全局作用域，便于把通用 skill 与仓库特定规则分开。
- 可预览 `SKILL.md`、README 和代码片段，再决定是否同步。

## 风险边界

- Skill 是可执行行为指令；恶意或被接管的上游可诱导 agent 读取数据、运行命令或扩大权限。
- 自动更新和批量同步会扩大 blast radius；链接与复制模式还会产生不同的更新、回滚和删除语义。
- GitHub token、代理、Git clone/fetch、在线搜索和 curated list 都是网络与供应链边界。
- README 只把 macOS 标为已验证，Windows/Linux 是设计预期；不能把跨平台表格当作实测兼容性。
- 绕过 Gatekeeper 属性检查会移除隔离标记；安装未签名构建前应核验来源、hash 和构建链。
- 本页依据上游 README、release 与 API，未安装或执行定时同步。

## 补充建议

1. 默认关闭自动更新，只在 review queue 中检查 upstream commit、`SKILL.md` 与脚本 diff。
2. 先导入无副作用的只读 skill，分别验证 symlink、copy、禁用、删除和回滚语义。
3. 给中央库和 GitHub token 做最小权限、备份、审计和离职/换机回收。
4. 将 skill 安全扫描、来源 allowlist 和版本 pin 设为批量部署前置 gate。
5. 在 macOS 优先自行构建或等待可验证签名版本，不盲目移除 quarantine。

## 参考资料

- 仓库与 README：https://github.com/qufei1993/skills-hub
- Releases：https://github.com/qufei1993/skills-hub/releases
- 中文说明：https://github.com/qufei1993/skills-hub/blob/main/docs/README.zh.md
- 工具路径适配：https://github.com/qufei1993/skills-hub/blob/main/src-tauri/src/core/tool_adapters/mod.rs
- Security policy：https://github.com/qufei1993/skills-hub/blob/main/SECURITY.md
