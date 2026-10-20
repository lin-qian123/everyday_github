<!-- markdownlint-disable MD013 -->

# dsh-pet

> 更新：2026-10-21（Asia/Shanghai）。分类：前端、UI 与 Agent 交互层。上游 `PC2005-cloud/dsh-pet`；快照 `cf3ed3c4dd68`（main）。本文为官方资料与源码静态研究；热度、发行时间及社媒限制见[当日日报](../../daily/2026-10-21/ai-hotspots.md)。

## 定位

DeepSeek Harness（DSH）的动画宠物插件，也支持独立桌面模式。除待机、漫游、拖拽与动作菜单，还可显示会话工作状态、余额气泡及可选聊天；仓库同时提供角色提示词、视频处理脚本和插件。[README.md](https://github.com/PC2005-cloud/dsh-pet/blob/cf3ed3c4dd6829b252f352d4c61a18db6fdb26d4/README.md)

## 用法

已具备 DSH 时，桌面版在插件管理中安装 `dsh-pet`；Web 版按文档用 `dsh plugin --profile web add dsh-pet`。源码安装需进入内层 `dsh-pet/`、安装依赖并手动构建。独立运行另用 npm 包与对应入口；不要混淆 DSH profile 安装目录与全局命令 PATH。[README.md](https://github.com/PC2005-cloud/dsh-pet/blob/cf3ed3c4dd6829b252f352d4c61a18db6fdb26d4/README.md) [dsh-pet/package.json](https://github.com/PC2005-cloud/dsh-pet/blob/cf3ed3c4dd6829b252f352d4c61a18db6fdb26d4/dsh-pet/package.json)

自制素材按“源视频 → 水印区域处理 / 绿幕抠像或人工 alpha → 统一尺寸与站姿 → 播放变体”管线处理，需要 Python、ffmpeg、numpy、scipy。文档示例不代表本轮完成了动画制作。[README.md](https://github.com/PC2005-cloud/dsh-pet/blob/cf3ed3c4dd6829b252f352d4c61a18db6fdb26d4/README.md)

## 原理

把 DSH 事件或独立进程状态映射到动画状态机，并在浏览器或透明置顶窗口中播放素材。素材生成与实时播放分开，宠物动起来本身不需要每帧调用模型。独立 AI 配置默认 `enabled=false`、自动碎碎念关闭，启用时另配 provider URL、模型和 key。[README.md](https://github.com/PC2005-cloud/dsh-pet/blob/cf3ed3c4dd6829b252f352d4c61a18db6fdb26d4/README.md) [dsh-pet/src/standalone/ai-config.ts](https://github.com/PC2005-cloud/dsh-pet/blob/cf3ed3c4dd6829b252f352d4c61a18db6fdb26d4/dsh-pet/src/standalone/ai-config.ts)

## 价值

工程判断：适合研究 Agent 状态的低干扰反馈，以及从 AI 视频到透明动画资产的交付流程。动画数量与演示效果不能代替多屏、CPU / 内存、失焦通知和长期运行测量。

## 风险边界

- 许可分层：根 LICENSE 为 MIT，但 README 对动画、提示词、源视频声明禁止商用，并要求二创介绍、展示、分发处回链原作者；不能将整个素材包概括为 MIT。[LICENSE](https://github.com/PC2005-cloud/dsh-pet/blob/cf3ed3c4dd6829b252f352d4c61a18db6fdb26d4/LICENSE) [README.md](https://github.com/PC2005-cloud/dsh-pet/blob/cf3ed3c4dd6829b252f352d4c61a18db6fdb26d4/README.md)
- 独立模式当前代码校验本机 Host、Origin / Fetch Metadata，并对非公开读请求使用随机 capability token；部分静态 GET / HEAD 不要求 token。这是源码事实，尚未动态验证，也不能推广到所有历史版本和 DSH 宿主。[dsh-pet/src/standalone/request-security.ts](https://github.com/PC2005-cloud/dsh-pet/blob/cf3ed3c4dd6829b252f352d4c61a18db6fdb26d4/dsh-pet/src/standalone/request-security.ts)
- 启用聊天、碎碎念或余额查询会引入 provider 凭据、网络和费用；本地窗口不意味着模型离线。自制角色及视频应有相应使用权，处理水印不产生素材授权。[README.md](https://github.com/PC2005-cloud/dsh-pet/blob/cf3ed3c4dd6829b252f352d4c61a18db6fdb26d4/README.md) [dsh-pet/src/standalone/ai-config.ts](https://github.com/PC2005-cloud/dsh-pet/blob/cf3ed3c4dd6829b252f352d4c61a18db6fdb26d4/dsh-pet/src/standalone/ai-config.ts)

## 补充建议

先用自有素材和关闭 AI 的配置试单宠物，再验多开、缩放、跨屏、进程退出与网络请求。需要聊天时单独核 key 存储、数据出口和额度；商用素材先取得明确授权。本轮没有安装插件、生成素材或调用模型。

## 参考资料

- [README.md](https://github.com/PC2005-cloud/dsh-pet/blob/cf3ed3c4dd6829b252f352d4c61a18db6fdb26d4/README.md)
- [dsh-pet/src/standalone/ai-config.ts](https://github.com/PC2005-cloud/dsh-pet/blob/cf3ed3c4dd6829b252f352d4c61a18db6fdb26d4/dsh-pet/src/standalone/ai-config.ts)
- [LICENSE](https://github.com/PC2005-cloud/dsh-pet/blob/cf3ed3c4dd6829b252f352d4c61a18db6fdb26d4/LICENSE)
- [dsh-pet/package.json](https://github.com/PC2005-cloud/dsh-pet/blob/cf3ed3c4dd6829b252f352d4c61a18db6fdb26d4/dsh-pet/package.json)
- [dsh-pet/src/standalone/request-security.ts](https://github.com/PC2005-cloud/dsh-pet/blob/cf3ed3c4dd6829b252f352d4c61a18db6fdb26d4/dsh-pet/src/standalone/request-security.ts)
- [仓库 API](https://api.github.com/repos/PC2005-cloud/dsh-pet)
- [v0.3.7 Release](https://github.com/PC2005-cloud/dsh-pet/releases/tag/v0.3.7)
