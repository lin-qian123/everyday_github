<!-- markdownlint-disable MD013 -->

# Portable Local Studio：整合图像、聊天与语音的本地工作台

- 上游：[techjarves/Portable-Local-Studio](https://github.com/techjarves/Portable-Local-Studio)；分类：语音、视频与多模态。
- 更新：2026-11-03（Asia/Shanghai）；固定主线 SHA：`3f0830f527d4a3c3bf8664ecbbb293043dd496f2`。
- 热度快照：JavaScript daily +75；API 1,803 stars / 445 forks / 7 open issues（含 PR）。发行列表为空；界面 / README 品牌为 Portable AI Studio，目录保留上游仓库名。
- 证据：官方 Trending / API 与固定源码静态核读；下文用法供复核，不表示本轮已运行。

## 定位

项目以浏览器 GUI 统一 stable-diffusion.cpp 图像生成、llama.cpp GGUF 聊天、whisper.cpp 转写和 Kokoro TTS。它主要封装启动、模型管理与后端进程，不是新的基础模型，也不保证所有任务在所有 GPU / NPU 上均加速。

## 用法

从上游 checkout 检查启动与 setup 脚本后，按平台运行 windows.bat、linux.sh 或 mac.sh。macOS 的预构建支持 Apple silicon，README 明确不支持 Intel Mac：

```sh
git clone https://github.com/techjarves/Portable-Local-Studio
cd Portable-Local-Studio
chmod +x mac.sh
./mac.sh
```

首次启动会按缺失项安装便携 Node.js、依赖与后端，模型需下载或自行导入。随后访问 localhost:1420。图像放 app/models，聊天 GGUF 放 app/llm-models，Whisper 模型放 app/speech-models；不能只凭扩展名把不同任务的权重混用。

## 原理

- React 前端调用本地 Node server，由 server 管理图像、聊天、语音后端与输出。
- 平台脚本选择 Metal、CUDA、Vulkan、ROCm 等二进制，部分路径可回退或构建；llm-backends.json 单列 llama.cpp 后端来源。
- Model Manager 把模型下载到任务目录；视觉聊天可能还需要对应 mmproj。
- serve.cjs 的聊天路径只有 useWeb / use_web 明确为 true 才进入 Web 搜索增强；因此“推理可离线”与“开启搜索后联网”是不同运行状态。

## 价值

适合希望在一个界面比较本地图像、语音与聊天流程的用户，也便于把运行时、模型和输出按目录管理。便携性可减少全局环境改动，但仍要为特定系统和硬件准备依赖。

## 风险边界

- “100% offline / zero setup”是宣传表述。首次运行与模型管理会访问外部下载源，可选搜索会发送查询；本轮没有用断网或网络抓包验证整条链路。
- UI 无登录，源码默认绑定 127.0.0.1；设置 UAIS_HOST=0.0.0.0 会扩大访问面。不要把无认证服务直接放到共享网络。
- Linux 预构建要求 glibc >=2.38、GLIBCXX_3.4.32+；驱动、libgomp、Vulkan loader 等仍可能缺失。Intel NPU 另需设备、驱动与内核条件。
- app 本体 MIT，模型、语音资产与捆绑后端各有来源和条款。下载地址 / 版本、二进制完整性和权重身份应另留清单。
- 本轮未运行启动器、安装后端、采音、生成媒体或比较性能；“自动加速”不构成跨平台实测结论。

## 补充建议

1. 先固定一个小模型和单一路线，记录安装流量、模型 hash、启动日志和输出身份。
2. 下载完成后断网复测聊天 / 转写 / TTS / 图像各功能，单独检查可选搜索状态。
3. 用相同 prompt / seed / 采样器 / 模型比较后端；转写记录语言和 CER / WER，TTS 检查音色许可。

上游 [安装演示视频](https://www.youtube.com/watch?v=yeFvP3SWMak) 已核作者与标题，仅作为操作观察入口。

## 参考资料

- [README.md](https://github.com/techjarves/Portable-Local-Studio/blob/3f0830f527d4a3c3bf8664ecbbb293043dd496f2/README.md)。
- [mac.sh](https://github.com/techjarves/Portable-Local-Studio/blob/3f0830f527d4a3c3bf8664ecbbb293043dd496f2/mac.sh)。
- [scripts/setup/setup.sh](https://github.com/techjarves/Portable-Local-Studio/blob/3f0830f527d4a3c3bf8664ecbbb293043dd496f2/scripts/setup/setup.sh)。
- [scripts/server/serve.cjs](https://github.com/techjarves/Portable-Local-Studio/blob/3f0830f527d4a3c3bf8664ecbbb293043dd496f2/scripts/server/serve.cjs)。
- [scripts/config/llm-backends.json](https://github.com/techjarves/Portable-Local-Studio/blob/3f0830f527d4a3c3bf8664ecbbb293043dd496f2/scripts/config/llm-backends.json)。
- [LICENSE](https://github.com/techjarves/Portable-Local-Studio/blob/3f0830f527d4a3c3bf8664ecbbb293043dd496f2/LICENSE)。
- [仓库 API](https://api.github.com/repos/techjarves/Portable-Local-Studio)；本轮发行列表为空。
