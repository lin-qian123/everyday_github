<!-- markdownlint-disable MD013 MD034 -->

# fugleramme：把本地鸟声识别映射到电子墨水自然图鉴

> 上游仓库：https://github.com/arnegiacomo/fugleramme · 归类：语音、视频与多模态 · 本页基于 2026-09-18 的 README、硬件 / 安装文档、`pyproject.toml`、release 与多类许可证静态整理；未采购硬件，也未复现物种识别。

## 定位

fugleramme 是运行在 Raspberry Pi 上的本地 AI 鸟类展示系统：BirdNET-Go 从麦克风音频识别物种，fugleramme 轮询结果、匹配人工整理的 19 世纪自然史插画，再把近期鸟类排版到彩色电子墨水屏或 Web kiosk。

2026-09-18 的 GitHub 官方 Python Trending 抓取显示约 `+712 stars today`；REST API 快照为 `2,896 stars / 69 forks / 8 open issues`。代码为 MIT，`v0.22.1` 于 9 月 17 日发布，Python 要求 `>=3.11`；BirdNET 与图像、字体、数据另有许可证。

## 用法

开发模式可使用 fake detector；树莓派与容器路径分别为：

```sh
uv sync
uv run fugleramme-fake-detector
uv run fugleramme-dev
```

```sh
docker run -d -p 8080:8080 -v fugleramme:/data \
  -e FUGLERAMME_DETECTOR_URL=http://birdnet.local:8080 \
  ghcr.io/arnegiacomo/fugleramme
```

电子墨水屏不是必需，Web kiosk 可单独运行；真实检测还需另行部署 BirdNET-Go 和音频输入。

## 原理

- BirdNET-Go 负责声学分类，fugleramme 只消费其 API，不在自身进程里完成模型推理。
- 识别结果映射到 400 多种物种、800 多个手工抠图，按体重和页面位置排版，仅在鸟类集合变化时刷新低频电子墨水屏。
- 管理页配置展示规则，服务持久化数据到 `/data`，kiosk 可在同机屏幕或局域网浏览器显示。
- fake detector、测试与 web-only 模式让 UI / 排版可以脱离户外硬件开发。

## 价值

- 是少见的“AI 退到后台”案例：分类器承担一个窄任务，前台展示保留可追溯的历史插画而非无限生成内容。
- 音频、本地推理、公共领域资料、电子墨水和家庭部署形成清楚、可复制的端到端项目。
- 只在状态变化时刷新适合低功耗、环境式显示，不与手机通知竞争注意力。
- 上游明确列出艺术、模型、字体与数据来源，比只写代码许可证更利于复用判断。

## 风险边界

- BirdNET-Go / 模型采用 CC BY-NC-SA 4.0 等非商业条款，不能因 fugleramme 代码是 MIT 就假设整套设备可任意商用。
- 物种识别受麦克风、背景噪声、地区、季节、阈值与模型覆盖影响；电子墨水上出现插画不是可靠的生态调查记录。
- 欧洲物种插画覆盖最好，其他地区缺图会造成展示偏差；插画尺寸和构图也不是科学测量。
- 麦克风持续采集可能录到人声；即使本地处理，也需要安装位置、保存策略和局域网访问控制。
- 一键安装、自动更新、Docker、管理页和网络可达 BirdNET API 都扩大供应链与局域网攻击面。
- 本页未运行模型、硬件或 `v0.22.1`，未测误报/漏报、刷新寿命、功耗、断网恢复或不同屏幕兼容性。

## 补充建议

1. 先用 web-only + fake detector 验证布局，再以录音金标统计本地常见物种的 precision / recall 和阈值敏感性。
2. 麦克风只覆盖室外目标区域，不保留原始音频；为管理页、BirdNET API 和 kiosk 设置 VLAN、loopback 或访问控制。
3. 固定容器 digest 与 `v0.22.1`，备份 `/data`，测试断电、磁盘损坏、更新失败和屏幕刷新异常。
4. 商用、展览或再分发前逐项审查 BirdNET、插画、字体和数据 attribution，不能只引用根 LICENSE。

## 参考资料

- 上游 README：https://github.com/arnegiacomo/fugleramme
- 硬件文档：https://github.com/arnegiacomo/fugleramme/blob/main/docs/hardware.md
- 安装文档：https://github.com/arnegiacomo/fugleramme/blob/main/docs/install.md
- `v0.22.1` release：https://github.com/arnegiacomo/fugleramme/releases/tag/v0.22.1
- GitHub REST API：https://api.github.com/repos/arnegiacomo/fugleramme
- LICENSE：https://github.com/arnegiacomo/fugleramme/blob/main/LICENSE
