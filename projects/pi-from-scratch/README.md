<!-- markdownlint-disable MD013 -->

# pi-from-scratch

- 仓库：[SaladDay/pi-from-scratch](https://github.com/SaladDay/pi-from-scratch)
- 快照：2026-08-10 抓取；GitHub API 显示其创建于 2026-08-09，约 63 stars、2 forks，MIT。数字会随时间变化。
- 分类：Coding Agents 与终端助手

## 定位

一套把极简 TypeScript coding agent 拆解为可逐步阅读的教程和源码的项目。它以 `pi` 的核心数据流为参照，完成一个能读文件、改代码、执行命令的 `nano-pi`，并用网页 Trace 配合解释执行过程。

## 用法

本地运行 agent 需 Node.js 22+、OpenAI 兼容 API，以及 `NANOPI_API_KEY`；执行 `npm install && npm run dev`。可用 `NANOPI_MODEL` 和 `NANOPI_BASE_URL` 更换模型或端点。教学网站位于 `web/`，可单独 `npm install && npm run dev`；仓库声明可分别运行根目录和 `web/` 的 `npm test`。

## 原理

项目刻意去掉完整 agent 产品的工程细节，只保留模型调用、文件/命令工具、会话数据流等最小闭环。在线 Trace 是预生成静态数据，浏览网页本身不会请求模型；因此它更适合作为 agent loop 的可读参考，而不是通用运行时。

## 价值

对需要理解 coding agent 如何把模型输出落到工具调用的人，这种小体量实现便于逐行阅读、修改和做教学演示。它也能帮助团队区分“最小 agent 机制”与权限、恢复、审计、成本控制等生产要求。

## 风险边界

`nano-pi` 能修改文件并执行命令，模型提示或工具调用一旦被误导就可能影响本地工作区。OpenAI 兼容端点和 API key 的数据、费用、保留策略取决于实际 provider；63 stars 只是创建后不久的开发者关注，不能说明工具安全或可用于生产。

## 补充建议

先在临时目录、低权限账户和最小测试仓库中运行，并设置独立、限额的 API key。对每个工具调用增加路径 allowlist、命令确认和日志，再考虑将教学代码扩展到真实任务；不要把简化实现直接接入含凭据的仓库。

## 参考资料

- [项目 README 与源码](https://github.com/SaladDay/pi-from-scratch)
- [在线教学与 Trace](https://pi-from-scratch.vercel.app)
- [GitHub API 元数据快照](https://api.github.com/repos/SaladDay/pi-from-scratch)
