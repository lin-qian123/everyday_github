# blinkface

## 定位

`blinkface` 是以双手框选为交互的实时人像风格化实验：CUDA GPU 主机运行 FLUX.2 klein 4B 图像 API，浏览器或 Mac 端作为远程取景器，支持文生图、图生图和预览切换。截至 2026-07-25，仓库创建于 2026-07-24，约 21 stars、2 forks。

## 用法

在 GPU 机器上创建虚拟环境、按 CUDA 版本安装 PyTorch 与 `requirements-server.txt`，配置 `.env` 后启动 `python server.py`。客户端配置 `BLINKFACE_HOST` 和可选 token，运行 `python web-serve.py` 后从浏览器打开本地页面；远程相机访问必须置于 HTTPS 反向代理后。

## 原理

FastAPI/diffusers 在 GPU 端提供 FLUX 生成接口；MediaPipe Hand Landmarker 检测双手取景框，前端把框选区域和 prompt 发至同源代理。代理代持 token，浏览器不直接保存密钥；仓库用 Tailscale、LAN 或 SSH 隧道连接跨设备客户端。

## 价值

- 把图像生成从一次性 prompt 变成带手势反馈的低延迟交互样本。
- 服务端与浏览器解耦，便于复用已有 GPU，同时让轻客户端参与创作。
- README 明确给出了端口、token、模型许可证和使用同意边界，适合作为安全配置案例阅读。

## 风险边界

- 仅应处理本人或已明确同意的人像；不得用于未经授权的换脸、冒充或违法用途。
- GPU 服务若绑定公网或在不受信网络中无 token 暴露，会成为匿名生成入口。
- 不同 FLUX 权重的许可证不同；提示词中的风格名不构成与权利人的关联或授权。

## 补充建议

优先保持默认 localhost 绑定，跨设备使用 Tailscale/认证反代，不要将 8000 端口直接暴露公网。正式采集前应取得可记录的同意，并为上传图片设置删除期限和访问控制。

## 参考资料

- GitHub：<https://github.com/xcc3641/blinkface>
- FLUX.2 klein 4B 模型卡：<https://huggingface.co/black-forest-labs/FLUX.2-klein-4B>
- MediaPipe Hand Landmarker：<https://ai.google.dev/edge/mediapipe/solutions/vision/hand_landmarker>
