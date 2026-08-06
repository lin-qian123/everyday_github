<!-- markdownlint-disable MD013 -->

# macos-disk-cleanup

- 仓库：[himynameisben/macos-disk-cleanup](https://github.com/himynameisben/macos-disk-cleanup)
- 快照：2026-08-07 抓取；GitHub API 显示其创建于 2026-08-06，约 20 stars、0 forks，MIT。数字会随时间变化。
- 分类：Agent 框架与技能生态

## 定位

供 Claude Code、Codex 等 coding agent 使用的 macOS 磁盘诊断与清理 skill。它针对 Finder 中难解释的“系统数据”，提供唯读占用扫描、缓存/孤儿 container/稀疏文件识别，以及对潜在删除项的三档风险规则。

## 用法

可按 README 将仓库放入对应 agent 的 skills 目录；不安装 skill 时也可仅执行仓库的 `scripts/disk_scan.sh` 或 `scripts/disk_scan.sh --deep` 进行唯读检查。若 agent 提出删除动作，先核对完整路径、大小、内容和备份，再逐项人工确认；不要把诊断脚本的输出直接当作删除清单。

## 原理

脚本枚举用户目录、Library、Xcode/Simulator 与常见包管理器缓存，比较稀疏文件的逻辑大小和实际占用，并按“可重建缓存 / 可重新下载 / 可能是唯一用户数据”划为 SAFE、CONFIRM、DANGER。README 专门提示 container 中的符号链接、APFS snapshot 与异步删除会造成直觉误判。

## 价值

它把容易被忽略的开发缓存与 macOS 专属陷阱写成可复用的 agent 约束，尤其适合作为空间排障的只读第一步。明确分级和预览内容的流程，能减少“让 agent 一键腾空间”的冲动操作。

## 风险边界

该项目的核心动作最终仍可能删除文件，且分类规则不是操作系统强制保护；扫描结果可能因权限、符号链接、APFS snapshot 或应用行为而失真。绝不能在没有可恢复备份、路径核验和人工批准的情况下运行任何清理命令，也不应由 agent 自主处理 Documents、聊天记录、钥匙串、容器数据或未知目录。

## 补充建议

先记录 `df`、Time Machine/备份状态与只读扫描结果，优先清理可重新生成且已确认的缓存；一次只处理一类目标并重新测量空间。对大文件和 container 先用 `ls -la`/Finder 确认是否为 symlink 或用户资料，重要删除改用可恢复的废纸篓/快照流程。

## 参考资料

- [项目 README](https://github.com/himynameisben/macos-disk-cleanup)
- [陷阱清单](https://github.com/himynameisben/macos-disk-cleanup/tree/main/references)
- [GitHub API 元数据快照](https://api.github.com/repos/himynameisben/macos-disk-cleanup)
