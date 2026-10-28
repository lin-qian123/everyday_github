<!-- markdownlint-disable MD013 -->

# Upscayl

## 定位

Upscayl 是面向 Linux、macOS、Windows 的 AI 图像放大桌面工具。它以本地原生推理后端处理低分辨率图片，并提供模型选择、批量处理和输出选项。图像增强是在推断可能的细节，应与忠实记录原始信息的任务区分。

2026-10-29 快照：TypeScript daily +59 stars；API 51,229 stars / 2,660 forks / 48 open issues（含 PR），应用许可 AGPL-3.0。主线 `a00d55fee90e` 的 package 为 2.15.0，发行首项 v2.15.0 发布于 **2024-12-25 UTC**，并非今日发布。本轮做静态阅读，未安装、放大图片或抓包。

## 用法

1. 从官方发行选择与系统匹配的包；README 要求 Vulkan 兼容 GPU，macOS 为 12 及以上，部分集显不能正常推理。
2. 用授权样图选择模型、倍率和独立输出目录；先关闭覆盖原图，保留原始文件。
3. 比较文字、面部、线稿、纹理和边缘，检查输出尺寸与处理失败提示，再决定是否批量。

macOS README 也给出 Homebrew 入口：

```bash
brew install --cask upscayl
```

自动更新、模型与发行二进制都应记录来源和版本。需要 CLI 时，上游另指向 upscayl-ncnn，桌面包不应直接等同于可脚本化的同名命令。

## 原理

Electron / React 界面选择参数，通过本机 child process 启动资源目录中的原生二进制。上游说明后端使用 Real-ESRGAN / NCNN 与 Vulkan，模型估计高分辨率纹理而非找回已丢失的真实像素。模型类型、图像内容、倍率与切块条件会共同影响结果。

## 价值

- 为非命令行用户提供可视化的本地图像放大与对比流程。
- 批量处理和模型切换便于建立针对照片、动漫和线稿的固定工作方式。
- 对普通展示素材有实际用途；科研图、票据和证据图则应保留原图并说明处理。

## 风险边界

- 模型可能生成错误纹理、改变小字和身份特征；README 也说明它不适合失焦或完全模糊图片，不能把清晰观感当作事实恢复。
- **本地推理不等于无统计出口**：当前 `_app.tsx` 挂载 PostHog wrapper，`enableContribution` 默认 true；wrapper 的 effect 调用 init，并在 loaded 回调捕获带系统信息 / 版本的 `app_launched`。
- 在该 wrapper 中，贡献开关 false 仅改变返回的 Provider 树，effect 本身未按此开关跳过。因而仅凭 UI 开关不能证明启动事件已被阻止；这是固定主线的静态观察，未核发行包是否同构，也未验证实际网络发送。
- 主线关闭 pageview / autocapture / session recording，并不等于完全不初始化统计。云端产品和桌面处理的数据路径也应分别审查。
- 应用 AGPL、Real-ESRGAN 的 BSD 文本、各模型与图片权利分层核对；GPU 兼容和性能不能由跨平台标签保证。

## 补充建议

先用公开样图建立质量对照，保存原图与参数，记录伪影和文字变化。敏感用途先核二进制来源，再以受控环境检查贡献开关、启动网络和更新行为；不要只凭 package 版本或本地推理判断隐私。

## 参考资料

- [上游仓库](https://github.com/upscayl/upscayl)、[GitHub API](https://api.github.com/repos/upscayl/upscayl)。
- [固定 README：兼容与原理](https://github.com/upscayl/upscayl/blob/a00d55fee90e0f9435d5eaa86e76700df8199af8/README.md)、[版本与打包配置](https://github.com/upscayl/upscayl/blob/a00d55fee90e0f9435d5eaa86e76700df8199af8/package.json)、[v2.15.0](https://github.com/upscayl/upscayl/releases/tag/v2.15.0)。
- [原生进程调用](https://github.com/upscayl/upscayl/blob/a00d55fee90e0f9435d5eaa86e76700df8199af8/electron/utils/spawn-upscayl.ts)、[应用挂载入口](https://github.com/upscayl/upscayl/blob/a00d55fee90e0f9435d5eaa86e76700df8199af8/renderer/pages/_app.tsx)。
- [PostHog 初始化](https://github.com/upscayl/upscayl/blob/a00d55fee90e0f9435d5eaa86e76700df8199af8/renderer/components/posthog-provider-wrapper.tsx)、[贡献与更新开关默认值](https://github.com/upscayl/upscayl/blob/a00d55fee90e0f9435d5eaa86e76700df8199af8/renderer/atoms/user-settings-atom.ts)。
- [应用许可](https://github.com/upscayl/upscayl/blob/a00d55fee90e0f9435d5eaa86e76700df8199af8/LICENSE)、[Real-ESRGAN 许可](https://github.com/upscayl/upscayl/blob/a00d55fee90e0f9435d5eaa86e76700df8199af8/Real-ESRGAN_LICENSE.txt)。
