<!-- markdownlint-disable MD013 -->

# Paradev（原 Superset，保留 superset 目录）

- 更新：2026-11-07（Asia/Shanghai）；官方 TypeScript daily +62，为读取快照，不是自然日结算。
- GitHub API：16,030 stars / 1,433 forks / 1,185 open issues（含 PR）；仓库 ID `1080370450`。
- 核读基线：`19db630c1ef9ae4624d8b19cefc44e7b5de62afd`；仅文档与抽样实现核验，未安装运行或独立评测。

## 定位

Paradev 是把 Claude Code、Codex、OpenCode 等 CLI 编码 Agent 放进工作台的桌面应用，集中管理 worktree、终端、代码审阅和浏览器预览。它本身不是模型，也不代理各 CLI 的模型调用；订阅和 API 凭据由用户自行提供。

旧 `superset-sh/superset` API 返回永久迁移到仓库 ID `1080370450`，与当前仓库一致；README 明示 formerly Superset。本页原位更新并保留旧链接，未新建重复目录。它与 Apache Superset 无关。[当前 README](https://github.com/ParadevAI/Paradev/blob/19db630c1ef9ae4624d8b19cefc44e7b5de62afd/README.md)

## 用法

优先从稳定 [desktop-v2.0.5](https://github.com/ParadevAI/Paradev/releases/tag/desktop-v2.0.5)（UTC 2026-11-05）选择系统对应安装包；`desktop-canary` 标为内部测试，CLI v2.0.5 也带 prerelease 标记，不能混称稳定桌面版。macOS 支持 Apple Silicon / Intel，Linux x64 AppImage 仍属实验，Windows 暂未提供。

添加一个已有仓库，创建小任务 workspace，选择已安装的 CLI，完成后在 Changes 查看 diff、运行测试，再决定提交。CLI 仍叫 `superset`；当前 Homebrew 入口为：

```bash
brew install paradevai/tap/superset
```

升级时先备份应用状态与未提交修改，检查 `.paradev/` 和兼容的 `.superset/` 配置。已有 worktree 的导入框默认不运行 setup script。[工作区](https://github.com/ParadevAI/Paradev/blob/19db630c1ef9ae4624d8b19cefc44e7b5de62afd/apps/docs/content/docs/workspaces.mdx)

## 原理

本地项目 workspace 采用独立 Git worktree / branch，云 workspace 使用独立 clone；无项目 session 则使用托管临时工作目录。桌面、CLI、SDK、MCP 可操作同一工作区。worktree 分开工作文件，不能隔离进程、凭据、网络和全局服务，也不能消除合并冲突。

生命周期脚本支持 setup、teardown、run。当前默认是在 setup 执行时立即启动 Agent；“等待 setup 成功”需在实验设置另开。主仓库、worktree、本机覆盖和 legacy 配置存在优先级，诊断时须保留实际解析结果。[脚本规则](https://github.com/ParadevAI/Paradev/blob/19db630c1ef9ae4624d8b19cefc44e7b5de62afd/apps/docs/content/docs/setup-teardown-scripts.mdx)

## 价值

适合把可独立审阅的多个开发任务、CLI 状态、终端与 PR 信息集中管理，尤其便于比较候选实现。可观察指标应是合并后正确率、冲突和返工、任务成本与主机负载；并发数量不能直接代表交付效率。

## 风险边界

- 当前根 LICENSE 已为 MIT；v2.0.5 发行记录包含重新许可。旧页的 ELv2 描述不再代表本次固定源码，历史制品与可选商业服务仍须各按实际版本判断。
- Remote Access 经 Paradev Relay 传递终端和端口流量。授权客户端可触及 host service 可达的文件、终端与 Agent，官方建议使用专门主机；端口转发的 cookies / headers 也会流向远端。
- 开关远端访问会重启 host service、打断在途终端；同组织成员不是自动获得 host 权限，需要另加成员。
- CLI / SDK / MCP 删除工作区时，teardown 失败会以 warnings 返回而继续删除，不能把 teardown 当可靠阻断门。
- 计费、遥测、真实授权、远端撤权与恢复未做运行验证；README 的“不代理模型调用”不能推出全部控制面流量留在本机。[远端范围](https://github.com/ParadevAI/Paradev/blob/19db630c1ef9ae4624d8b19cefc44e7b5de62afd/apps/docs/content/docs/remote-access.mdx)

## 补充建议

从两个可丢弃任务开始，记录 CLI / release、真实配置、token、CPU / 内存和审阅返工。把环境准备设为启动前条件，测试失败 setup、重复调度、断线和撤权。共享主机仅放所需仓库与凭据，PR 合并及外部操作使用独立授权。本轮未安装、导入 worktree、开启 relay 或执行任何脚本。

## 参考资料

- [当前仓库](https://github.com/ParadevAI/Paradev)、[旧 API 迁移证据](https://api.github.com/repos/superset-sh/superset)、[发行列表](https://github.com/ParadevAI/Paradev/releases)。
- [固定 README](https://github.com/ParadevAI/Paradev/blob/19db630c1ef9ae4624d8b19cefc44e7b5de62afd/README.md)、[当前 MIT 许可](https://github.com/ParadevAI/Paradev/blob/19db630c1ef9ae4624d8b19cefc44e7b5de62afd/LICENSE.md)。
- [Workspaces](https://github.com/ParadevAI/Paradev/blob/19db630c1ef9ae4624d8b19cefc44e7b5de62afd/apps/docs/content/docs/workspaces.mdx)、[Lifecycle scripts](https://github.com/ParadevAI/Paradev/blob/19db630c1ef9ae4624d8b19cefc44e7b5de62afd/apps/docs/content/docs/setup-teardown-scripts.mdx)、[Remote Access](https://github.com/ParadevAI/Paradev/blob/19db630c1ef9ae4624d8b19cefc44e7b5de62afd/apps/docs/content/docs/remote-access.mdx)。
