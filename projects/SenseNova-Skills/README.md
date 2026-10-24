<!-- markdownlint-disable MD013 -->

# SenseNova-Skills：面向办公与研究的技能工作流

- 主上游：[OpenSenseNova/SenseNova-Skills](https://github.com/OpenSenseNova/SenseNova-Skills)；repository ID `1210155353`。
- 采样日期：2026-10-25（Asia/Shanghai）；分类：办公、商业与行业应用。
- API 累计快照：5,898 stars / 422 forks / 22 open issues（含 PR 口径）；与榜单日增分开。
- 默认分支 `main`，本页静态依据固定在 `7838651111ef2dc3ac0293f08008730f1a022694`。公开 Release 列表为空，不据此推断没有 tag 或包发行。
- 核验层级：直接读取上游文档、许可、元数据和下列部分实现；未安装运行、调用模型或复现性能。

## 定位

SenseNova-Skills 是面向 OpenClaw、hermes-agent 等宿主的技能与辅助资源集合，覆盖图像、PPT、Excel、研究、网页和任务跟踪。每个技能独立用 SKILL.md 声明入口与执行方式；不是独立模型，也不能把小浣熊产品的用户规模或安全宣传当作这套仓库的实测效果。

## 用法

上游提供 Agent Pack 和手动复制两种路线。希望审阅依赖与权限时，可先只克隆，再选择单个需要的技能：

```bash
git clone --depth=1 https://github.com/OpenSenseNova/SenseNova-Skills.git
```

手动接入目录按宿主分别为 ~/.openclaw/skills/ 或 ~/.hermes/skills/，必要时重启宿主。按 INSTALL_CN.md 配置相同地区的 Base URL、key 与模型，按具体技能安装依赖，不要将“全量复制后可见”视为全部能力已可用。上游免费套餐描述不作为本轮额度或长期价格承诺；本轮未安装或请求 API。

## 原理

技能作为编排层，按任务选择底层模型、搜索、脚本和导出工具；例如图像基础层供信息图等上层技能复用。PPT 标准模式由 Entry / Story 准备任务与大纲，再组织逐页 HTML、渲染、评审和专用 exporter；创意模式则以每页全图生成。不同模式的输出结构不同，不能由扩展名 PPTX 断言逐对象可编辑。

## 价值

适合把办公任务分成可检查的大纲、证据、资产和最终产物，方便复用已有流程。研究与表格技能可提供步骤和中间数据，但真实文献、数值、公式、表格单位及最终渲染仍需逐项核对，不能由自动评审分数替代人工验收。

## 风险边界

宿主会执行脚本、读取文件并调用模型与搜索服务，技能说明本身不收窄宿主权限。sn-image-doctor 明确会交互补齐变量并写入 .env，不是纯只读诊断；不同 doctor 行为不能混为一谈。模型调用可能产生数据外发与费用，外部网站和论文仍可能受访问或版权限制。根许可证为 MIT，依赖、模型、图片与产品服务独立适用条款。

## 补充建议

优先安装一条小工作流，用合成 Excel 或公开材料做完整输出验证，再扩大技能集。PPT 需要分别验收文字 / 图表 / 公式可编辑性、字体、溢出、导出重开与来源；研究报告对每个关键判断回查原始文献。密钥写入前确认目标、权限和忽略规则，关闭不需要的长期任务。

## 参考资料

- [README_CN.md](https://github.com/OpenSenseNova/SenseNova-Skills/blob/7838651111ef2dc3ac0293f08008730f1a022694/README_CN.md)。
- [INSTALL_CN.md](https://github.com/OpenSenseNova/SenseNova-Skills/blob/7838651111ef2dc3ac0293f08008730f1a022694/INSTALL_CN.md)。
- [skills/sn-ppt-standard/SKILL.md](https://github.com/OpenSenseNova/SenseNova-Skills/blob/7838651111ef2dc3ac0293f08008730f1a022694/skills/sn-ppt-standard/SKILL.md)。
- [skills/sn-image-doctor/SKILL.md](https://github.com/OpenSenseNova/SenseNova-Skills/blob/7838651111ef2dc3ac0293f08008730f1a022694/skills/sn-image-doctor/SKILL.md)。
- [LICENSE](https://github.com/OpenSenseNova/SenseNova-Skills/blob/7838651111ef2dc3ac0293f08008730f1a022694/LICENSE)。
- [仓库 API](https://api.github.com/repos/OpenSenseNova/SenseNova-Skills)、[发行 API](https://api.github.com/repos/OpenSenseNova/SenseNova-Skills/releases?per_page=3)；动态元数据只代表本轮采样。
- 事实来源为以上固定文件；价值、风险评估和验证建议为本库工程判断，未作为上游实测结果。
