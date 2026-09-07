<!-- markdownlint-disable MD013 MD034 -->

# camofox-browser（jo-inc/camofox-browser）

> 记录日期：2026-09-08（Asia/Shanghai）。本页依据上游 README、Security Model、release、LICENSE 与 GitHub REST API 做静态整理；本轮未安装浏览器、未导入 Cookie、未访问受保护站点，也未验证绕过率、内存、token 或匿名 telemetry 声明。

## 定位

`camofox-browser` 是面向 AI agent 的无头浏览器服务：底层使用 Camoufox（Firefox fork）在原生实现层调整 WebGL、AudioContext、屏幕、WebRTC 等浏览器指纹，上层提供 REST API、OpenAPI、accessibility snapshot、稳定 element refs、会话与搜索宏。上游把它定位为 Playwright / Puppeteer 在反自动化站点上的替代入口。

2026-09-08 的 GitHub 官方综合 / JavaScript Trending 抓取显示约 `+285 stars today`；REST API 快照为 `9,645 stars / 1,012 forks / 125 open issues`，许可证为 MIT。最新 release 标签为 `camoufox-backup-380139564`（2026-09-06），命名不像常规语义版本，升级前应另外确认其用途与变更内容。

## 用法

上游提供 OpenClaw plugin、npm、源码与 Docker 路径。最小源码入口为：

```bash
git clone https://github.com/jo-inc/camofox-browser.git
cd camofox-browser
npm install
npm start
```

服务默认端口为 `9377`，首次安装会下载约 300 MB 的 Camoufox 浏览器包。真实试用应先绑定 localhost、设置 `CAMOFOX_ACCESS_KEY`、关闭 crash telemetry，并只用专用测试账号；不要先导入日常浏览器 Cookie。

## 原理

- **原生指纹调整**：Camoufox 在 Firefox C++ 层处理部分可识别表面，避免仅靠页面脚本 shim。
- **Agent 友好表示**：将页面 accessibility tree 转为较小 snapshot，并给交互元素分配稳定 ref，供 click/type/extract 使用。
- **会话隔离与持久化**：按 user ID 分离 Cookie / localStorage；默认把状态写入 `~/.camofox/profiles/<hashed-userId>/`，还可选择保存 IndexedDB。
- **认证与登录迁移**：Cookie import 默认要求 `CAMOFOX_API_KEY`；所有路由可用 `CAMOFOX_ACCESS_KEY` 做 bearer auth，并可通过 VNC 完成人工登录。
- **代理、下载与 trace**：支持 proxy/GeoIP、文件上传下载、截图、Playwright trace、结构化抽取和搜索宏。
- **网络与进程**：核心浏览器访问目标网站；可选 yt-dlp 抽取 YouTube 字幕；crash/hang reporter 默认向 Cloudflare Worker 发送上游声明已匿名化的数据。

## 价值

- 把浏览器状态、交互和抽取统一成 agent 可调用的 API，降低不同宿主重复集成成本。
- accessibility snapshot 与 element ref 比直接把整页 HTML 交给模型更节省上下文，也更利于回放和审计。
- 独立会话、VNC 登录、Cookie import、trace 和下载接口覆盖了长时程 Web agent 常见的工程缺口。
- 自托管与多种部署入口方便在隔离环境中做可控试验。

## 风险边界

- 上游直接宣传 bypass Cloudflare、bot detection 与 anti-scraping；这不是绕过访问控制、网站条款、robots、版权、隐私或地域规则的授权。
- “anti-detection”不是不可检测。站点会结合行为、账户、IP、支付、设备和历史信号；本页没有测任何成功率。
- README 称服务默认绑定所有接口，若未设置全局 access key，浏览器、下载、截图、会话和持久 Cookie 可能暴露给局域网或公网。
- 持久 Cookie、localStorage、可选 IndexedDB、trace zip、截图和下载都可能保存认证信息或敏感页面；hashed user ID 不是加密。
- npm 生命周期会下载浏览器二进制；release 名称也较特殊。校验下载来源、锁定版本与构建 provenance 后再用于受信账号。
- telemetry 是上游的匿名化声明，本轮未抓包；关闭或自托管 reporter 才能缩小未知数据出口。
- 页面内容可向 agent 注入恶意指令。浏览器会话隔离不等于模型、文件系统、凭据或后果性操作隔离。

## 补充建议

- 在专用容器 / VM 和假账号中固定版本，先验证默认 bind、认证失败、Cookie 路径穿越、下载目录和 trace 删除。
- 对允许访问的域名、方法、下载类型和提交动作设 allowlist；登录、发布、购买、删除等动作必须有人确认。
- 用含 Cloudflare、普通表单、动态列表、文件下载和恶意 prompt 的小型 golden set 比较原生 Playwright 与 camofox；同时记录成功率、误操作、内存与 token，而不只看“是否打开”。
- 默认设置 `CAMOFOX_CRASH_REPORT_ENABLED=false`，并定期清理 profile、trace、截图和下载资产。

## 参考资料

- GitHub 仓库：https://github.com/jo-inc/camofox-browser
- GitHub REST API：https://api.github.com/repos/jo-inc/camofox-browser
- Security Model：https://github.com/jo-inc/camofox-browser#security-model
- Releases：https://github.com/jo-inc/camofox-browser/releases
- LICENSE：https://github.com/jo-inc/camofox-browser/blob/master/LICENSE
- Camoufox：https://camoufox.com/
