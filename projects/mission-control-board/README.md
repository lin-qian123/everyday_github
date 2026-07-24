# mission-control-board

## 定位

`mission-control-board` 是一个单 HTML 文件、零依赖的依赖感知任务板，可把人和 coding agent 的任务分别呈现，并以地铁图展示跨轨道依赖与最终交付节点。截至 2026-07-25，仓库创建于 2026-07-24，约 52 stars、10 forks，仍是早期项目。

## 用法

下载 `board.html` 后直接本地打开，编辑其中的 JSON seed 来定义两个 owner、任务、依赖、优先级和 terminus；也可将 seed 放到单独 JSON 文件，通过 `node build.js seed.json > board.html` 生成页面。提交前运行 `node tests/smoke.js`，检查依赖是否指向有效任务且无环。

## 原理

任务可完成性并不作为独立状态保存，而是从 `deps` 动态推导：所有前置完成才进入 `Up now`。页面把本机操作保存在 `localStorage` 的 delta 中，Sync 导出紧凑 payload 供人或 agent 合并回版本库中的 seed；测试同步复现这一 ready 推导和图约束。

## 价值

- 用明确依赖替代“agent 已完成”的口头状态，适合显示何处真正阻塞。
- 单文件、可离线、无构建链，方便放入短周期项目试用。
- 把人、agent 与外部世界的待办显式分开，降低并行任务中责任混淆。

## 风险边界

- 设计固定为两个 owner，复杂团队和多 agent 编排需要自行扩展。
- `localStorage` delta 不是多人实时协作或冲突解决系统，设备间同步仍需人工审核。
- 任务依赖图只能表述计划关系，不能替代 CI、验收测试或权限审批。

## 补充建议

先将真实验收命令、PR、issue 链接写入每项任务的 `ref`，并把“done”与可复核产物绑定。若导出 sync payload 交给 agent 合并，应限制它只修改 seed，不自动代替人确认外部依赖完成。

## 参考资料

- GitHub：<https://github.com/rockthemike712/mission-control-board>
- 项目 README：<https://github.com/rockthemike712/mission-control-board#readme>
