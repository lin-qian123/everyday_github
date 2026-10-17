<!-- markdownlint-disable MD013 -->

# PilotDeck（OpenBMB/PilotDeck）中文解读

> 上游仓库：<https://github.com/OpenBMB/PilotDeck> · 归类：记忆层与个人 AI 基础设施 · 证据快照：2026-10-18（Asia/Shanghai）。认证 API：4,584 stars / 511 forks / 155 open issues；最新稳定 Release `v2026.10.17`；API 首个 tag `v260806` 不作最新版依据；AGPL-3.0。本页为上游材料及所列源码的静态整理，未安装运行、复测 benchmark 或完成全面安全审计。

## 定位

PilotDeck 围绕 WorkSpace 组织文件、技能、可编辑记忆和长任务，组合白盒记忆、强弱模型路由与 Always-on。适合研究任务接续、办公产物和个人 Agent 工作空间；“2000 轮持续工作”、低成本和质量优势均是上游声明，不能直接外推到任意任务。

## 用法

优先先读源码安装文档，再在测试 profile / 工程副本配置 provider。README 源码路线要求 Node.js 22.13+ 且 <23，使用锁文件和指定 pnpm filters；首次 UI onboarding 会写模型配置并启动 Gateway。Docker 路线持久化整个 PILOT_HOME；若只需本机访问，收窄 Compose 的端口绑定，再测试文件产物、记忆编辑和权限提示。本轮未执行安装。

## 原理

Gateway 执行 Agent，UI Server 提供 Web / REST / WebSocket。按 WorkSpace 组织上下文与记忆，Dream Mode 整理并支持回滚；Smart Routing 分配主 / 子模型。独立 permissions 配置可表达 allow / ask / deny，当前 `skipPermissions` 默认 false；Gateway token 文件以受限目录 / 文件权限生成。

## 价值

可见、可修订的记忆有助于定位上下文污染和错误来源；按任务记录 token 与成本则利于小规模比较路由策略。相比只展示结果，保留记忆 provenance、最终文件和恢复记录更易审查，但路由器和记忆整理本身也需要验收。

## 风险边界

- WorkSpace 是组织 / 检索范围，不能仅凭 README 的“完全隔离”表述认定 OS 安全边界；Docker bind mount 和工具权限决定实际可触达文件。
- Compose 当前发布 `3001:3001`，`config.js` 默认关闭本地 UI 的 JWT 登录检查，需设置 `PILOTDECK_DISABLE_LOCAL_AUTH=0` 或 `false` 恢复用户名 / 密码认证；部署前核有效认证与网络绑定，Gateway token 不能替代全部 UI 身份控制。
- 上游 7 个复杂任务的评分 / 成本与特定社媒工作流仅是作者报告，模型、评审、重试和任务样本影响结论，未独立复测。
- 全部 sessions、memory、skills、auth DB 和 provider 配置会持久化；后台工具可能执行 shell、上传文件或操作服务。AGPL 与内置第三方技能需分别核许可，不能把本机安装理解为资料不外发。

## 补充建议

建两个含不同标记的测试 WorkSpace，检查检索串扰、文件越界、记忆回滚和 shell 拒绝；用同一金标任务比较固定单模型与路由，记录总费用、质量和失败率。先关非必要后台任务，验证 UI 登录拒绝和卷备份恢复后再长期运行。

## 参考资料

- 上游仓库：<https://github.com/OpenBMB/PilotDeck>
- GitHub REST API：<https://api.github.com/repos/OpenBMB/PilotDeck>
- README / 2.0 与作者评测：<https://github.com/OpenBMB/PilotDeck/blob/main/README.md>
- 源码安装：<https://github.com/OpenBMB/PilotDeck/blob/main/README_SOURCE_INSTALL.md>
- Docker 文档：<https://github.com/OpenBMB/PilotDeck/blob/main/README_DOCKER.md>
- Compose 暴露与认证注释：<https://github.com/OpenBMB/PilotDeck/blob/main/docker-compose.yml>
- 权限默认值：<https://github.com/OpenBMB/PilotDeck/blob/main/src/permission/settings.ts>
- Gateway token 实现：<https://github.com/OpenBMB/PilotDeck/blob/main/src/gateway/server/authToken.ts>
- UI 认证默认配置：<https://github.com/OpenBMB/PilotDeck/blob/main/ui/server/constants/config.js>
- UI 认证中间件：<https://github.com/OpenBMB/PilotDeck/blob/main/ui/server/middleware/auth.js>
- Release：<https://github.com/OpenBMB/PilotDeck/releases/tag/v2026.10.17>
- 许可：<https://github.com/OpenBMB/PilotDeck/blob/main/LICENSE>
