# AbaoPal

- 仓库：[banye-technology/AbaoPal](https://github.com/banye-technology/AbaoPal)
- 快照：2026-08-04；创建于 2026-08-03，约 6 stars、0 forks，MIT。
- 分类：前端、UI 与 Agent 交互层

## 定位

Android 端的开源手机自动化 agent。它让自然语言任务经由规划、执行与结果判断循环，结合无障碍 UI 树、屏幕截图、可编辑录制步骤、YAML skills、语音和定时入口跨应用操作。

## 用法

按 README 配置 Android SDK、JDK 17 与本机 `local.properties`，执行 Gradle 单测、lint 和 debug 构建后，仅在测试设备启用无障碍与悬浮窗权限。先从打开设置、搜索和录制可逆步骤开始；涉及支付、密码、验证码和身份资料时立即人工接管。

## 原理

`Planner`、`Executor`、`Director` 等组件基于事件总线协作：文本 UI 树和截图提供双通道感知，无障碍动作、手势和 Intent 执行操作，屏幕反馈驱动下一轮规划。技能可通过本地存储和向量检索匹配任务语境。

## 价值

原生 Android 形态使移动端 computer-use 的权限、可观测界面与可回放任务同时可见，适合评估多模态模型在真实 UI 波动下的可靠性。

## 风险边界

无障碍、截图、麦克风、悬浮窗、跨应用动作以及可选云端 LLM/ASR/TTS 会扩大隐私与操作风险。有限关键词/包名拦截不是完整安全保障；应用更新、ROM 差异、网络和模型失误都会导致误操作。

## 补充建议

使用独立测试账号和无敏感数据设备；为每个 skill 建立允许应用、动作、时间和人工确认清单，保存最小化日志并测试紧急停止。发布前还应审查供应链、云端数据流和无障碍政策合规。

## 参考资料

- [项目 README](https://github.com/banye-technology/AbaoPal)
- [GitHub API 元数据快照](https://api.github.com/repos/banye-technology/AbaoPal)
