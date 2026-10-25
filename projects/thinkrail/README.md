<!-- markdownlint-disable MD013 -->

# ThinkRail：以 pi、工作区和持续规格组织编码的 Agent IDE

- 主上游：[JetBrains/thinkrail](https://github.com/JetBrains/thinkrail)；repository ID `1293238217`。
- 采样日期：2026-10-26（Asia/Shanghai）；分类：Coding Agents 与终端助手。
- API 累计快照：1,622 stars / 101 forks / 199 open issues（含 PR 口径）；与榜单日增分开。
- 默认分支 `main`，本页静态依据固定在 `d299f20d2ba014f382ddbcc9b49f2aa63fada132`。发行 API 首项 [v0.3.0-nightly.6](https://github.com/JetBrains/thinkrail/releases/tag/v0.3.0-nightly.6)，UTC 2026-10-25T06:49:25Z，预发行。
- 核验层级：读取上游文档、许可、元数据及所列部分实现；未安装运行上游、调用模型或复现实验。

## 定位

ThinkRail 是 JetBrains 孵化中的 Agent IDE，把 pi 编码引擎、编辑器、终端、diff、GitHub PR 和项目规格放在一个工作台中。当前文档把完整扩展支持列为后续方向，不能把“自我扩展”愿景全部算成已交付功能。

## 用法

优先从已核验的 Release 下载对应平台制品与 SHA256SUMS，确认稳定 / nightly 通道后再安装。启动入口如下，本轮未执行：

```bash
thinkrail ~/code/my-repo
```

通过 JetBrains AI 或 pi 的 provider 身份接入模型。桌面 macOS 仅提供 Apple Silicon，Intel CLI 也没有预编译包；Linux 桌面有 glibc 2.38+ 等依赖，不能由“跨平台”推断旧系统即装即用。源码开发需要固定 Bun 1.4.4、Node.js ≥22.19；滚动安装脚本与所选发行要分开核对。

## 原理

宿主在进程内运行 pi，每个 chat 有独立会话；Bun HTTP / WebSocket 服务通过带版本的协议连接 React 界面。Git worktree 提供独立分支与工作目录，旁置 SPEC.md 图谱保存设计意图，Agent Skills 承载可复用流程。pi 负责模型、上下文压缩与会话，应用负责工作区、编辑和交互。用户也能直接使用原项目目录，不能假定每次运行都进入新 worktree。

## 价值

适合已有 Git 工程中需要同时看代码、计划、规格和差异的任务：意图可留在代码旁，审阅意见能回到 Agent，减少在终端、编辑器与 PR 之间搬运上下文。是否提高正确率和效率仍须用自己的任务比较，界面集中本身不构成实测收益。

## 风险边界

- worktree 解决工作副本冲突，不提供 OS 隔离；shell、provider、扩展与 GitHub 操作仍受真实用户权限和凭据影响。
- README 表示会对 MCP 未声明只读的调用提问，并让项目定义的服务先等待批准；只读标记属于服务声明，不能代替独立权限检查。
- **`--no-analytics` / `THINKRAIL_NO_ANALYTICS=1` 仅抑制额外统计。** 固定 analytics 规格和 service 源码显示：带项目 key 的非 CI / test 构建仍有 basic 事件与错误报告；无 key 的源码构建不初始化供应商客户端。默认目标为 PostHog EU。
- 上游设计将 prompt、源码、凭据和任意错误消息排除出统计，按闭集事件和清洗后的异常字段发送；本轮只核了部分实现，未抓包证明全部运行路径。首启额外分享开关还会在对话框挂载后应用，而非等按 Done 才生效。
- 当前 API 首项是预发行 nightly；主线说明、稳定版和该 nightly 的能力不能混为一谈。代码为 Apache-2.0，模型服务另有费用与条款。

## 补充建议

用无 secret 的小仓库做一次从规格、修改、审阅到 PR 草稿的完整试用，记录工作目录、凭据出口和实际授权提示。分别验证“关闭额外统计”“不带统计 key 的构建”和网络抓包结果。检查 SPEC.md 是否与实现同步，保留用户修改和模型费用记录，再决定是否迁入主项目。

## 参考资料

- [README.md](https://github.com/JetBrains/thinkrail/blob/d299f20d2ba014f382ddbcc9b49f2aa63fada132/README.md)。
- [LICENSE](https://github.com/JetBrains/thinkrail/blob/d299f20d2ba014f382ddbcc9b49f2aa63fada132/LICENSE)。
- [packages/server/src/analytics/SPEC.md](https://github.com/JetBrains/thinkrail/blob/d299f20d2ba014f382ddbcc9b49f2aa63fada132/packages/server/src/analytics/SPEC.md)。
- [packages/server/src/analytics/service.ts](https://github.com/JetBrains/thinkrail/blob/d299f20d2ba014f382ddbcc9b49f2aa63fada132/packages/server/src/analytics/service.ts)。
- [packages/server/src/analytics/sink.ts](https://github.com/JetBrains/thinkrail/blob/d299f20d2ba014f382ddbcc9b49f2aa63fada132/packages/server/src/analytics/sink.ts)。
- [packages/server/src/analytics/mute.ts](https://github.com/JetBrains/thinkrail/blob/d299f20d2ba014f382ddbcc9b49f2aa63fada132/packages/server/src/analytics/mute.ts)。
- [仓库 API](https://api.github.com/repos/JetBrains/thinkrail)、[发行 API](https://api.github.com/repos/JetBrains/thinkrail/releases?per_page=1)；动态元数据仅代表本轮采样。
- 事实来源为以上一手材料；价值、风险评估和建议为本库工程判断，未当作上游实测结果。
