# Browser-BC

<!-- markdownlint-disable MD013 -->

## 定位

`Browser-BC` 的 GitHub 描述是“Agent behavior clone for browser using”，README 当前显示产品名为 Journey Forge Local。它聚焦本地记录浏览器任务轨迹，把每个网站积累成 capability bucket，并把同类轨迹蒸馏为可复用 skill，最终供 Claude Desktop / Claude Code 等 agent 使用。

截至 2026-07-11，GitHub API 显示该仓库约 406 stars，创建于 2026-06-26，主要语言为 TypeScript，但 README 中运行时强调 Python、本地 server 和浏览器扩展。它适合归入“前端、UI 与 Agent 交互层”，因为它处理的是网页任务录制、技能蒸馏和 browser-use 能力复用。

## 用法

README 给出的流程：

```bash
cp config.example.env .env.local
./scripts/start.sh
cd extension && pnpm install && pnpm build
```

随后在 Chrome 扩展页加载 `extension/dist/chrome-mv3`，录制一个网站上的短任务，停止、打标签、上传。后台 harness 会执行 atomize、classify、bucket、distill 和 install，把技能安装到 Claude Code skills root，或打包成 Claude Desktop 可上传的 zip。

## 原理

系统由浏览器扩展、本地 server、harness pipeline 和本地数据目录组成。扩展记录自由任务，server 在 `localhost:8099` 接收 trace chunks 并生成 `data/traces/<id>/trace.json`。harness 将事件分段，归类到“域名 + capability”的 bucket，再用 LLM 蒸馏出 `SKILL.md`、`TRACE_GUIDE.md`、`meta.json` 和 `evidence.jsonl`。

关键点是每个网站不是只有一条演示轨迹，而是持续积累“登录、注册、搜索、下单、上传”等 capability bucket。新轨迹会增强已有 bucket，skill 也随之更新。

## 价值

- 把 browser-use 经验从一次性录屏变成可复用 skill。
- 本地优先，trace、bucket 和 skill 状态保存在 `data/` 下。
- 能连接 Claude Desktop 和 Claude Code，适合非代码网页操作复用。
- 为 GUI agent 训练/评估之外的真实个人自动化提供了轻量路径。

## 风险边界

- README 明确需要自带 LLM API key，蒸馏调用可能把轨迹内容发给模型端点。
- 浏览器 trace 可能包含账号、表单、隐私数据，录制前必须隔离测试账号或脱敏。
- skill 只是指令，不自动授予浏览器控制能力；真实执行仍需 Playwright MCP 等工具。
- GitHub API 未识别到标准许可证，复用前需要确认授权。

## 补充建议

- 与 `Agent-S`、`peerd`、`sim-use` 区分：本项目偏个人网页任务轨迹蒸馏，不是 GUI benchmark 或移动端控制。
- 建议后续观察是否支持多浏览器、多用户隔离、trace 脱敏和失败样本回灌。
- 对企业内部系统，必须先做数据分类和最小权限策略，再录制真实流程。

## 参考资料

- GitHub 仓库：<https://github.com/Einsia/Browser-BC>
- browser-use：<https://github.com/browser-use/browser-use>
- Agent-S：<https://github.com/simular-ai/Agent-S>
- peerd：<https://github.com/NotASithLord/peerd>
