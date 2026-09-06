<!-- markdownlint-disable MD013 -->

# openwhispr（OpenWhispr/openwhispr）

> 记录日期：2026-09-07（Asia/Shanghai）。本页依据上游 README、文档、release、LICENSE 与 GitHub REST API 做静态整理；本轮未安装桌面应用、未录音、未连接日历/云模型，也未验证转写、说话人分离或隐私声明。

## 定位

`openwhispr` 是跨 macOS、Windows 与 Linux 的语音听写、会议转写、笔记和语音 AI 助手桌面应用。它允许在 Whisper、NVIDIA Parakeet 等本地路径与 BYOK 云端模型之间选择，并提供自动粘贴、翻译、speaker diarization、团队空间、API 与 MCP。

2026-09-07 的 GitHub 官方综合 Trending 抓取显示约 `+225 stars today`；REST API 快照为 `7,316 stars / 929 forks / 333 open issues`，最新 release 为 `v1.9.2`，许可证为 MIT。

## 用法

普通用户可从 release 下载平台安装包；开发方式要求 Node.js 24+：

```bash
git clone https://github.com/OpenWhispr/openwhispr.git
cd openwhispr
npm install
npm run dev
```

首次试用应只授权麦克风，不连接日历、屏幕、云同步或外部模型；确认本地路径、缓存和删除行为后再逐项增加权限。

## 原理

- **全局听写**：热键触发录音与 ASR，再把清理后的文本粘贴到当前应用。
- **本地或云端 ASR**：本地可用 Whisper/Parakeet 及 Metal、CUDA、Vulkan 路径；云端模式通过用户选择的 provider 处理。
- **语音助手**：语音可作为 LLM 指令，选择性携带高亮文本或屏幕截图，并把结果粘贴回光标或浮层。
- **会议链路**：检测 Zoom、Teams、FaceTime 等通话，结合 speaker diarization、voice fingerprint 与日历集成生成记录。
- **笔记与协作**：本地/语义搜索之外，还提供云同步、共享链接与团队空间。
- **扩展接口**：公开 API 和 MCP 让外部 agent 管理笔记与转写资产。

## 价值

- 将日常听写、会议、笔记和 agent 指令放在同一跨平台入口。
- 本地模型路径为敏感语音提供了减少云端外发的可选架构。
- BYOK 与多 provider 让用户可按速度、语言、成本和数据政策选择处理路径。
- API/MCP 使转写资产能够进入可审计的后续工作流，而不局限于 GUI。

## 风险边界

- “本地可用”不等于所有功能均离线：云模型、云同步、团队分享、日历、网页分享和截图上下文会形成不同数据流。
- 麦克风、会议内容、声纹、日历和屏幕截图属于高敏感数据；组织和与会者同意、保留期、访问控制与删除必须先定义。
- 自动粘贴和高亮文本编辑可能写入错误应用或把秘密带入模型上下文；焦点、剪贴板和快捷键冲突需实测。
- ASR、翻译、说话人分离与摘要会出错，不能把自动记录直接作为医疗、法律、人事或财务事实。
- README 的“no telemetry / no data collection”是上游声明，本轮未做流量抓包、二进制审计或云端策略验证。
- Intel Mac 缺少部分 ONNX 能力；不同硬件、模型、语言和噪声条件下的速度与质量不能互相外推。

## 补充建议

- 用虚构会议和 canary secrets 做本地/云端两套抓包，记录音频、转写、embedding、日志、缓存与 crash report 去向。
- 默认关闭截图、云同步、公开分享和日历；每项启用时单独说明数据接收方与删除机制。
- 按语言、口音、噪声、多人重叠和专有名词建立 WER/DER 与人工核对表。
- 对自动粘贴设置预览或确认键，并测试密码框、终端、聊天软件和远程桌面的焦点边界。
- 团队使用前核对角色权限、共享链接撤销、离职回收、数据导出与备份删除。

## 参考资料

- [GitHub 仓库](https://github.com/OpenWhispr/openwhispr)
- [GitHub REST API](https://api.github.com/repos/OpenWhispr/openwhispr)
- [v1.9.2 Release](https://github.com/OpenWhispr/openwhispr/releases/tag/v1.9.2)
- [官方文档](https://docs.openwhispr.com/)
- [MCP 集成](https://docs.openwhispr.com/integrations/mcp)
- [MIT License](https://github.com/OpenWhispr/openwhispr/blob/main/LICENSE)
