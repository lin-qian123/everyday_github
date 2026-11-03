<!-- markdownlint-disable MD013 -->

# ai-goofish-monitor：闲鱼监控、筛选与 AI 分析工作台

- 上游：[Usagi-org/ai-goofish-monitor](https://github.com/Usagi-org/ai-goofish-monitor)；分类：办公、商业与行业应用。
- 更新：2026-11-04（Asia/Shanghai）；固定 master SHA：`77f8d75869acd65f9dba72731b95c7c49ea67bdf`。
- 热度：综合 daily +204；API 16,331 stars / 2,840 forks / 42 open issues（含 PR）。最新发行 2.5，UTC 2026-10-09；当前主线与发行镜像应分别核对。
- 证据范围：官方榜单、API、发行记录与固定源码静态核读；本轮未部署、导入登录态、采集商品或调用模型。

## 定位

基于 Playwright、FastAPI 与 Web UI 的多任务商品监控系统。用户配置关键词、价格、地区、发布时间、定时规则与账号；系统抓取商品和卖家信息，再用关键词规则或多模态模型判断，向通知渠道发送结果。它提供筛选辅助，不能证明商品真实、价格合理或卖家可靠。

## 用法

上游推荐 Docker；先固定源码，审查配置和镜像身份：

```sh
git clone https://github.com/Usagi-org/ai-goofish-monitor
cd ai-goofish-monitor
git checkout 77f8d75869acd65f9dba72731b95c7c49ea67bdf
cp .env.example .env
```

AI 路线需配置 OpenAI 兼容服务地址、key 和支持图片的模型；关键词任务不经过 AI 生成标准流程。启动前更换默认 Web 凭据，并将 compose 的 `8000:8000` 改为 `127.0.0.1:8000:8000`，或放入有独立认证的受限网络。随后按上游说明执行 `docker compose up -d`，在本机 8000 端口管理任务。README 的本机访问地址不表示默认端口只绑定本机。

闲鱼登录态需要用户自行授权导入，保存于 state；不要把 cookie 当作普通配置上传。当前主线使用 SQLite，首次启动会尝试从旧 config / jsonl / price_history 导入；升级前备份并核对迁移结果。固定 checkout 也不会自动固定 compose 中的 latest 镜像。

## 原理

- 后端调度任务进程，Playwright 搜索、翻页、读取详情和图片；账号 / 代理轮换与失败保护是独立配置。
- AI 模式先异步生成分析标准，再逐商品调用模型；关键词模式走规则判断。
- SQLite 保存任务、结果与价格历史；登录态、提示词、日志与图片仍在文件系统。
- 通知模块连接 ntfy、Bark、Telegram、企业微信、Webhook 等外部渠道，形成采集、判断、通知链路。

## 价值

适合把重复搜索和初步筛选变成可检查的任务、日志与结果记录。关键词路线也便于先建立可解释基线，再衡量 AI 是否减少误报；需要人工复查商品事实和购买决策。

## 风险边界

- 本轮读取 app、tasks / accounts 路由与依赖文件，未见统一后端会话或 token 鉴权；`/auth/status` 只返回凭据校验结果，前端用 localStorage 保存登录状态。**不能将登录页视为 API 访问控制**。这是静态发现，未执行绕过测试。
- 默认 admin/admin123、监听 0.0.0.0 与 compose 未指定宿主 IP 的端口映射需要一并处理；只改密码不能补齐 API 鉴权。
- cookie、账号、图片、卖家信息、模型 key 与通知凭据分布在多个目录和服务中；AI / 通知服务会形成数据出口。
- 轮换和重试不等于获得采集授权；遵守目标平台规则、访问频率和账号使用范围，风控或结构变化会导致漏报。
- 根许可为 MIT；平台内容、账号及第三方服务条款另行适用。主线 SQLite 迁移不能从旧发行号推断已部署镜像具有相同行为。

## 补充建议

1. 先用非敏感测试数据核对后端认证与网络边界，再导入账号。
2. 对已标注商品比较关键词与 AI 的漏报、误报、延迟和调用成本，保留模型与 prompt 版本。
3. 固定镜像 digest，验证 SQLite 导入数量、重复处理与备份恢复；为 cookie、日志和图片设置保留期限。

## 参考资料

- [README](https://github.com/Usagi-org/ai-goofish-monitor/blob/77f8d75869acd65f9dba72731b95c7c49ea67bdf/README.md)、[compose](https://github.com/Usagi-org/ai-goofish-monitor/blob/77f8d75869acd65f9dba72731b95c7c49ea67bdf/docker-compose.yaml)。
- [app 与认证入口](https://github.com/Usagi-org/ai-goofish-monitor/blob/77f8d75869acd65f9dba72731b95c7c49ea67bdf/src/app.py)、[任务路由](https://github.com/Usagi-org/ai-goofish-monitor/blob/77f8d75869acd65f9dba72731b95c7c49ea67bdf/src/api/routes/tasks.py)、[账号路由](https://github.com/Usagi-org/ai-goofish-monitor/blob/77f8d75869acd65f9dba72731b95c7c49ea67bdf/src/api/routes/accounts.py)、[依赖](https://github.com/Usagi-org/ai-goofish-monitor/blob/77f8d75869acd65f9dba72731b95c7c49ea67bdf/src/api/dependencies.py)。
- [前端登录状态](https://github.com/Usagi-org/ai-goofish-monitor/blob/77f8d75869acd65f9dba72731b95c7c49ea67bdf/web-ui/src/composables/useAuth.ts)、[环境示例](https://github.com/Usagi-org/ai-goofish-monitor/blob/77f8d75869acd65f9dba72731b95c7c49ea67bdf/.env.example)、[LICENSE](https://github.com/Usagi-org/ai-goofish-monitor/blob/77f8d75869acd65f9dba72731b95c7c49ea67bdf/LICENSE)。
- [仓库 API](https://api.github.com/repos/Usagi-org/ai-goofish-monitor)、[2.5 发行](https://github.com/Usagi-org/ai-goofish-monitor/releases/tag/2.5)。
