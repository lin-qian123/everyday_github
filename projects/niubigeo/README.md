<!-- markdownlint-disable MD013 -->

# NiubiGEO（Albert-Weasker/niubigeo）中文解读

> 上游：[Albert-Weasker/niubigeo](https://github.com/Albert-Weasker/niubigeo) · 分类：办公、商业与行业应用 · 核验：2026-11-09，仓库 ID 1356159928，主线 SHA `6f0eeeb11b4319e845b491a5067d2cfdc8d07b52`。本页为文档与抽样源码静态核读，未安装运行、登录或调用模型 / 云资源。

## 定位

NiubiGEO 是自托管的 GEO（生成式引擎优化）研究工作台：从域名与问题出发，对比不同模型如何描述、提及或推荐品牌，保留原始回答、来源和历史观测。当前稳定发行 v0.3.3；官方付费人工测试 / 优化服务与开源程序分开，不把服务宣传当作优化效果证据。

## 用法

需要 Node.js 22.13+。按官方说明检出 v0.3.3、运行 `npm ci`，配置自己的模型服务凭据后用 `npm run server` 启动工作台。先选择一个模型和少量非敏感问题，核对联网设置及原始答案，再增加采样。

定时监控另需 `npm run schedule:worker`，server 与 worker 使用同一数据目录和服务端密钥；浏览器临时 Key 不能供后台 worker 使用。已建监控可先运行 `npx tsx src/cli.ts keyword-run --project PROJECT_ID --monitor MONITOR_ID --repeats 5 --dry-run`，只估请求数，不推理或估准金额。

## 原理

- 保存项目、问题 / 基线、模型、端点和搜索条件；各模型独立执行，失败记录仍保留。
- 按明确配置的品牌及别名识别提及，分别记录推荐对象、原始回答与 provider 返回引用；普通答案 URL 与 provider citation 分开。
- 历史 / Diff / CSV / JSON 将观测追溯到样本和运行条件；v0.3.3 增加日期 / 模型筛选、重复采样和证据导出。

## 价值

适合产品团队建立可以复查的品牌回答样本，而不是依赖单一黑箱分数。把“被问到后识别品牌”“不点名问题中提及品牌”“明确推荐”分开，有助于提出后续内容和产品假设。

## 风险边界

- 4 个成功样本提及 3 次、另 1 次失败，应报告 3/4 加 1 次失败；失败不能算作未提及。重试保留原样本，不是新的一轮独立观测。
- 改问题、模型、搜索或识别协议后，不能直接把 Diff 当增长；小样本比例没有自动统计置信度，API 回答也不等于消费端产品回答，引用不能证明推荐因果。
- 自托管仍向所选模型 / 搜索提供商发送问题；真实推理、重试和联网可能收费。远程部署需另配认证与 TLS，官方 Docker 示例只映射 loopback。
- v0.3.2 修复网站抓取的私网目标 / 重定向 / DNS 校验，并将历史 Docker 标签改指安全兼容镜像；旧标签不保证原提交身份，升级需核 digest 和实际版本。v0.3.3 的 CI 验收是作者的 fixture / 容器记录，本轮未复跑。
- 根代码 Apache-2.0；`SECURITY.md` 支持版本仍写 v0.1.0-alpha，与当前发行有文档滞后。

## 补充建议

固定问题集、模型 / 端点、联网、别名和采样协议，导出原始样本及失败再比较。先设请求预算；升级前停写并备份完整实际产品数据目录，server / worker 同版本重建。用独立重复观测验证变化，不把市场宣传或一次截图写成 GEO 提升结论。

## 参考资料

下列固定文件均对应本次核验的主线 SHA；主线恰与 v0.3.3 目标提交一致。

- [上游仓库](https://github.com/Albert-Weasker/niubigeo)、[仓库 API](https://api.github.com/repos/Albert-Weasker/niubigeo)、[v0.3.3](https://github.com/Albert-Weasker/niubigeo/releases/tag/v0.3.3)、[v0.3.2 安全与镜像说明](https://github.com/Albert-Weasker/niubigeo/releases/tag/v0.3.2)。
- [README](https://github.com/Albert-Weasker/niubigeo/blob/6f0eeeb11b4319e845b491a5067d2cfdc8d07b52/README.md)、[监控证据与 CLI](https://github.com/Albert-Weasker/niubigeo/blob/6f0eeeb11b4319e845b491a5067d2cfdc8d07b52/docs/monitoring-guide.zh-CN.md)、[Docker / 数据卷](https://github.com/Albert-Weasker/niubigeo/blob/6f0eeeb11b4319e845b491a5067d2cfdc8d07b52/docs/deployment/docker.md)、[安全政策](https://github.com/Albert-Weasker/niubigeo/blob/6f0eeeb11b4319e845b491a5067d2cfdc8d07b52/SECURITY.md)、[LICENSE](https://github.com/Albert-Weasker/niubigeo/blob/6f0eeeb11b4319e845b491a5067d2cfdc8d07b52/LICENSE)。
