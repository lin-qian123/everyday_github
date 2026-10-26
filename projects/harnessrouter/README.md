<!-- markdownlint-disable MD013 -->

# HarnessRouter：把多个 Agent harness 接成统一的任务接口

- 主上游：[HarnessRouter/harnessrouter](https://github.com/HarnessRouter/harnessrouter)；repository ID `1329163060`。
- 采样日期：2026-10-27（Asia/Shanghai）；分类：Agent 框架与技能生态。
- API 累计快照：3,691 stars / 394 forks / 23 open issues（含 PR 口径），与榜单日增分开。
- 默认分支 `main`；本页主线静态依据固定在 `cd37f226ba3c3cb226dd8b4b2489936f9501b763`。发行 API 首项 [v0.37.2](https://github.com/HarnessRouter/harnessrouter/releases/tag/v0.37.2)，UTC 2026-10-26T17:38:34Z，正式发行标记。
- 核验层级：读取一手文档、许可、元数据与所列部分实现；未安装运行上游、调用模型或复现实验。

## 定位

HarnessRouter Community Edition 是自托管的 Console、Gateway 和 Runner，将 Codex、Claude Code、Hermes、Pi 等 harness 接入相近的任务生命周期。UHP 描述会话、文件、流式输出、取消和技能 / 插件配置，任务表面兼容 Responses API；这不表示每个后端的模型、工具和失败行为完全等价。

## 用法

先固定所选发行及镜像身份，准备 Docker、约 4 GB 磁盘和模型 provider 凭据。上游快速启动示例如下；镜像未固定 digest，本轮未拉取运行：

```bash
docker run -d --name harnessrouter \
  -p 127.0.0.1:3000:3000 \
  -v harnessrouter:/data \
  harnessrouter/harnessrouter
```

首次启动会安装启用的 harness CLI，等到 ready 日志后打开本机控制台。初始账号 / 密码均为 `harnessrouter`，立即在 Profile 修改并保持 loopback。控制台密码、provider key、CE 签发的 API key 是三个不同凭据；产品后端调用实例的 `/api/harness/v1/responses`，用 `metadata.harness_id` 选择 harness。不要将产品 API key 放入前端。

## 原理

Console 的同源代理通向 Gateway，再交由 Runner 在独立会话目录和 OS 用户下执行。持久卷保存数据库、文件、凭据与工作区；会话不是各自一只容器。UHP 统一生命周期语义，再由 adapter 处理 harness 差异。请求可使用 Idempotency-Key 避免重试重复执行；同 key 换 body 会报冲突，仍需验证失败恢复和外部副作用。

## 价值

适合产品后端希望替换 Agent 引擎、保留会话和统一日志的场景。能减少逐一对接 CLI 的工作，但选择哪个 harness 更便宜、更快、更可靠，仍要用同任务、同模型及同权限的测量判断；界面自带 recorded example 也不能计作实时生成验收。

## 风险边界

- 默认口令和公网暴露必须联合处理。环境变量、持久卷内修改后的凭据有优先级；换容器启动参数不一定覆盖已保存密码。
- 容器入口和 Runner 保留 root 管理会话用户，Console / Gateway 与 Agent 降权。独立目录和用户提供一定边界，但共享容器内核，不能等同每任务独立 VM；本轮未做隔离攻击测试。
- CE 关闭的是 Console 产品分析管线，模型请求仍发送至所配置 provider。传给 Agent 的秘密即使在日志中脱敏，仍可被 Agent 读取并向外发送。
- 协议中的 MUST 是实现要求，不等于本轮证明所有路径合规；插件扩展信任、文件输入和 prompt injection 都由采用方继续治理。
- CE 为 Apache-2.0，harness CLI 和 Starter Kits 适用各自条款；主线描述的后端数量也不等于当前发行全部可用。

## 补充建议

先选两个 harness，固定模型和版本，检查会话续接、文件权限、取消、重复请求和失败恢复。备份 `/data` 后再升级，升级拉镜像不会替换正在运行的容器。将成本、耗时和任务通过率与权限配置一起留档，再决定是否迁入正式服务。

## 参考资料

- [README.md](https://github.com/HarnessRouter/harnessrouter/blob/cd37f226ba3c3cb226dd8b4b2489936f9501b763/README.md)。
- [docs/self-hosting-guide.md](https://github.com/HarnessRouter/harnessrouter/blob/cd37f226ba3c3cb226dd8b4b2489936f9501b763/docs/self-hosting-guide.md)。
- [protocol/versions/2026-10-19/security.md](https://github.com/HarnessRouter/harnessrouter/blob/cd37f226ba3c3cb226dd8b4b2489936f9501b763/protocol/versions/2026-10-19/security.md)。
- [LICENSE](https://github.com/HarnessRouter/harnessrouter/blob/cd37f226ba3c3cb226dd8b4b2489936f9501b763/LICENSE)。
- [仓库 API](https://api.github.com/repos/HarnessRouter/harnessrouter)、[发行 API](https://api.github.com/repos/HarnessRouter/harnessrouter/releases?per_page=1)；动态元数据仅代表本轮采样。
- 事实依据为以上一手材料；价值、风险判断与建议为本库工程分析，未写作实测结论。
