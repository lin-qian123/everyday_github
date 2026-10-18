<!-- markdownlint-disable MD013 -->

# LazySkills

> 更新：2026-10-19（Asia/Shanghai）。分类：Agent 框架与技能生态。上游 `alvinunreal/lazyskills`；本文基于官方榜单、认证 API 与文档 / 源码静态核验，未安装运行。源码快照 `4ce98ca91650`；Release 与主分支行为分别说明。热度见[当日官方榜单](https://github.com/trending/go?since=daily)。

## 定位

Go 编写的 agent skills 管理 TUI：把项目级、全局、通用与特定 agent 目录合并展示，识别缺失 SKILL.md、frontmatter、坏 symlink、lock 缺项与不可见技能；同时提供搜索、安装、更新、删除与恢复入口。[来源 1](https://github.com/alvinunreal/lazyskills/blob/4ce98ca91650d3a0154cd93bbed50fd65771f7b4/README.md)

官方 Go Trending 约 +107 当日 stars；API 为 555 / 70 / 8（stars / forks / open issues）；最新稳定 Release v1.2.0，MIT。README 同时有“star 抽贴纸”活动，因此增星也可能受活动影响，不能全部解释为实际使用者增长。[来源 1](https://github.com/alvinunreal/lazyskills/blob/4ce98ca91650d3a0154cd93bbed50fd65771f7b4/README.md)[来源 2](https://api.github.com/repos/alvinunreal/lazyskills)[来源 3](https://github.com/alvinunreal/lazyskills/releases/tag/v1.2.0)

## 用法

可从 v1.2.0 Release 选择对应平台制品，或依上游 Homebrew / Go 说明安装。当前 main 的 go.mod 声明 Go 1.26.3，源码构建需检查本机工具链。[来源 3](https://github.com/alvinunreal/lazyskills/releases/tag/v1.2.0)[来源 4](https://github.com/alvinunreal/lazyskills/blob/4ce98ca91650d3a0154cd93bbed50fd65771f7b4/go.mod)

```bash
# 首次只看只读健康报告
lazyskills doctor --json
# 按 agent 需求发现候选
lazyskills find --json "browser automation"
```

TUI 中 `a` 切 agent、`f` 切作用域、Enter 看细节；安装或更新前审命令与目标目录。restore 会安装 lock 记录但磁盘缺失的技能，`--yes` 可跳过确认，本轮没有运行上述命令或修改任何技能。

## 原理

扫描目录和 lock metadata，计算技能来源、作用域、agent 可见性与健康状态，再把操作转成明确外部命令执行。doctor 是只读路径；restore 在预览后和每次安装前重扫 / 重验身份与命令，发现变化即停，可能已有部分技能恢复。[来源 1](https://github.com/alvinunreal/lazyskills/blob/4ce98ca91650d3a0154cd93bbed50fd65771f7b4/README.md)[来源 5](https://github.com/alvinunreal/lazyskills/blob/4ce98ca91650d3a0154cd93bbed50fd65771f7b4/cmd/lazyskills/restore.go)

这解决的是技能安装状态与发现问题；“可见”只说明符合其扫描规则，不证明 agent 实际正确加载或遵守技能。

## 价值

多 agent、多目录用户可用一个界面找出“文件在但 agent 看不到”等安装问题，减少盲目重装。结构化 doctor 输出也便于做工作区检查；效果还需和真实 agent 的技能枚举结果交叉核对。

## 风险边界

- 技能内容、安装脚本和依赖仍是第三方代码 / 指令，预览与确认不能证明安全。全局安装会扩大影响面。
- 更新 / 删除 / prune / restore 会改动技能与 lock；批量失败可能留下部分完成状态，备份和回滚要单独验证。[来源 1](https://github.com/alvinunreal/lazyskills/blob/4ce98ca91650d3a0154cd93bbed50fd65771f7b4/README.md)[来源 5](https://github.com/alvinunreal/lazyskills/blob/4ce98ca91650d3a0154cd93bbed50fd65771f7b4/cmd/lazyskills/restore.go)
- restore 的重复校验缩小并发竞态，上游也明确不是完全 race-free；不能一边运行安装器一边无条件信任预览。
- skills.sh 与 GitHub 搜索结果不保证来源质量、许可或版本不可变。根 MIT 只覆盖本工具，各技能另核条款。[来源 6](https://github.com/alvinunreal/lazyskills/blob/4ce98ca91650d3a0154cd93bbed50fd65771f7b4/LICENSE)
- star 活动属于传播机制，不能据此认定增长造假，也不能把增星直接换算采用率。[来源 1](https://github.com/alvinunreal/lazyskills/blob/4ce98ca91650d3a0154cd93bbed50fd65771f7b4/README.md)

## 补充建议

在复制的测试目录准备一个正常技能、坏 symlink、缺 lock 和同名来源，比较 doctor / TUI 与实际 agent 可见性；再做单项 restore 并检查文件差异。固定来源 commit，先项目级安装，确认后再考虑全局作用域。

## 参考资料

1. [README、使用和贴纸活动](https://github.com/alvinunreal/lazyskills/blob/4ce98ca91650d3a0154cd93bbed50fd65771f7b4/README.md)
2. [仓库 API](https://api.github.com/repos/alvinunreal/lazyskills)
3. [v1.2.0 Release](https://github.com/alvinunreal/lazyskills/releases/tag/v1.2.0)
4. [Go 工具链](https://github.com/alvinunreal/lazyskills/blob/4ce98ca91650d3a0154cd93bbed50fd65771f7b4/go.mod)
5. [restore 执行与重验](https://github.com/alvinunreal/lazyskills/blob/4ce98ca91650d3a0154cd93bbed50fd65771f7b4/cmd/lazyskills/restore.go)
6. [LICENSE](https://github.com/alvinunreal/lazyskills/blob/4ce98ca91650d3a0154cd93bbed50fd65771f7b4/LICENSE)
