# Vibe-Research

<!-- markdownlint-disable MD013 MD012 -->

## 定位

`Vibe-Research` 是一个个人 AI 投研系统，主打 A 股，同时兼看美股、港股和部分韩股。它把行情、财报、估值、研报、公告、资金面、资讯、自选股、持仓和研究记录放到一个本地看板里，再把 AI 分析入口交给用户自选模型或 agent。

它强调“提供数据与工作台，不推荐股票、不预测涨跌、不替用户决策”。

## 用法

项目由 FastAPI 后端和 React 前端组成，README 示例：

```bash
cd backend && python3 -m venv .venv && .venv/bin/pip install -r requirements.txt
.venv/bin/python -m uvicorn app:app --host 127.0.0.1 --port 8900

cd frontend && npm install && npm run dev
```

浏览器打开本地前端后，可以查看每日复盘、资讯雷达、个股数据、自选股、板块中心、持仓、研报和研究记录，并在“接入 AI”页配置 Claude Code、Codex、Qwen Code、DeepSeek CLI 或 OpenAI-compatible API。

## 原理

项目把投研系统拆成三层：

- 数据层：内置 `a-stock-data`、`global-stock-data`、`investment-news` 的公开数据能力。
- 服务层：FastAPI 后端整理行情、财报、资讯、持仓、研报和 AI 调用。
- 前端层：React 19 + Vite 看板承载日常复盘、个股页、资讯和研究记录。

AI 接入分两类：调用本机已登录 CLI 做一次性分析，或使用 API / MCP 让 agent 调用数据工具。

## 价值

- 对个人投研：把分散的数据源和研究动作放到同一工作台，降低日常复盘摩擦。
- 对 agent 应用：展示了“先把数据备好，再让 AI 分析”的稳健形态。
- 对中文金融场景：A 股公告、研报、资金面、板块和短线情绪等模块比通用美股 dashboard 更贴近本土需求。
- 对本地优先产品：持仓、研报和记录可在本地沉淀，便于自主管理。

## 风险边界

- 项目不是投资建议系统，不能把 AI 输出当成买卖指令。
- 公开数据源可能延迟、失效或口径不一致，关键决策必须交叉验证。
- 金融数据和个人持仓属于敏感信息，云端部署时要单独处理访问控制。
- API 模型和 CLI 工具可能记录请求内容，接入前需要核查隐私策略。

## 补充建议

- 适合用作“个人研究记录 + 数据看板”，不适合无人值守交易。
- 建议把 AI 输出强制分成事实、推断、风险、待验证数据四段。
- 对研报上传功能，应增加文件索引、脱敏和备份策略。
- 后续观察它是否能引入可复现因子、回测、审计日志和多市场数据质量报告。

## 参考资料

- GitHub 仓库：<https://github.com/simonlin1212/Vibe-Research>
- 官网：<https://viberesearch.wiki>
- A 股数据上游：<https://github.com/simonlin1212/a-stock-data>
- 全球市场数据上游：<https://github.com/simonlin1212/global-stock-data>
