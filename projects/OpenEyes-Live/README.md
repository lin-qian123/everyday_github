# OpenEyes-Live

## 定位

`OpenEyes-Live` 是模块化、可插拔的端侧多模态运行时，面向摄像头与麦克风的离线实时理解；README 列出 CLIP、Phi-3.5 Vision、Silero VAD、SenseVoice ASR 与 ERes2Net 声纹等可选引擎。截至 2026-07-26，仓库创建于 2026-07-25，约 2 stars、0 forks，Apache-2.0 许可。

## 用法

克隆后执行 `pip install -r requirements.txt` 与 `pip install -e .`，再用 CLI 查看可用子引擎。按需下载模型，例如 `openeyes install encoder`、`openeyes install llm`、`openeyes install vad` 或 `openeyes install asr`；先关闭真实摄像头/麦克风输入，用录制的无敏感样本验证单个引擎和模型磁盘占用。

## 原理

系统以 scheduler 管理可独立下载、加载和组合的视觉、语音、VAD、说话人识别等 engine，并提供生命周期管理与 MCP gateway。端侧执行可减少原始音视频上云，但模型下载、镜像、日志和任何网关配置仍需单独审计。

## 价值

- 将实时多模态能力拆成可替换模块，便于按硬件和任务选择模型。
- 离线处理有潜力减少持续上传摄像头/麦克风数据的暴露面。
- Apache-2.0 与跨平台声明使其可作为本地多模态原型的观察样本。

## 风险边界

- 摄像头、麦克风、声纹和人脸场景属于高敏感数据；本地运行不自动等于合规或已取得同意。
- README 中的引擎大小、性能和测试徽章应由目标机器实测，不能视为生产 SLA。
- 模型下载与 MCP gateway 可能重新引入网络、供应链和权限风险。

## 补充建议

默认禁用网络出口和自动模型下载，明确可见的录制提示与同意机制；分别测量端侧 CPU/GPU、内存、延迟、误报与跨平台兼容性。若启用 speaker ID 或持续监控，先完成法律与组织层面的授权审查。

## 参考资料

- GitHub：<https://github.com/vfvincentwong2026/-OpenEyes-Live>
- 架构文档：<https://github.com/vfvincentwong2026/-OpenEyes-Live/blob/main/docs/ARCHITECTURE.md>
