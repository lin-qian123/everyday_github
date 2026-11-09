<!-- markdownlint-disable MD013 -->

# GeoLibre

## 定位

GeoLibre 是 OpenGeos 的 GIS 可视化与处理平台，同一项目可在浏览器、桌面、移动端和 Jupyter 使用，并提供 AI assistant、MCP 项目构建与桌面控制。AI 辅助操作，空间数据、坐标与分析有效性仍需核验。

- 上游：[opengeos/GeoLibre](https://github.com/opengeos/GeoLibre)，仓库 ID `1251648409`。
- 2026-11-10：8,522 stars / 955 forks / 20 open issues（含 PR）；TypeScript daily +66。
- 稳定发行 [v3.7.0](https://github.com/opengeos/GeoLibre/releases/tag/v3.7.0)，UTC 11-08；PyPI 同版、Python ≥3.11。本页按主线 `9ac3f0367d53f40933e2c11a654cd977408589ea` 静态核读，配置不自动适用全部发行构建。

## 用法

1. 在 Web 或桌面版打开公开小数据，先核 CRS、单位、范围与属性；COG / GeoParquet / PMTiles 等云格式还要核实际源站。
2. 将图层、样式、视图与处理流程保存为项目，再导出重开。3.7.0 新增室内地图 / 楼层、I3S 与 JAXA Earth 相关能力，格式与后端条件分别核。
3. MCP 安装入口为 `python -m pip install "geolibre[mcp]"`，创建专用目录后运行 `geolibre-mcp --root ./maps`；默认 stdio，无 root 时使用当前目录，因此不要从家目录启动。
4. 文件工具无界面生成项目；`live_*` 操作打开的桌面地图，修改停留在会话直到从应用保存。两者都要与意图和最终文件对照。

本轮未安装应用、处理数据、运行 MCP 或接云服务。

## 原理

平台以 React / TypeScript、MapLibre、deck.gl 和 DuckDB-WASM Spatial 组织图层与查询，Tauri 提供原生宿主。可切 MapLibre、Mapbox、Cesium、ArcGIS 渲染器，功能与凭据并不完全相同；部分处理走 WASM，另可使用本机 Python helper。

MCP 在 Python authoring 层生成应用可重开的项目。抽查 `workspace.py` 可见路径 canonicalize、允许根、格式后缀和覆盖开关检查；预览网络模块另有公网地址、授权和请求限制。文件根、预览网络与桌面 live relay 是不同边界。

## 价值

- 降低教学、数据初查与跨设备展示的环境门槛，保留开放项目文件。
- 组合空间 SQL、地图与可保存流程；AI 可辅助创建图层和流程，结果需回到数据与算法。
- 浏览器处理减少大文件整体上传，但吞吐、内存和工具兼容性要按数据测量；工具数量不等于逐项正确性。

## 风险边界

- **明确数据出口**：隐私政策说明 AI 发 prompts、图层名与属性字段名给 LLM；协作经 relay 共享项目及本地 GeoJSON，Project → Share 上传项目并嵌入本地矢量层。
- **应用与网站统计不同**：政策称安装应用不采自身 analytics，官网与托管 Web 使用 GA4。默认底图、插件注册表、更新和 DuckDB 扩展仍请求网络；插件注册表依据已有下载请求计算使用量。
- **部署策略有层次**：公开的 `deployment.json` 不能放 secret。客户端 plugin policy / 界面隐藏不是服务端安全边界，Docker 门禁另核；缺失、无效、超时的策略不能当作已成功限制。
- **空间数值定义**：CRS / 椭球、轴顺序、单位、NoData、重采样和空间连接影响结果；AI 生成地图不能直接作为测绘或灾害决策依据。
- **许可分层**：根 MIT 不自动涵盖底图、数据、SDK、插件或模型，本轮未逐一审第三方资产。

## 补充建议

以公开小数据核已知坐标、距离 / 面积和空间 SQL，保留输入、项目、导出哈希与参数。逐项列 LLM、协作、分享、插件和数据服务出口；专用 MCP root 与网络限制要实测，项目生成成功不等于分析正确或数据从未离机。

## 参考资料

- [固定 SHA README：平台与教程](https://github.com/opengeos/GeoLibre/blob/9ac3f0367d53f40933e2c11a654cd977408589ea/README.md)
- [MCP 的文件、预览与 live 差异](https://github.com/opengeos/GeoLibre/blob/9ac3f0367d53f40933e2c11a654cd977408589ea/docs/mcp.md)
- [路径与写入检查](https://github.com/opengeos/GeoLibre/blob/9ac3f0367d53f40933e2c11a654cd977408589ea/python/src/geolibre/mcp/workspace.py)、[预览网络模块](https://github.com/opengeos/GeoLibre/blob/9ac3f0367d53f40933e2c11a654cd977408589ea/python/src/geolibre/mcp/network.py)
- [隐私政策：2026-11-07 更新](https://github.com/opengeos/GeoLibre/blob/9ac3f0367d53f40933e2c11a654cd977408589ea/docs/privacy.md)
- [部署策略与失败行为](https://github.com/opengeos/GeoLibre/blob/9ac3f0367d53f40933e2c11a654cd977408589ea/docs/deployment-policy.md)
- [根许可证](https://github.com/opengeos/GeoLibre/blob/9ac3f0367d53f40933e2c11a654cd977408589ea/LICENSE)、[PyPI 快照](https://pypi.org/pypi/geolibre/json)
