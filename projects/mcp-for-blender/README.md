<!-- markdownlint-disable MD013 -->

# MCP for Blender（ahujasid/mcp-for-blender）中文解读

> 上游仓库：<https://github.com/ahujasid/mcp-for-blender> · 归类：语音、视频与多模态 · 证据快照：2026-10-16（Asia/Shanghai）。API：30,960 stars / 2,817 forks / 51 open issues；MIT；无 GitHub Release / tag，Python manifest `2.1.9`；旧名 `blender-mcp`。本页为上游文档与相关源码的静态整理，未安装运行、接入真实数据 / 凭据、复测性能或完成全面安全审计。

## 定位

MCP for Blender 是第三方 Blender 与 LLM 的桥接项目，原名 `blender-mcp`。它将场景检查、viewport 观察、Python 执行、素材搜索 / 导入与部分 3D 生成接成 MCP tools，帮助 Agent 在实际 3D 编辑器中迭代。上游明确与 Blender Foundation 无官方隶属关系。

## 用法

在已备份的测试工程和独立 Blender profile 中安装；官方 `uvx mcp-for-blender setup` 会选择 MCP 客户端、写配置并安装 / 启用 addon，执行前先查看预期修改。若手动接入，客户端以 stdio 启动 `uvx mcp-for-blender`，再启用 Blender addon 的本地 server。先设置 `DISABLE_TELEMETRY=true`，用 `get_scene_info` / `look` 检查空白场景，之后才尝试单物体编辑；部署固定包版本与 addon 副本。

## 原理

- MCP server 将 tool 请求转成 JSON-over-TCP，addon 默认监听 `localhost:9876`，在 Blender 主线程调度实际场景操作。
- `execute_blender_code` 可调用 Blender Python API；`look` 提供 viewport、camera、多视图或动画帧反馈，形成观察与修改闭环。
- Poly Haven、Sketchfab、Poly Pizza 等提供素材；Tripo、Hunyuan3D、Hyper3D 等生成服务属于另外的数据、凭据与费用链。

## 价值

- 直接修改可编辑场景，便于在几何、材质、灯光和视角之间迭代，并由人继续在 Blender 中修订。
- 工具返回视图，能暴露“脚本执行成功但画面不符合意图”的差异。
- 素材导入会保留部分来源与署名元数据，有助于人工追踪，但仍需逐素材核对权利。

## 风险边界

- `execute_blender_code` 在 Blender 内执行任意 Python，权限接近当前用户；loopback TCP 本身不构成 sandbox，勿将端口直接开放到外网。
- README 的“telemetry opt-in”特指内容采集：默认仍发送 install / session ID、工具名、成功、耗时、版本、OS 和时间；同意后还可收集 prompt、代码、截图、scene 与 trajectory，用于研究或训练。完全关闭需使用环境变量。
- setup / update 会修改客户端配置与 addon，旧 package 名、PyPI 版本和无 GitHub tag 的发布状态要区分。
- 生成模型与第三方资产可能联网、计费或要求署名；好看的 viewport 不能证明拓扑、尺度、渲染、导出和许可均合格。

## 补充建议

- 在工程副本验证只读检查 → 一次修改 → 保存 → 重开 → 导出，记录 mesh、材质、单位与文件差异。
- 使用低权限用户和最少网络出口，关闭不需要的 asset / generator 集成，私有场景禁用内容遥测。
- 保存 MCP 包、addon、Blender 版本和素材来源清单，先由人工审阅 Agent 的 Python 再运行。

## 参考资料

- 上游仓库：<https://github.com/ahujasid/mcp-for-blender>
- GitHub REST API：<https://api.github.com/repos/ahujasid/mcp-for-blender>
- README 与客户端设置：<https://github.com/ahujasid/mcp-for-blender/blob/main/README.md>
- Addon / TCP 执行层：<https://github.com/ahujasid/mcp-for-blender/blob/main/addon.py>
- 遥测实现：<https://github.com/ahujasid/mcp-for-blender/blob/main/src/blender_mcp/telemetry.py>
- 遥测条款：<https://github.com/ahujasid/mcp-for-blender/blob/main/TERMS_AND_CONDITIONS.md>
- Python manifest：<https://github.com/ahujasid/mcp-for-blender/blob/main/pyproject.toml>
- LICENSE：<https://github.com/ahujasid/mcp-for-blender/blob/main/LICENSE>
- Releases：<https://github.com/ahujasid/mcp-for-blender/releases>
