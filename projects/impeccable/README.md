<!-- markdownlint-disable MD013 -->

# impeccable

## 定位

Impeccable 为 coding agent 提供设计词汇、技能命令和确定性检测器，主线已经从旧页的多目录复制流程发展为统一安装、项目上下文、24 个命令及 live 迭代。2026-03-25 旧页在此原位刷新，避免按同一上游重复建档。

2026-10-30 快照：综合 / Rust daily +2,881 stars；API 累计 95,212 stars / 5,610 forks / 45 open issues（含 PR）。核读 main `02523aec3e4c`；发行 API 首项 [skill-v4.8.0](https://github.com/pbakaus/impeccable/releases/tag/skill-v4.8.0)，2026-10-26 UTC。以下为文档与有限源码核读，未安装运行。

## 用法

在准备修改的项目根目录审阅安装器后运行上游入口：

```bash
npx impeccable install
```

重载宿主后初始化项目；Codex 文档入口是 $impeccable init，其他宿主可用 /impeccable init。先选一个组件运行 critique / audit，再决定修改。init 写 PRODUCT.md，document 写 DESIGN.md。本文介绍上游用法，未安装或批准任何 hook。

检测器可单独执行 npx impeccable detect src/ 或扫描自己的本地开发 URL。退出 2 表示有 findings，1 表示目标不能扫描；源码和浏览器扫描覆盖不同规则。

## 原理

技能把设计动作拆成可组合命令并读取产品 / 视觉上下文；detector 用 62 条确定性规则检查模式，源码扫描偏语法，渲染扫描补充对比度和字号。live overlay 可选择页面元素、生成变体并把接受结果写回源码，不同层分别依赖宿主模型、浏览器与本地引擎。

## 价值

给设计沟通与回归检查建立共同词汇，减少“再好看一点”的模糊反馈。适合对已有组件做窄范围迭代，同时将例外写入带理由的 ignore；作者示例不构成跨任务效果评测。

## 风险边界

- 根 Apache-2.0。旧页中 20 命令、dist/ 复制路径及 3 月热度已过时；当前主线 24 命令含已弃用 craft 别名，发行 skill-v4.8.0 与 main 仍需区别。
- skill 使用模型与宿主工具；只有确定性 detector 的相关路径不需 LLM / API key，不能把整套设计流程说成无模型或完全离线。
- 安装可写 hook 并下载引擎；README 特别说明 Claude Code command hooks 可能在模型命令被拒绝时仍运行。Codex 项目 hook 另需宿主信任，先核已安装项。
- live mode 只应用于本地 checkout；手动文案应用可运行 package.json 的 impeccable:manual-edit-validate，以用户权限执行。
- 关闭 telemetry 仍会请求 visual directions catalog；关闭匿名选择记录不等于零联网。README 的字段排除声明未在本轮抓包验证。
- 规则命中、模型 critique 分数与可访问性 / 产品效果不同。品牌字体可能合理，需要有理由的例外和真实浏览器 / 用户检验。

## 补充建议

先固定版本，检查安装 diff 与 hook 内容，运行源码加本地 URL 两种扫描；核对键盘操作、移动端、对比度、字体授权及真实文案。分别保留自动规则结果、人工设计判断和页面截图，不能用编译成功替代视觉验收。

## 参考资料

- [上游仓库](https://github.com/pbakaus/impeccable)、[仓库 API](https://api.github.com/repos/pbakaus/impeccable)。
- [README.md](https://github.com/pbakaus/impeccable/blob/02523aec3e4c4580102d996d1b6a71fbe062e03f/README.md)。
- [LICENSE](https://github.com/pbakaus/impeccable/blob/02523aec3e4c4580102d996d1b6a71fbe062e03f/LICENSE)。
