<!-- markdownlint-disable MD013 -->

# Pascal Editor（pascalorg/editor）中文解读

> 证据快照：2026-09-10（Asia/Shanghai）。GitHub REST API 显示 22,876 stars、2,893 forks、48 open issues，MIT；稳定 `latest` 为 `v0.9.1`，仓库同时发布了较新的 CLI / agent-skills 预览构建。本文未安装或运行项目。

## 定位

Pascal Editor 是一个 local-first 的 3D 建筑编辑器，以 React Three Fiber / WebGPU 提供浏览器界面，同时暴露 CLI、MCP 和 agent skills，让人或 AI agent 能围绕建筑场景执行读取、编辑、布局与检查工作。

它更接近“可编程建筑场景工作台”，不是通用图片生成器，也不是已经覆盖法规、结构、机电和施工交付的完整 BIM 审查系统。

## 用法

需要 Node.js 22.13 或更新版本。上游给出的持久本地安装入口是：

```bash
npx @pascal-app/cli editor
```

CLI 会启动编辑器和经过认证的本地 MCP 服务，选择 loopback 端口，并把项目保存到 `~/.pascal/data/pascal.db`。agent 侧可连接 `pascal mcp connect`；skills 可通过 `npx skills add pascalorg/editor --skill pascal-3d --skill furniture-fit` 安装。

若任务依赖仓库最新的 furniture candidate 检查，需先核对 README 指定的 GitHub prerelease、SHA-256 与当前 npm 版本；不能默认稳定 npm 包已包含 main 分支能力。

## 原理

- 3D 编辑层以 WebGPU、Three.js / React Three Fiber 表达可交互建筑场景。
- 本地 CLI 负责服务生命周期、端口、版本与 SQLite 数据目录。
- MCP 把场景操作转成 agent 可调用工具；skills 进一步规定连接检查、场景操作和结果边界。
- README 要求单个本地 CLI service 只连接一个 active agent client；并发独立任务应使用不同 `PASCAL_HOME` 与独立进程，避免共享 active scene state。

## 价值

- 把建筑 3D 场景从只能人工点击的界面变成可脚本化、可由 agent 调用的对象模型。
- 本地编辑器、CLI 与 MCP 可以形成“生成—读取—检查—修正”的可审阅闭环。
- `furniture-fit` 这类窄技能强调只对有证据的 footprint 条件作判断，适合把几何自动化与结论边界一起交付。

## 风险边界

- “local-first”不代表所有使用路径都离线；本地 connector 与 hosted MCP / 账户组织是不同的数据与认证边界。
- 预览包、稳定 release、npm 版本和 main 分支能力不完全同步，安装前必须固定版本并核对 checksum。
- MCP 能操作场景，不等于具备结构安全、消防、无障碍、机电碰撞、材料、成本或当地建筑规范审查能力。
- 平面 footprint 通过不能推出高度、门扇、运输、装配或人体工学均通过；上游 skill 也明确要求收窄结论。
- 共享 service 的 scene state 会让并发 agent 相互影响；认证本身也不能替代最小工具权限和变更回读。

## 补充建议

1. 先在副本项目用固定版本启动本地服务，记录 `pascal --version`、数据目录、MCP schema 与安装包 hash。
2. 为移动、删除、批量生成等写操作设置人工批准，并在每次操作后读取 scene state 或导出物做差异核验。
3. 用已知尺寸的房间和家具建立 golden scenes，分别测试坐标系、单位、碰撞、撤销、并发客户端和版本升级。
4. 把几何结果交给建筑专业人员和法规工具复核；不要把 agent 输出直接升级为可施工结论。

## 参考资料

- GitHub：<https://github.com/pascalorg/editor>
- GitHub REST API：<https://api.github.com/repos/pascalorg/editor>
- Releases：<https://github.com/pascalorg/editor/releases>
- 本地编辑器文档：<https://editor.pascal.app/docs/developers/local-editor>
- Agent skills：<https://github.com/pascalorg/editor/tree/main/skills>
- LICENSE：<https://github.com/pascalorg/editor/blob/main/LICENSE>
