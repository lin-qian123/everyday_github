<!-- markdownlint-disable MD013 -->

# CozyClay

> 更新：2026-11-24（Asia/Shanghai）。分类：语音、视频与多模态。当前上游 `HaD0Yun/CozyClay`；旧 `NomaDamas/CozyClay` API 指向同一仓库 ID `1315384578`，原位续更。固定 SHA `7645fc69eaa06e5c1d04429c779dcdd815bf14d7` 与 v3.3.0 tag 相同。本轮为文档和局部源码静态核读，未安装、登录模型、导出 / 观看视频或迁移工程；热度见[当日日报](../../daily/2026-11-24/ai-hotspots.md)。

## 定位

浏览器 3D 运动预演：先摆场景与人物，编动作和镜头，再把帧、参考片和提示词交给 AI 视频模型。3.3.0 改用第二个 motion writer 模型反复写运动规格、读取确定性引擎测量及 contact sheets，再安装 take；这仍是预演与参考条件，不能保证下游模型服从动作、镜头和剪辑。[README](https://github.com/HaD0Yun/CozyClay/blob/7645fc69eaa06e5c1d04429c779dcdd815bf14d7/README.md)

## 用法

上游常规入口为 `npx cozyclay`，Node `>=22.19.0` 与 Chromium；本机工作室默认 `http://127.0.0.1:5180/app/`。手动建场景无需本地 GPU、Python 或模型权重；Agent motion 需要模型登录 / key。MCP 入口 `npx -y cozyclay mcp`，CLI 可用 `cclay live status --wait` 观察运行中的工作室。[README](https://github.com/HaD0Yun/CozyClay/blob/7645fc69eaa06e5c1d04429c779dcdd815bf14d7/README.md)、[package.json](https://github.com/HaD0Yun/CozyClay/blob/7645fc69eaa06e5c1d04429c779dcdd815bf14d7/package.json)

**发行和包分开确认。** v3.3.0 GitHub Release 发布于 UTC 2026-11-23 22:57，即北京时间 11-24 06:57；npm 指定版本初查 404，07:06 复查指定版本与 `latest` 均 HTTP 200、版本 3.3.0。可用 `npx cozyclay@3.3.0` 固定包版本，或固定源码 SHA；这里只核元数据，未下载 / 验签包内容。常规 `npx cozyclay` 每次取新版本，而关闭 update check 不等于固定制品。[Release](https://github.com/HaD0Yun/CozyClay/releases/tag/v3.3.0)、[npm 指定版本元数据](https://registry.npmjs.org/cozyclay/3.3.0)、[README](https://github.com/HaD0Yun/CozyClay/blob/7645fc69eaa06e5c1d04429c779dcdd815bf14d7/README.md)

## 原理

场景 / cast / 镜头形成可编辑状态；motion writer 写规格，确定性引擎产帧并测滑步、接触、平衡和穿模，writer 根据结果迭代。默认尝试已登录服务可用的 `claude-opus-5-5` medium，否则回落会话模型；显式 CLIProxy 环境覆盖优先，账号拒绝目标模型后有会话级回退。它是多模型 / 多数据路径，不能只核聊天面板所选模型。[CHANGELOG](https://github.com/HaD0Yun/CozyClay/blob/7645fc69eaa06e5c1d04429c779dcdd815bf14d7/CHANGELOG.md)、[motion-writer.mjs](https://github.com/HaD0Yun/CozyClay/blob/7645fc69eaa06e5c1d04429c779dcdd815bf14d7/bin/agent/motion-writer.mjs)

AI video reference zip 在每四帧中导出一帧轻马赛克、三帧重模糊，每镜头重启序列，另带 `prompt.txt` 与 `scene-facts.json`。这是面向 Seedance 类视频模型的条件构造；“保持 blocking”是上游预期，仍需实片检验。[CHANGELOG](https://github.com/HaD0Yun/CozyClay/blob/7645fc69eaa06e5c1d04429c779dcdd815bf14d7/CHANGELOG.md)

## 价值

适合把人物位置、走位、镜头和切点提前做成可编辑资产，降低文字提示的歧义，也便于把同一预演交给多个视频后端对照。节省多少付费生成与返工，要按固定镜头、模型、失败样本和人工验收统计，不能只看作者演示片。

## 风险边界

- **旧工程兼容性有破坏。** 3.3.0 移除 storyboard project；旧 storyboard 打开为新建未保存的 animation，保存不覆盖原文件。新版本镜头文档为 v8，3.2.3 打开时没有镜头；保留原工程和旧版副本，不能把降级当成无损恢复。旧 pose library / still shots 等也有移除。[CHANGELOG](https://github.com/HaD0Yun/CozyClay/blob/7645fc69eaa06e5c1d04429c779dcdd815bf14d7/CHANGELOG.md)
- **运动测量不等于画面完全正确。** 新 motion 只驱动 rig characters；capsule 与 imported rigs 原样站立。手接触可能差数厘米，默认 cube 外观和底层 rig 接触面不一致；手写高度须按当前显示身体尺度。上游另列手动转 rail 的描述与 shot action sentence 缺口。[CHANGELOG](https://github.com/HaD0Yun/CozyClay/blob/7645fc69eaa06e5c1d04429c779dcdd815bf14d7/CHANGELOG.md)
- **费用面板不完整。** motion writer 的 token 不显示在 Agent 用量 / 成本里；一次 motion 可耗数分钟和多轮调用。发行记录只报告 CLIProxyAPI 上指定模型的真实运行，其他登录和 fallback 是 stand-in server 检查；不外推为所有 provider 兼容。[CHANGELOG](https://github.com/HaD0Yun/CozyClay/blob/7645fc69eaa06e5c1d04429c779dcdd815bf14d7/CHANGELOG.md)
- **托管网页会录屏，npm 不录 replay。** 隐私文档称官网托管 `/app/` 默认 PostHog US Cloud session replay，3D viewport 2 fps，输入与 Agent transcript 遮罩，不采 console / 网络内容；landing 与 npm 不录 replay。官方 npm 仍默认用量遥测，源码 checkout 不发，不能写成“本地绝无出口”或“所有分发都录屏”。这是文档 / 配置核验，未抓包验证遮罩。[privacy.md](https://github.com/HaD0Yun/CozyClay/blob/7645fc69eaa06e5c1d04429c779dcdd815bf14d7/docs/privacy.md)、[analytics-values.js](https://github.com/HaD0Yun/CozyClay/blob/7645fc69eaa06e5c1d04429c779dcdd815bf14d7/src/analytics-values.js)
- `cclay telemetry off` 清除 npm 标识，`COZYCLAY_TELEMETRY=0` / `DO_NOT_TRACK=1` 为启动时禁用；损坏的状态文件回落 telemetry on。关闭统计不关闭模型和生成服务，motion 记录 / contact sheets / clip 还在本机配置目录的 `motion-runs/` 保留最近 20 次。[telemetry-state.mjs](https://github.com/HaD0Yun/CozyClay/blob/7645fc69eaa06e5c1d04429c779dcdd815bf14d7/bin/telemetry-state.mjs)、[CHANGELOG](https://github.com/HaD0Yun/CozyClay/blob/7645fc69eaa06e5c1d04429c779dcdd815bf14d7/CHANGELOG.md)
- 组合程序为 AGPL-3.0-or-later；修改后网络服务的对应源码入口由 `VITE_SOURCE_CODE_URL` 指定。素材、字体、模型和权重仍各自遵守条款。[LICENSING.md](https://github.com/HaD0Yun/CozyClay/blob/7645fc69eaa06e5c1d04429c779dcdd815bf14d7/LICENSING.md)

## 补充建议

先用无敏感资产、单 rig、两镜头测试保存 / 重开 / 导出，并保留升级前副本。将运动规格的米制坐标、显示人物尺度、contact sheet 与全片逐帧对照；费用同时读 provider 账单和 motion 运行记录。完成预演 QA 后，再用同一模型和小额限额比较参考片是否减少失败 take，最后完整观看与回听。

## 参考资料

- [当前仓库](https://github.com/HaD0Yun/CozyClay)、[旧 API 的迁移指针](https://api.github.com/repos/NomaDamas/CozyClay)、[当前 API](https://api.github.com/repos/HaD0Yun/CozyClay)、[v3.3.0](https://github.com/HaD0Yun/CozyClay/releases/tag/v3.3.0)
- 固定 SHA 的 [README](https://github.com/HaD0Yun/CozyClay/blob/7645fc69eaa06e5c1d04429c779dcdd815bf14d7/README.md)、[manifest](https://github.com/HaD0Yun/CozyClay/blob/7645fc69eaa06e5c1d04429c779dcdd815bf14d7/package.json)、[变更及限制](https://github.com/HaD0Yun/CozyClay/blob/7645fc69eaa06e5c1d04429c779dcdd815bf14d7/CHANGELOG.md)
- [隐私](https://github.com/HaD0Yun/CozyClay/blob/7645fc69eaa06e5c1d04429c779dcdd815bf14d7/docs/privacy.md)、[统计开关](https://github.com/HaD0Yun/CozyClay/blob/7645fc69eaa06e5c1d04429c779dcdd815bf14d7/bin/telemetry-state.mjs)、[托管录屏配置](https://github.com/HaD0Yun/CozyClay/blob/7645fc69eaa06e5c1d04429c779dcdd815bf14d7/src/analytics-values.js)、[模型路由](https://github.com/HaD0Yun/CozyClay/blob/7645fc69eaa06e5c1d04429c779dcdd815bf14d7/bin/agent/motion-writer.mjs)、[许可说明](https://github.com/HaD0Yun/CozyClay/blob/7645fc69eaa06e5c1d04429c779dcdd815bf14d7/LICENSING.md)
