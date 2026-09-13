<!-- markdownlint-disable MD013 -->

# AI Coding Dictionary（mattpocock/dictionary-of-ai-coding）中文解读

> 证据快照：2026-09-14（Asia/Shanghai）。GitHub REST API 显示 4,567 stars、527 forks、20 open issues；未识别 SPDX 许可证，根目录也没有独立 `LICENSE`，没有 GitHub Release。仓库 `package.json` 标为 `private` 且没有发行版本，README 由 `dictionary/*.md`、curriculum 与模板生成。本文未逐条事实核查全部词条，也未将站点内容用于培训或再分发。

## 定位

AI Coding Dictionary 是面向 AI coding 实践者的英文术语表，把 model、token、context、harness、tool call、sandbox、hallucination、handoff、skill、subagent、human-in-the-loop 等词汇放进同一套工作语境，并为每个概念提供通俗解释、反例和用法。

它更像作者维护的教学型概念地图，而不是标准组织发布的规范或经同行评审的教科书。价值主要在统一讨论语言，不能把单一词条直接当成产品合同、计费定义或安全保证。

## 用法

- 直接浏览生成后的 GitHub README，按七个主题章节顺序阅读。
- 在项目评审中链接到具体锚点，用精确术语替代模糊的“AI”“记忆”“沙箱”等词。
- 贡献者可修改 `dictionary/*.md` 源文件，并重新生成总 README：

```bash
git clone https://github.com/mattpocock/dictionary-of-ai-coding.git
cd dictionary-of-ai-coding
npm install
npm run generate
```

仓库没有作为 npm 库发布；`package.json` 主要服务于内容生成和格式化。

## 原理

- 用独立 Markdown 词条作为内容源，由生成脚本合并为带目录和交叉链接的长 README。
- 章节从模型、上下文与工具环境，推进到失败模式、handoff、memory/steering 和工作模式。
- 词条通过互相链接建立概念图，例如把 agent 拆回 model、harness、tools、context 与循环，而不是把能力归于一个黑箱标签。
- 每项常配 `Avoid` 与 `Usage`，用反例和对话示例说明术语怎样影响需求、调试和协作。

## 价值

- 让产品、工程和管理者对 context window、cache、permission、sandbox、compaction 等词使用更一致。
- 把常见失败拆成可定位的机制，有助于写更清楚的 issue、handoff 与测试假设。
- 生成式内容结构方便 review 单个词条，同时保持总入口可搜索。
- 适合作为 onboarding 索引，再链接到 provider 文档、论文与本地实现证据。

## 风险边界

- 术语定义含作者取舍，且模型、provider、产品 UI 与计费规则变化很快；同一个词在不同工具中可能有不同合同含义。
- 通俗化会压缩例外条件；例如 sandbox、stateful、cache、human review 都必须回到具体实现和权限边界。
- 词条并非逐项附带一手来源或版本日期，历史归因、定量主张与产品行为需要另查原始资料。
- 根目录无独立 LICENSE、API 未识别 SPDX；在复制、翻译、出版或训练数据再利用前，不能凭公开仓库推断授权。
- newsletter 与个人课程入口属于作者生态，关注度不能替代内容正确性或中立性。

## 补充建议

1. 团队引用时记录 commit，并在关键术语旁补充实际 provider/API/源码定义。
2. 为容易漂移的条目增加 `last_verified`、来源和产品差异表，不把生成时间等同于事实更新时间。
3. 用真实故障复盘检查术语是否帮助定位，而不是只增加 jargon。
4. 计划翻译或再分发前先取得明确许可；内部摘要也应保留作者与原始链接。

## 参考资料

- GitHub：<https://github.com/mattpocock/dictionary-of-ai-coding>
- GitHub REST API：<https://api.github.com/repos/mattpocock/dictionary-of-ai-coding>
- 在线词典：<https://aicodingdictionary.com>
- 生成说明与 README 源：<https://github.com/mattpocock/dictionary-of-ai-coding/blob/main/README.md>
- `package.json`：<https://github.com/mattpocock/dictionary-of-ai-coding/blob/main/package.json>
- 作者 X：<https://x.com/mattpocockuk>
- 作者 YouTube：<https://www.youtube.com/@mattpocockuk>
