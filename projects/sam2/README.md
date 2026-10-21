<!-- markdownlint-disable MD013 -->

# SAM 2

> 更新：2026-10-22（Asia/Shanghai）。分类：语音、视频与多模态。主上游 `facebookresearch/sam2`；默认分支快照 `2b90b9f5ceec`。官方资料与源码静态研究；热度、发行及社媒口径见[当日日报](../../daily/2026-10-22/ai-hotspots.md)。

## 定位

Meta FAIR 的可提示图像 / 视频分割模型：用点击、框等提示产生目标掩膜，并在视频中传播。Transformer 配流式记忆，把图像视为单帧视频；不自动给所有目标命名，也不保证身份跟踪或科学边界真值。[README.md](https://github.com/facebookresearch/sam2/blob/2b90b9f5ceec907a1c18123530e92e794ad901a4/README.md)

## 用法

源码 editable 安装入口 `pip install -e .`；当前要求 Python `>=3.10`、torch `>=2.5.1`、torchvision `>=0.20.1`。下载匹配的 SAM 2.1 checkpoint 与 config 后，用 `SAM2ImagePredictor` 或 `build_sam2_video_predictor` 运行；图像、视频与自动掩膜示例需分别看。[README.md](https://github.com/facebookresearch/sam2/blob/2b90b9f5ceec907a1c18123530e92e794ad901a4/README.md) [pyproject.toml](https://github.com/facebookresearch/sam2/blob/2b90b9f5ceec907a1c18123530e92e794ad901a4/pyproject.toml)

视频流程为初始化 state、加入点 / 框提示、调用 `propagate_in_video`。`vos_optimized=True` 开启整模型编译路径，首次编译耗时与稳态 FPS 要分开记录。[README.md](https://github.com/facebookresearch/sam2/blob/2b90b9f5ceec907a1c18123530e92e794ad901a4/README.md) [RELEASE_NOTES.md](https://github.com/facebookresearch/sam2/blob/2b90b9f5ceec907a1c18123530e92e794ad901a4/RELEASE_NOTES.md)

## 原理

图像编码器得到特征，提示与记忆帮助解码当前对象掩膜，再在帧间更新。当前视频 predictor 独立处理各对象、共享 backbone 特征，允许追踪开始后添加对象；legacy predictor 保留旧行为。[README.md](https://github.com/facebookresearch/sam2/blob/2b90b9f5ceec907a1c18123530e92e794ad901a4/README.md) [RELEASE_NOTES.md](https://github.com/facebookresearch/sam2/blob/2b90b9f5ceec907a1c18123530e92e794ad901a4/RELEASE_NOTES.md)

## 价值

工程判断：适合有交互纠正的标注、视频抠像和候选区域生成，能把一次提示复用到更多帧。实际收益需计入纠正次数和人工时间，不能只看模型 FPS 或演示片段。

## 风险边界

- README 中 SAM 2.1 为 2024-09 发布，整模型编译更新为 2024-12；今日上榜不代表今天发布新模型。GitHub Release 列表为空，也不代表没有 checkpoint / release notes。[README.md](https://github.com/facebookresearch/sam2/blob/2b90b9f5ceec907a1c18123530e92e794ad901a4/README.md) [RELEASE_NOTES.md](https://github.com/facebookresearch/sam2/blob/2b90b9f5ceec907a1c18123530e92e794ad901a4/RELEASE_NOTES.md)
- 上游提醒编译可能引入小数值差异；CUDA 扩展构建失败可继续部分功能，但后处理可能受限，需核实际安装日志。[RELEASE_NOTES.md](https://github.com/facebookresearch/sam2/blob/2b90b9f5ceec907a1c18123530e92e794ad901a4/RELEASE_NOTES.md) [README.md](https://github.com/facebookresearch/sam2/blob/2b90b9f5ceec907a1c18123530e92e794ad901a4/README.md)
- macOS demo 的 Docker 路径只用 CPU，MPS 要本机运行且可能受内存限制；不能将 CUDA 测得的 FPS 外推到 Mac。[demo/README.md](https://github.com/facebookresearch/sam2/blob/2b90b9f5ceec907a1c18123530e92e794ad901a4/demo/README.md)
- README 声明模型 checkpoint / demo / training code Apache-2.0，字体等单独许可；`sav_dataset/LICENSE` 明确针对评估软件，不是原视频数据的通用授权。访问在线 demo 涉及素材上传，需另核服务条款。[README.md](https://github.com/facebookresearch/sam2/blob/2b90b9f5ceec907a1c18123530e92e794ad901a4/README.md) [LICENSE](https://github.com/facebookresearch/sam2/blob/2b90b9f5ceec907a1c18123530e92e794ad901a4/LICENSE) [sav_dataset/LICENSE](https://github.com/facebookresearch/sam2/blob/2b90b9f5ceec907a1c18123530e92e794ad901a4/sav_dataset/LICENSE)

## 补充建议

选获授权的短视频，覆盖遮挡、快速运动、细结构和新对象；冻结提示策略，报告 IoU / J&F、纠正次数、显存和端到端时间。需比较现代 SAM 版本时另设同条件实验，不能仅按模型编号定优劣。本轮未下载权重、运行分割或上传素材。

## 参考资料

- [README.md](https://github.com/facebookresearch/sam2/blob/2b90b9f5ceec907a1c18123530e92e794ad901a4/README.md)
- [LICENSE](https://github.com/facebookresearch/sam2/blob/2b90b9f5ceec907a1c18123530e92e794ad901a4/LICENSE)
- [pyproject.toml](https://github.com/facebookresearch/sam2/blob/2b90b9f5ceec907a1c18123530e92e794ad901a4/pyproject.toml)
- [RELEASE_NOTES.md](https://github.com/facebookresearch/sam2/blob/2b90b9f5ceec907a1c18123530e92e794ad901a4/RELEASE_NOTES.md)
- [demo/README.md](https://github.com/facebookresearch/sam2/blob/2b90b9f5ceec907a1c18123530e92e794ad901a4/demo/README.md)
- [sav_dataset/LICENSE](https://github.com/facebookresearch/sam2/blob/2b90b9f5ceec907a1c18123530e92e794ad901a4/sav_dataset/LICENSE)
- [仓库 API](https://api.github.com/repos/facebookresearch/sam2)
