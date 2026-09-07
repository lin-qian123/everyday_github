<!-- markdownlint-disable MD013 MD034 -->

# OpenBidKit_Yibiao（FB208/OpenBidKit_Yibiao，易标投标工具箱）

> 记录日期：2026-09-08（Asia/Shanghai）。本页依据上游中文 README、release、LICENSE 与 GitHub REST API 做静态整理；本轮未下载安装包、未导入招标文件、未调用模型或 MinerU，也未验证生成质量、查重、废标项检查或数据隐私。

## 定位

`OpenBidKit_Yibiao` 是 Electron 桌面端 AI 标书工作台，覆盖招标文件解析、方案扩写、多标段 / 多阶段投标、知识库、全文一致性、查重、废标项 / 错别字 / 逻辑检查、图片与 Mermaid / HTML 图、插件和开放 API。它面向真实投标文档生产，但“生成”和“检查”都属于辅助环节，不能替代招标原文、法律商务和签章交付审核。

2026-09-08 的 GitHub JavaScript Trending 抓取显示约 `+93 stars today`；REST API 快照为 `2,834 stars / 733 forks / 49 open issues`，最新 release 为 `v2.25.27`（2026-09-07），许可证为 AGPL-3.0。

## 用法

普通用户可从上游 release / 官网获取安装包；开发者需要 Node.js 22，调试 Open XML 或本地打包还需要 .NET 10 SDK：

```bash
git clone https://github.com/FB208/OpenBidKit_Yibiao.git
cd OpenBidKit_Yibiao/client
npm ci
npm run dev
```

README 的“下载方式”链接当前指向另一个 `yibiaoai/yibiao-simple` release 仓库，而当前仓库自身也有 release；下载前应核对域名、签名 / hash、版本、源码 commit 和两个分发入口的关系。首次试用只用虚构标书，不输入真实客户、报价、资质或未公开招标材料。

## 原理

- **Electron 分层**：Main / Preload 提供本地文件和系统能力，React renderer 通过 `window.yibiao` 调用受控 IPC。
- **本地状态**：配置写本地文件，业务状态放 SQLite；耗时任务在 Main 后台运行并支持恢复。
- **AI / Agent 层**：统一 AI Service 处理模型请求，Pi Agent 用独立 Runtime / Session 运行任务。
- **文档链路**：支持本地或 MinerU 解析、Open XML 操作和图片渲染，再生成章节、检查项与导出物。
- **知识和质量工具**：本地知识库、全局事实、查重、一致性、废标项与语义修改围绕同一标书 workspace 工作。
- **在线服务**：Cloudflare Worker 提供公告、资源、插件、模型信息、许可证和统计服务，因此桌面 / 本地数据并不等于系统完全离线。

## 价值

- 将长文档解析、资料复用、生成、检查与导出集中在一个面向中文投标场景的工作台。
- 本地 SQLite、可恢复任务和 Open XML 有利于保留中间状态与可编辑交付物，而非只输出聊天文本。
- 全局事实、一致性和废标项检查为“生成后必须核对”提供明确入口。
- AGPL 源码与本地开发路径使团队可审计、扩展或自托管关键环节。

## 风险边界

- 招标文件中的资格、格式、签章、报价、日期、承诺和废标条件是高后果约束；LLM / 规则漏检一次就可能造成实际损失。
- 知识库与全局事实可能过期或串标；引用旧客户、旧参数、竞争信息或未经授权材料会引入保密、知识产权与合规风险。
- 本地客户端仍会连接模型、MinerU、Cloudflare 服务、插件或赞助 API；数据流必须按具体 provider 和功能抓包确认。
- AI 查重、逻辑与错别字检查不是法律审查、商业审批、工程校核或反抄袭证明。
- 插件、开放 API、Electron IPC、本地文件写入和自动更新扩大供应链与权限表面；安装包 provenance 需要独立验证。
- AGPL-3.0 对修改、分发和网络服务有义务；NOTICE 与第三方依赖也要一起审查。

## 补充建议

- 建立脱敏 golden tender：故意放入冲突日期、遗漏签章、互斥参数、硬性废标项和跨章节不一致，逐项统计 precision / recall。
- 把所有生成段落标出来源、模型、prompt、时间与人工 owner；关键数字只能从锁定字段或人工确认表回填。
- 先以网络 deny-by-default 运行，按功能逐项放行 provider；检查日志、缓存、crash report、插件和删除后的残留。
- 对最终 DOCX / PDF 做确定性 schema、页码、目录、字体、附件、签章位与 hash 检查，并保留双人审批。

## 参考资料

- GitHub 仓库：https://github.com/FB208/OpenBidKit_Yibiao
- GitHub REST API：https://api.github.com/repos/FB208/OpenBidKit_Yibiao
- 当前仓库 release：https://github.com/FB208/OpenBidKit_Yibiao/releases/tag/v2.25.27
- 项目官网：https://yibiao.pro/
- 上游演示：https://www.bilibili.com/video/BV1sC5i6SE74
- LICENSE：https://github.com/FB208/OpenBidKit_Yibiao/blob/main/LICENSE
