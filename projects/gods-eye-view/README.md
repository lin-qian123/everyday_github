<!-- markdownlint-disable MD013 -->

# God's Eye View（bilawalsidhu/gods-eye-view）中文解读

> 证据快照：2026-09-11（Asia/Shanghai）。GitHub REST API 显示 24,111 stars、5,020 forks、178 open issues；最新 release 与根 package 均为 `v0.1.1` / `0.1.1`。API 许可证字段为 `NOASSERTION`，但根 `LICENSE` 对源码给出 MIT，同时明确第三方数据、地图与 3D 资产不随源码获得 MIT 授权。本文未安装或运行项目，也未核验上游自报的跨平台播放量。

## 定位

God's Eye View 是一个在浏览器中融合地理空间公开信号的 3D globe：把航班、船舶、卫星、地震、道路交通、公共摄像头、火点、发射任务与基础设施叠加在同一视图，并用 OpenAI Realtime voice agent 操作场景、查询当前对象和生成简短 HUD 摘要。

它更接近可扩展的 GEOINT / OSINT 可视化与交互原型，不是“实时侦察卫星”。上游明确说明交通车辆是沿真实道路的模拟，摄像头姿态与火箭轨迹含估计，公开数据也存在时效、覆盖和误差边界。

## 用法

上游推荐 Node.js `24.14+` 或 `26.x`：

```bash
git clone https://github.com/bilawalsidhu/gods-eye-view.git
cd gods-eye-view
npm ci
npm run doctor
npm run dev
```

默认在 `http://localhost:4173` 打开。多数图层可无 key 启动；Photorealistic 3D、地点搜索、船舶、火点、实时交通和语音分别依赖 Cesium ion、Google Maps、AISStream、NASA FIRMS、TomTom、OpenAI 等 provider。正式使用前应逐项核对当前价格、地区、配额与许可。

## 原理

- 前端以 vanilla JavaScript、CesiumJS、Vite 和 GLSL 组织 globe、图层、传感器视觉风格与场景控制。
- 航班、卫星、地震、摄像头等模块分别调用公开或需凭据的数据源；缓存、轮询预算和 proxy 用于控制请求量。
- OpenAI Realtime agent 获取当前坐标、图层、选中实体和可选视口截图，通过 28 个工具控制相机、图层、标注和查询；浏览器只收到短时 session token。
- 服务器端代理保管 OpenAI、AISStream、OpenSky OAuth 等秘密；Google Maps 与 Cesium ion token 会进入浏览器，因此必须在 provider 侧限制来源与额度。

## 价值

- 把分散的空间数据源统一到可探索的 3D context，便于教学、演示、OSINT 原型和地理交互设计。
- 图层模块化、公开数据源清单和数据许可说明为添加自有数据提供了可读起点。
- voice agent 不只回答问题，还能调用明确的场景工具，展示领域对象如何变成 agent 可操作 surface。
- 上游主动区分 live、simulated、estimated 与 reconstructed，可作为科学/情报可视化证据标签的参考。

## 风险边界

- 公开数据的聚合、历史轨迹和摄像头投影仍可能造成跟踪、骚扰、误判或行动安全风险；“公开”不等于可无条件二次使用。
- 航班 ADS-B、OSM、公共摄像头、火点和新闻上下文本身可能延迟、缺失或错误；AI 摘要不能替代原始源核对。
- 根 MIT 只覆盖源码。TeleGeography 数据为 CC BY-NC-SA 3.0，OSM 派生数据涉及 ODbL，3D 模型和运行时 provider 各有独立条款；商业使用不能只看 GitHub badge。
- `.env` 是本地明文文件；旧版 Pinokio 配置面板曾记录提交值。即使默认绑定 localhost，主动开放到 LAN 后也会把代理的 provider 能力暴露给可达客户端。
- 上游性能、启动时间和“病毒式传播”数字是特定快照或自报材料，本页未独立复现。

## 补充建议

1. 先无 key 启动，只启用低敏感图层；确认来源、更新时间和模拟/估计标签正确显示。
2. 为浏览器可见 key 设置 URL 限制，为付费 provider 设置硬 quota、账单上限和轮换策略；敏感 key 优先放系统 keychain。
3. 对每个导出画面保存抓取时间、数据源、原始记录链接和转换步骤，避免把渲染效果当成事实证明。
4. 若做商业、研究或安全分析，先清点第三方数据/模型许可，并建立人工复核与误报更正流程。

## 参考资料

- GitHub：<https://github.com/bilawalsidhu/gods-eye-view>
- GitHub REST API：<https://api.github.com/repos/bilawalsidhu/gods-eye-view>
- Releases：<https://github.com/bilawalsidhu/gods-eye-view/releases>
- 数据来源与许可：<https://github.com/bilawalsidhu/gods-eye-view/blob/main/DATA_SOURCES.md>
- 安全说明：<https://github.com/bilawalsidhu/gods-eye-view/blob/main/SECURITY.md>
- 上游演示视频：<https://www.youtube.com/watch?v=GRJaKcXZS94>
- 上游 X 热度说明（2026-08-29）：<https://x.com/bilawalsidhu/status/2093798887815348521>
