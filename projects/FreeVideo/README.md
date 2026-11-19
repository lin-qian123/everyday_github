<!-- markdownlint-disable MD013 -->

# FreeVideo

## 定位

面向消费级硬件的 MiniMax H3 本地视频生成引擎，以 ComfyUI 自定义节点、创作面板和跨平台启动器提供文本、图像及音视频参考生成。适合观察低显存推理、工作流复用与本地视频制作；“能装入内存”与生成速度、画质及可发布性需要分别评价。

- 上游：[FlashML-org/FreeVideo](https://github.com/FlashML-org/FreeVideo)，仓库 ID `1368913638`。
- 2026-11-20 07 时段：官方 Python daily **+99**；API stars / forks / open issues（含 PR）为 **3,421 / 453 / 731**。[API](https://api.github.com/repos/FlashML-org/FreeVideo)
- 最新核到的非预发行版：[v0.6.5](https://github.com/FlashML-org/FreeVideo/releases/tag/v0.6.5)，UTC 11-19 20:54，即北京时间 11-20 04:54。本页依据 main `225997487d52a873882183245c594e3b0249a3d6` 静态抽读，未验收发行二进制。
- 分类：`语音、视频与多模态`。今天首次建档，README 记载项目于 10-02 开源，不是今日首发。

## 用法

已有 ComfyUI 时，可将节点放入其 `custom_nodes`，再重启并打开 FreeVideo-All-in-One 模板。以下是固定源码示例，本轮没有执行安装或生成：

```bash
cd ComfyUI/custom_nodes
git clone https://github.com/FlashML-org/FreeVideo.git
git -C FreeVideo checkout 225997487d52a873882183245c594e3b0249a3d6
```

在 FreeVideo 设置中完成运行环境与模型配置；启动器也能复用已有模型。源码包声明 Python `>=3.12,<3.13`，不要直接沿用任意现有 Python 环境。Mac 文档要求 Apple 芯片、macOS 14+ 与 Xcode 命令行工具，并将 Mac 版本标为实验性。[使用说明](https://github.com/FlashML-org/FreeVideo/blob/225997487d52a873882183245c594e3b0249a3d6/README.zh-CN.md)、[包配置](https://github.com/FlashML-org/FreeVideo/blob/225997487d52a873882183245c594e3b0249a3d6/pyproject.toml)、[Mac 说明](https://github.com/FlashML-org/FreeVideo/blob/225997487d52a873882183245c594e3b0249a3d6/docs/Mac.zh-CN.md)

## 原理

1. **模型与步数**：README 将其描述为基于 VDN-H3 的 8 步模型与 Video DeltaNet 混合注意力，并非把完整原始模型不加改动地搬到小显卡。
2. **分层调度**：统一管理显存、系统内存和磁盘，用权重流式加载、异步预取、分块计算及不同精度降低峰值占用；最低 8GB 显存 / 16GB RAM 是上游适配声明，不是所有尺寸、时长和档位的保证。
3. **硬件路径**：Mac 在阶段开始前按可用统一内存规划分块和常驻层；M5 及更新芯片使用 int8 大矩阵路径，较早芯片把同类权重解码成 BF16 计算。硬件代际和可用内存都会改变耗时。
4. **工作流与输出**：ComfyUI 管理生成参数、参考素材、LoRA 与后续编辑。v0.6.5 新增的 48 / 60 fps 导出通过 GPU 补帧实现，不能据导出帧率宣称模型原生生成速率或实时生成。

以上来自固定 [README](https://github.com/FlashML-org/FreeVideo/blob/225997487d52a873882183245c594e3b0249a3d6/README.zh-CN.md)、[Mac 文档](https://github.com/FlashML-org/FreeVideo/blob/225997487d52a873882183245c594e3b0249a3d6/docs/Mac.zh-CN.md)与 [v0.6.5 发行说明](https://github.com/FlashML-org/FreeVideo/releases/tag/v0.6.5)，没有独立性能复现。

## 价值

- 将显存放不下的问题转为分层执行与时间开销，给已有消费级设备增加视频生成入口。
- 同一工作流可留存提示词、种子和参数，便于对照档位、LoRA 与设备结果。
- 本地生成便于自管素材和输出；实际收益应按成功率、端到端耗时、峰值内存、磁盘占用与人工筛片时间衡量。

## 风险边界

- **代码与模型许可不同。** 代码为 Apache-2.0；模型使用 MiniMax H3 社区许可。本轮仓库附带文本与 README 指向的 Hugging Face LICENSE 去首尾空白后一致；该文本排除欧盟、英国、韩国、美国等使用地区，并包含用途、公开内容 AI 标识等要求。不能从代码许可推导模型及输出可任意使用。[代码许可](https://github.com/FlashML-org/FreeVideo/blob/225997487d52a873882183245c594e3b0249a3d6/LICENSE)、[附带模型许可](https://github.com/FlashML-org/FreeVideo/blob/225997487d52a873882183245c594e3b0249a3d6/freevideo_engine/licenses/MiniMax-H3-Community-License-Agreement.txt)、[模型来源文本](https://huggingface.co/OpenVDN/vdn-minimax-h3-edge/blob/main/LICENSE)
- **低内存不等于快速。** Mac 文档的作者测试为 M5、24GB 统一内存、约 14GB 可用、轻量档：1344×768 的 10 秒视频约需 42 分钟；更早 Mac 使用不同计算路径。这个历史单配置例子不能外推到所有 Mac 或本次发行。
- **首次安装会联网并写入环境。** 启动器下载缺失的依赖和模型；离线包需要提前完整准备。Mac 文档仍称预览版未公证并要求核 SHA-256；本轮未下载、验签或打开应用。
- **清除草稿有适用范围。** `comfy_privacy.py` 仅对 FreeVideo 管理的 ComfyUI 设置默认关闭浏览器工作流草稿，保留用户已有选择；读取 / 写入失败会保留原设置。它不证明已有 ComfyUI、输出目录或第三方节点没有留存和网络出口。[源码](https://github.com/FlashML-org/FreeVideo/blob/225997487d52a873882183245c594e3b0249a3d6/freevideo_engine/comfy_privacy.py)

## 补充建议

先选一个短片和固定种子，保存模型 / 节点版本、原生帧数、导出帧率、分辨率、档位、完整耗时与峰值内存，再比较加速路径。检查人物、动作连续性、声音同步与补帧伪影；API 成功或文件可解码不能代替完整观看与艺术验收。敏感素材使用前另核所选 Agent、ComfyUI 节点和模型下载链路。

## 参考资料

- [组件许可展示实现](https://github.com/FlashML-org/FreeVideo/blob/225997487d52a873882183245c594e3b0249a3d6/freevideo_engine/component_licenses.py)
- [安全反馈渠道](https://github.com/FlashML-org/FreeVideo/blob/225997487d52a873882183245c594e3b0249a3d6/SECURITY.md)
- [发行列表](https://github.com/FlashML-org/FreeVideo/releases)；本文固定 SHA 资料与未运行边界见相关段落。
