<!-- markdownlint-disable MD013 -->

# moli

- 仓库：[lexmount/moli](https://github.com/lexmount/moli)
- 快照：2026-08-11 抓取；GitHub API 显示其创建于 2026-08-10，约 15 stars、5 forks，未声明 SPDX 许可证。数字会随时间变化。
- 分类：前端、UI 与 Agent 交互层

## 定位

一个以 Rust 实现、面向 agent 自动化的 headless 浏览器。它主张默认给出 DOM、结构化文本和脚本执行能力，只有请求几何或像素时才临时执行 layout/渲染，以压低抓取和 browser-use 工作负载的常驻成本。

## 用法

项目提供 CLI、MCP、CDP、WebDriver Classic/BiDi 等接入面。使用前需按其构建文档获取二进制或自行编译；自动化可从导航、Markdown/DOM 提取、交互元素发现和脚本执行开始，确有空间定位或截图需求时再启用 `--layout`。把它放进生产 agent 前应先测试目标站点兼容性。

## 原理

README 描述其使用 V8、原生 DOM/CSS 状态和按需软件渲染：非视觉任务直接读取运行时，几何与屏幕帧由当前 DOM/style 临时重建，而非保持 GUI 浏览器的持续 compositor。这样是在资源模型上优化，不意味着实现了 Chrome 级完整兼容性或安全隔离。

## 价值

对高并发页面提取、RAG 采集、agent 评测和 DOM 优先的网页操作，按需渲染可能减少空闲内存和不必要的视觉循环；多协议接口也降低了替换既有自动化驱动的摩擦。

## 风险边界

新浏览器内核可能与复杂网站、登录、反自动化、无障碍树、CSS/媒体能力存在行为差异。加载第三方网页仍会处理脚本、cookie、存储和网络流量；不应把“headless”或“按需渲染”误认为隐私保护或执行沙箱。API 元数据未声明 SPDX 许可证，商用/分发前须核对仓库许可文件。

## 补充建议

用代表性页面建立兼容性、性能和安全回归集，特别覆盖登录、上传、下载、跨域、cookie 与网络代理。默认限制网络出口、profile 生命周期和凭据注入；遇到付款、账号设置或发布动作，保持人工确认。

## 参考资料

- [项目 README 与源码](https://github.com/lexmount/moli)
- [GitHub API 元数据快照](https://api.github.com/repos/lexmount/moli)
