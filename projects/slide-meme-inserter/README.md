<!-- markdownlint-disable MD013 -->

# slide-meme-inserter

## 定位

`slide-meme-inserter` 是同时面向 Claude Code 与 Codex 的 HTML 演示文稿 skill：它在新建或既有 deck 中规划、检索并克制地插入已有梗图，以帮助转场、类比或回收观点。截至 2026-07-25，仓库创建于 2026-07-24，约 37 stars、0 forks，属于早期开发者信号。

## 用法

Claude Code 可通过仓库 README 给出的 marketplace 命令安装；Codex 可让 agent 从仓库安装 `insert-slide-memes` skill，或手动复制 `skills/insert-slide-memes`。已有 HTML deck 时选择 `postprocess`，从主题和提纲制作时选择 `plan-and-build`；最后运行仓库提供的 `audit_memes.py` 审核 HTML 的结构与资源记录。

## 原理

skill 将梗图限制为 reaction、analogy、callback、transition 等明确叙事角色，先保留原有逻辑和版式，再按受众与语境挑选已知模板。它把资料、玩法说明与审计脚本分离，并让 Claude Code/Codex 复用同一份 `SKILL.md`，以减少两套规则漂移。

## 价值

- 给 HTML 演示的 agent 工作流补上“叙事节奏”这一常被忽略的层。
- 将选图、位置、版权记录与渲染检查变成可重复步骤，而非临场随意贴图。
- 是观察 Codex/Claude Code 跨 runtime skill 分发兼容性的轻量案例。

## 风险边界

- 仓库代码为 MIT，并不授予 meme 图片本身的再使用权；公开演示前须逐项确认授权与平台条款。
- “熟悉的梗”高度依赖语言、文化与受众，可能分散注意力或造成冒犯。
- 审计 HTML 不等于保证浏览器渲染、外链图片可用性或商业发布合规。

## 补充建议

将它用于内部培训、产品 demo 等容错较高的场景，先让人工确认笑点、语境和版权。对正式品牌演示，最好将素材固定到已获许可的本地资产库，并在目标浏览器中做截图 QA。

## 参考资料

- GitHub：<https://github.com/amnotyoung/slide-meme-inserter>
- 项目 README：<https://github.com/amnotyoung/slide-meme-inserter#readme>
