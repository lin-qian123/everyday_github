<!-- markdownlint-disable MD013 -->

# Remotion：以 React 源码组织 Agent 视频生产

- 主上游：[remotion-dev/remotion](https://github.com/remotion-dev/remotion)；repository ID `274495425`。
- 采样日期：2026-10-28（Asia/Shanghai）；分类：语音、视频与多模态。
- API 累计快照：68,255 stars / 5,544 forks / 202 open issues（含 PR 口径），与榜单日增分开。
- 默认分支 `main`；主线依据固定在 `4bf07553bd5493307ad1ae21988a23e593730bcd`。发行 API 首项 [v4.0.539](https://github.com/remotion-dev/remotion/releases/tag/v4.0.539)，UTC 2026-10-26T12:04:13Z，正式发行标记。
- 核验层级：一手文档、元数据和所列部分实现的静态阅读；未安装运行、调用模型、复现基准或验证真实用户效果。

## 定位

Remotion 以 React 代码作为视频与图像的源文件，将程序化动画、交互编辑和 Coding Agent 工作流连接起来。它提供制作与渲染工具，生成内容是否正确、好看以及素材是否合法仍需人工验收；它本身不是通用文生视频模型。

## 用法

在有 Node.js 的专用目录，按 README 创建项目；官方 Agent Skills 是独立的 `remotion-dev/skills` 上游：

```bash
npx create-video@latest
npx skills add remotion-dev/skills
```

上面是上游滚动入口，本轮未执行。实际制作前固定模板、依赖版本与 lockfile；先做一个短片，检查 Studio 预览、字体、音频、字幕、目标分辨率，再按项目选择本机或服务端渲染。API 发行首项为 4.0.539，不把 main 的能力直接当作该发行已经具备。

## 原理

组件、时间与数据共同决定画面；React 源码可复用为动画设计资产与参数化模板。Agent 写代码，Studio 提供预览 / 编辑入口，渲染流程输出媒体。官方 Skills 分别覆盖创建、markup、Studio、render 等环节；安装技能不会自动把任意组件变为可交互编辑，也不替代逐帧检查。

## 价值

适合参数化课程片头、数据驱动图表动画、产品短片与重复批量视频。源码、素材清单和版本锁定有助于重做与审阅；批量渲染能力不代表单机速度、跨环境像素一致或 AI 生成质量已验证。

## 风险边界

- **特殊许可**：当前固定 LICENSE 允许个人、最多 3 名员工的营利组织、非营利组织及非商业评估者在相应条件下免费使用；不符合资格者需 Company License。另限制销售 / 出租 / 再许可自有 Remotion 派生软件，不能当作 MIT 或任意再分发授权。此处为原文摘要，边界情形应核当前条款。
- LICENSE 还提示未来 5.0 将变更；当前页面不把未来规则写成 4.x 已生效事实，也不沿用不明日期的价格。
- 字体、音乐、照片、模板、第三方依赖与模型输出的权利独立于框架许可；能渲染不证明素材获准使用。
- 模板和 Agent 生成的代码会在开发 / 渲染环境执行，远程素材、模型服务和云渲染有各自的数据与费用边界。应限制凭据、固定输入，并设置批次资源上限。

## 补充建议

先制作 10–20 秒、两种画幅的样片，保留源代码与合法素材，只保存有效成品和 QA。逐项检查文字准确性、字幕时序、音画同步、色彩和目标设备播放；通过后再批量生成。

## 参考资料

- [README.md](https://github.com/remotion-dev/remotion/blob/4bf07553bd5493307ad1ae21988a23e593730bcd/README.md)。
- [LICENSE.md](https://github.com/remotion-dev/remotion/blob/4bf07553bd5493307ad1ae21988a23e593730bcd/LICENSE.md)。
- [package.json](https://github.com/remotion-dev/remotion/blob/4bf07553bd5493307ad1ae21988a23e593730bcd/package.json)。
- [官方 Agent Skills 用法](https://www.remotion.dev/docs/ai/skills)；技能源码与框架为不同上游。
- [仓库 API](https://api.github.com/repos/remotion-dev/remotion)、[发行 API](https://api.github.com/repos/remotion-dev/remotion/releases?per_page=1)；动态字段只代表本轮采样。
- 事实依据为以上一手材料；价值、风险推论与补充建议为本库工程分析。
