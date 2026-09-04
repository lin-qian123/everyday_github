<!-- markdownlint-disable MD013 -->

# text-to-cad（earthtojake/text-to-cad）

> 记录日期：2026-09-05（Asia/Shanghai）。本页依据上游 README、skills、release 与 GitHub API 做静态整理；未生成、切片、加工或打印任何实体零件。

## 定位

`text-to-cad` 是面向 CAD、CAE、CAM 与机器人描述文件的 agent skills 库。它把 CAD 建模、STEP 零件检索、DXF、URDF、SRDF、SDF、可视化、DfAM 检查、G-code 和部分打印机交接拆成独立技能，主张从本地项目文件生成、检查和交付工程产物。

2026-09-05 的 GitHub 官方 Python Trending 快照显示约 `+88 stars today`；REST API 快照为 `14,337 stars / 1,520 forks / 18 open issues`，许可证为 MIT，最新 release 是 `0.4.28`（2026-08-26）。

## 用法

上游推荐通过 Skills CLI 安装：

```bash
npx skills add earthtojake/text-to-cad
```

也提供 Codex、Claude Code 和 Grok Build 的 provider-native plugin 入口。安装或更新前应固定 commit / release，并只启用当前任务需要的 skill；CAD 生成、slicer、Bambu 上传和开始打印属于不同风险级别，不能一次性无条件授权。

## 原理

- **技能路由**：每个 `SKILL.md` 定义一种窄任务的步骤、工具和验收点。
- **可编辑源优先**：CAD skill 以 STEP 等工程格式为主，并可派生 STL、3MF、GLB。
- **机器人描述链**：URDF 描述 link / joint / inertial / mesh，SRDF 补 MoveIt planning group、end effector 和 collision rule，SDF 描述仿真模型与 world。
- **本地查看与检查**：CAD Viewer 提供本地浏览器预览，DfAM skill 测壁厚、悬垂、支撑量和构建方向。
- **制造交接**：G-code skill 调真实 slicer CLI，打印机 skill 把 dry-run、上传和启动分开。
- **供应件检索**：`step.parts` skill 用于查找螺钉、轴承、电机和连接器等现成 STEP 模型。

## 价值

- 将通用 agent 的模糊“画个零件”请求转成更具体的工程文件、检查与交付流程。
- 同时覆盖机械 CAD、二维制造图、机器人描述和增材制造，减少工具链切换成本。
- skill 文本可以版本化审查，便于团队固化输出格式和验收门槛。
- 对 agent 来说，先输出可编辑工程源再导出网格，比只交付不可追溯图片更有复用价值。

## 风险边界

- 生成成功、文件可打开或 STL watertight 都不能证明尺寸语义、装配、公差、受力、材料或制造安全正确。
- DfAM 指标依赖工艺、材料、设备和 slicer profile；自动检查不能替代工程签字或试制。
- URDF / SDF / SRDF 中的 joint limit、inertial、collision 和 frame 错误可能导致仿真与真机危险。
- 从第三方下载的 STEP 件仍需核对型号、revision、许可证和供应商图纸。
- plugin / skill 更新会改变提示和工具权限；`add` 覆盖安装且不会自动删除上游退役 skill，需显式审计漂移。
- 上传或开始打印是物理世界动作，必须使用 dry-run、测试机、人工确认和急停策略。

## 补充建议

- 每次交付至少验证单位、包围盒、关键截面、封闭面、孔深、壁厚和导出格式。
- 保留参数化源、STEP、网格、切片配置、预览图和验证 JSON，避免只保留最终 STL / G-code。
- 将“生成”“几何检查”“工程审核”“制造准备”“设备启动”设为独立批准门。
- 对机器人描述运行 frame tree、joint limit、collision 和惯量合理性测试，再进入真机。
- 对高风险零件进行专业 FEA、材料与制造审核；本项目不应承担最终工程认证。

## 参考资料

- [GitHub 仓库](https://github.com/earthtojake/text-to-cad)
- [GitHub REST API](https://api.github.com/repos/earthtojake/text-to-cad)
- [官方文档](https://www.texttocad.dev)
- [Skills 目录](https://github.com/earthtojake/text-to-cad/tree/main/skills)
- [0.4.28 Release](https://github.com/earthtojake/text-to-cad/releases/tag/0.4.28)
- [作者在 X 的入口](https://x.com/earthtojake)
