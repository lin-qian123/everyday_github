<!-- markdownlint-disable MD013 -->

# ComfyUI

> 更新：2026-10-19（Asia/Shanghai）。分类：语音、视频与多模态。上游 `Comfy-Org/ComfyUI`；本文基于官方榜单、认证 API 与文档 / 源码静态核验，未安装运行。源码快照 `8f04fd6ecf4a`；Release 与主分支行为分别说明。热度见[当日官方榜单](https://github.com/trending/python?since=daily)。

## 定位

通过节点图组织图像、视频、音频、3D 等模型工作流的创作引擎，含本地 core / API、独立 frontend、desktop 和付费 cloud 路线。支持模型、LoRA、采样、媒体处理与第三方 custom nodes；不是单个生成模型。[来源 1](https://github.com/Comfy-Org/ComfyUI/blob/8f04fd6ecf4a548937971e840af2a985529fab76/README.md)

官方综合 / Python Trending 约 +155 当日 stars；API 为 138,573 / 16,499 / 5,256（stars / forks / open issues）。采样 latest Release 为 v0.42.0，而 tags 首项已为 v0.42.1；读取的源码 version 文件仍为 0.42.0，三种信号不混作同一状态。核心 GPL-3.0。[来源 2](https://api.github.com/repos/Comfy-Org/ComfyUI)[来源 3](https://github.com/Comfy-Org/ComfyUI/releases/tag/v0.42.0)[来源 7](https://github.com/Comfy-Org/ComfyUI/blob/8f04fd6ecf4a548937971e840af2a985529fab76/LICENSE)[来源 8](https://github.com/Comfy-Org/ComfyUI/blob/8f04fd6ecf4a548937971e840af2a985529fab76/comfyui_version.py)

## 用法

新用户可按官网选择 desktop；手动安装则先按 GPU / OS 选择 PyTorch，再装 core 依赖并放置有权使用的模型。首轮使用官方基础 workflow、固定 seed 和本地模型，在无敏感素材的目录验证。[来源 1](https://github.com/Comfy-Org/ComfyUI/blob/8f04fd6ecf4a548937971e840af2a985529fab76/README.md)

```bash
# 手动安装依赖后启动本地测试；本轮未执行
python main.py --listen 127.0.0.1 --port 8188 --offline --disable-all-custom-nodes
```

打开回环地址 8188，保存 workflow JSON、模型 hash、seed 与输出。前端与 core / 自定义节点版本要配套，不要直接把 master、desktop 和不同日期教程混装。

## 原理

节点图表达模型加载、条件、采样、解码与媒体处理依赖；执行器按图调度并可复用未变化节点结果。workflow 可存 JSON，部分生成媒体也携带恢复工作流所需 metadata；API 可将相同图接入应用。[来源 1](https://github.com/Comfy-Org/ComfyUI/blob/8f04fd6ecf4a548937971e840af2a985529fab76/README.md)

本地 core 之外还有 paid partner / API nodes。`--disable-partner-nodes` 只关闭这类节点，frontend 仍可联网；`--offline` 同时限制 frontend CSP 并禁用 partner nodes，不能等同于从操作系统封住任意第三方 Python 网络。[来源 4](https://github.com/Comfy-Org/ComfyUI/blob/8f04fd6ecf4a548937971e840af2a985529fab76/comfy/cli_args.py)

## 价值

适合需要精确控制模型与中间步骤、比较参数或复用创作流程的用户，也便于把图工作流交给前端或应用执行。其价值在可组合和可追溯；“最快”“低显存可运行”等上游宣传没有本轮硬件和质量复测支持。

## 风险边界

- SECURITY.md 的信任模型是默认 127.0.0.1 且访问 URL 的人可信；裸 `--listen` 会改为全接口，公网 / 局域网部署需另配认证、TLS 与防火墙。[来源 4](https://github.com/Comfy-Org/ComfyUI/blob/8f04fd6ecf4a548937971e840af2a985529fab76/comfy/cli_args.py)[来源 5](https://github.com/Comfy-Org/ComfyUI/blob/8f04fd6ecf4a548937971e840af2a985529fab76/SECURITY.md)
- custom nodes 是任意 Python，源码通过模块加载执行；workflow 来源可信不等于所需插件可信。`--disable-all-custom-nodes` 是建立基础对照的办法，并非系统 sandbox。[来源 4](https://github.com/Comfy-Org/ComfyUI/blob/8f04fd6ecf4a548937971e840af2a985529fab76/comfy/cli_args.py)[来源 6](https://github.com/Comfy-Org/ComfyUI/blob/8f04fd6ecf4a548937971e840af2a985529fab76/nodes.py)
- `--offline` 的内置网络限制范围应逐组件核实，在线节点、插件下载器、frontend、模型下载和系统出站是不同路径。
- 模型 checkpoint、LoRA、输入素材和生成内容各有授权 / 隐私边界；根 GPL-3.0 不覆盖所有权重和素材。[来源 7](https://github.com/Comfy-Org/ComfyUI/blob/8f04fd6ecf4a548937971e840af2a985529fab76/LICENSE)
- 图缓存、随机性、后端数值和显存卸载可改变复现表现。权重体积不是峰值 RAM / VRAM，生成成功也不等于质量或业务可用。
- core / frontend / desktop 发行节奏不同，Release、tag 与主分支 snapshot 需分别记录。本轮未运行工作流或下载模型。

## 补充建议

先以禁用 custom nodes / partner nodes 的基础图做对照，记录模型 hash、core / frontend / torch / driver、耗时和峰值内存；再一次只添加一个插件或在线节点，检查依赖、流量、素材去向和成本。团队共享服务应单独做用户授权与输出隔离验收。

## 参考资料

1. [README 与工作流](https://github.com/Comfy-Org/ComfyUI/blob/8f04fd6ecf4a548937971e840af2a985529fab76/README.md)
2. [仓库 API](https://api.github.com/repos/Comfy-Org/ComfyUI)
3. [v0.42.0 Release](https://github.com/Comfy-Org/ComfyUI/releases/tag/v0.42.0)
4. [网络、offline 与插件参数](https://github.com/Comfy-Org/ComfyUI/blob/8f04fd6ecf4a548937971e840af2a985529fab76/comfy/cli_args.py)
5. [安全信任模型](https://github.com/Comfy-Org/ComfyUI/blob/8f04fd6ecf4a548937971e840af2a985529fab76/SECURITY.md)
6. [Custom node 加载](https://github.com/Comfy-Org/ComfyUI/blob/8f04fd6ecf4a548937971e840af2a985529fab76/nodes.py)
7. [LICENSE](https://github.com/Comfy-Org/ComfyUI/blob/8f04fd6ecf4a548937971e840af2a985529fab76/LICENSE)
8. [源码版本文件](https://github.com/Comfy-Org/ComfyUI/blob/8f04fd6ecf4a548937971e840af2a985529fab76/comfyui_version.py)
9. [官方产品与社媒回链](https://www.comfy.org/)
