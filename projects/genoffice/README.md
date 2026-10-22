<!-- markdownlint-disable MD013 -->

# genoffice

- 主上游：[genspark-ai/genoffice](https://github.com/genspark-ai/genoffice)
- 分类：办公、商业与行业应用。
- 核验日期：2026-10-23（Asia/Shanghai）；主线快照 `e416f9ba8312`。
- [API](https://api.github.com/repos/genspark-ai/genoffice) 快照：10,529 stars / 1,395 forks / 85 open issues；发行列表首项 [v0.12.29](https://github.com/genspark-ai/genoffice/releases/tag/v0.12.29)（UTC 2026-10-22，正式）。累计值不代表今日增量。

## 定位

GenOffice 把 Word、Excel、PowerPoint、PDF、Markdown 和 HTML 编辑器与 AI 面板放在同一桌面套件中，也提供 CLI / MCP 给编码助手操作文件。适合需要交付可继续编辑的 Office 成品、并愿意验证格式兼容性的个人与团队。[README](https://github.com/genspark-ai/genoffice/blob/e416f9ba831273fe5874fc082854b9ecdbcc9379/README.md)

## 用法

从正式发行页选择对应系统的制品；先用文档副本验证打开、保存和重开，再配置 Genspark 登录或自己的模型端点。应用的 Settings → Integrations 可安装 Agent skill。安装后的最小检查示例：

```bash
genoffice --version
genoffice info report.docx --json
genoffice create --type docx --from notes.md --out notes.docx
genoffice render notes.docx --out preview/
```

这些命令来自上游说明，本轮未执行。普通文件编辑与转换使用本地引擎；AI 面板、搜索重排和媒体能力需分别检查端点与费用。README 的宏大覆盖描述不替代实际文档兼容性测试。

## 原理

Electron 应用共享 TypeScript 引擎，表格另有 Rust sidecar。以 docx 为例，保留原始压缩包，将编辑块锚定原 XML，只将脏块转换后拼回，其余条目按原字节复制。AI 通过结构化编辑操作与快照呈现修改；该机制解释了保真设计，但不能据此推断所有公式、排版与嵌入对象均正确往返。[架构说明](https://github.com/genspark-ai/genoffice/blob/e416f9ba831273fe5874fc082854b9ecdbcc9379/README.md)

## 价值

把“Agent 输出文本”推进到“生成、读取、修改、渲染真实文件”的可检查工作流。CLI 的 JSON 输出、文档结构检查和逐页预览适合纳入现有交付流程。是否能替代现有 Office 工具，取决于用户文件集上的修复成本与协作兼容性。

## 风险边界

- 官方打包制品默认启用 GA4 使用统计，首次启动可在 onboarding 提示前发送；Settings → General 可关闭后续上报。声明不收集文档正文、文件名与路径，但包含随机安装标识、版本、系统与语言等元数据；未注入打包元数据的源码构建采用 no-op tracker。[隐私披露](https://github.com/genspark-ai/genoffice/blob/e416f9ba831273fe5874fc082854b9ecdbcc9379/PRIVACY.md)
- Jev 重排默认关闭，开启后会向所选服务发送命中文档片段；Ask AI 也会把读取的段落交给所选模型。不能把本地索引概括为全部功能离线。
- renderer 沙箱、IPC 校验与受限布局解释器是上游设计说明，本轮未做渗透或恶意文件实验。[安全模型](https://github.com/genspark-ai/genoffice/blob/e416f9ba831273fe5874fc082854b9ecdbcc9379/SECURITY.md)
- 主体 Apache-2.0，但 `ee/` 使用单独企业许可；不能把根许可证套到整个目录树。[企业许可](https://github.com/genspark-ai/genoffice/blob/e416f9ba831273fe5874fc082854b9ecdbcc9379/ee/LICENSE)

## 补充建议

用含中文、Office Math、批注、修订、复杂表格与母版的脱敏文件集验收；记录重开后的对象可编辑性、公式结果和逐页差异。先关闭不需要的统计与云重排，分别测本地保存和云 AI 的实际出口。本轮仅核文档与许可，未安装、上传文件或调用模型。

## 参考资料

- [README.md](https://github.com/genspark-ai/genoffice/blob/e416f9ba831273fe5874fc082854b9ecdbcc9379/README.md)（固定 commit）。
- [PRIVACY.md](https://github.com/genspark-ai/genoffice/blob/e416f9ba831273fe5874fc082854b9ecdbcc9379/PRIVACY.md)（固定 commit）。
- [SECURITY.md](https://github.com/genspark-ai/genoffice/blob/e416f9ba831273fe5874fc082854b9ecdbcc9379/SECURITY.md)（固定 commit）。
- [ee/LICENSE](https://github.com/genspark-ai/genoffice/blob/e416f9ba831273fe5874fc082854b9ecdbcc9379/ee/LICENSE)（固定 commit）。
- [正式发行列表](https://github.com/genspark-ai/genoffice/releases)、[仓库 API](https://api.github.com/repos/genspark-ai/genoffice)（动态状态）。
