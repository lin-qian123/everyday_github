<!-- markdownlint-disable MD013 -->

# AI Job Search

> 上游仓库：[MadsLorentzen/ai-job-search](https://github.com/MadsLorentzen/ai-job-search) · 归类：办公、商业与行业应用 · 本页基于 2026-08-27 的上游 README、SETUP.md、SECURITY.md 与 GitHub API 快照整理。

## 定位

AI Job Search 是一个在本机运行的 AI 求职申请框架，围绕 Claude Code 组织 `/setup`、`/scrape`、`/rank`、`/apply`、`/interview` 和 `/outcome` 等命令：从个人资料与职位文本出发，评估匹配度、生成定制 CV/求职信、准备面试并追踪申请结果。核心工作流与国家无关，但仓库自带的部分职位门户技能面向丹麦市场。API 快照为 36,428 stars、12,407 forks、5 个开放 issue，MIT；Trending 页面抓取时显示约 +1,299 当日 stars。热度不能证明生成材料真实、申请成功率普遍提升或符合任一地区的求职法规。

## 用法

上游要求 Claude Code CLI、Python 3.10+、Bun，以及可用的 LaTeX 发行版；`/apply` 还可使用 `pypdf` 或 `pdftotext` 做 ATS 文本层检查。基本安装路径如下：

```sh
gh repo fork MadsLorentzen/ai-job-search --clone
cd ai-job-search

# 根据仓库 README 安装职位搜索 CLI
for tool in jobbank-search jobdanmark-search jobindex-search jobnet-search linkedin-search freehire-search; do
  (cd .agents/skills/$tool/cli && bun install)
done
```

在 Claude Code 中先运行 `/setup` 填写或导入自己的资料，再用 `/scrape` 搜索职位；对单个职位可执行：

```text
/apply https://jobindex.dk/job/1234567
```

随后由 `/apply` 评估职位、起草 CV/求职信、调用第二个 agent 审阅、编译 PDF 并进行文本层检查。不能抓取的职位页面可以粘贴职位描述，但仍应人工确认来源和条款。

## 原理

- `/setup` 将 CV、LinkedIn 导出、学历、推荐信和历史申请整理成结构化候选人资料；输入越完整，后续匹配越依赖真实经历而非通用措辞。
- `/scrape` 调用多个门户 skill，去重职位并展示候选；`/rank` 按个人的 deal-breaker、偏好和五类评估维度批量排序。
- `/apply` 采用 drafter-reviewer 分离：一个 agent 起草，新的上下文审阅公司/职位与草稿，随后回写修订；声明不支持的技能或经历必须保留为缺口。
- CV 用 `lualatex`、求职信用 `xelatex` 编译，再检查页数、孤行、字体和 PDF 文本层；ATS 检查针对实际提取结果，而不是只看 `.tex` 源码。
- `/outcome` 把申请材料、职位快照、面试阶段和结果归档，形成后续校准匹配规则的本地记录；Notion/Gmail 同步属于可选的外部连接。

## 价值

- 将职位搜索、材料生成、人工审阅、PDF 版式和结果追踪串成可重复的本地工作流，减少在多个工具间复制资料。
- drafter-reviewer 与“只使用真实资料”的规则，为定制化写作增加了一层事实与相关性审查。
- PDF 文本层和 ATS 检查能发现图标乱码、阅读顺序错误、页数溢出等仅靠肉眼或源文件不易发现的问题。
- 门户 skill、模板和评估规则可按国家、语言、岗位和个人约束替换，适合做一个可版本化的求职工作区。

## 风险边界

- 个人资料、联系方式、薪资、学历和申请历史属于高敏感数据；若使用公开 fork、云端模型、Gmail/Notion 或职位网站，必须先核对数据流、留存和访问范围。
- 上游明确职位描述是“不可信输入”，但指令级防御不是 sandbox；网页内容、链接、恶意文本和第三方 skill 仍可能影响 agent 行为。
- LinkedIn 等自动访问可能受服务条款限制；应低频、个人使用，并在授权和合规范围内保留人工控制，不应批量自动投递。
- 生成的 CV、求职信、薪资信息和面试答案可能存在事实错误、偏见或过度迎合；编译成功和 ATS 可解析不等于内容真实或适合岗位。
- `/gmail-sync`、`/notion-sync` 和职位门户会扩大网络与 OAuth 权限；外部同步前要确认只读/写入方向、撤销方式和组织政策。

## 补充建议

1. 用私有仓库保存个人资料，并把真实简历与可公开贡献分开；先以合成候选人和公开职位做端到端演练。
2. 逐个阅读门户 CLI 与 `settings` allowlist，确认依赖、生命周期脚本、网络域名和读写路径；新门户先离线测试再启用。
3. 把每份最终材料与对应职位快照、原始资料和人工修改记录一起归档；模型生成内容必须逐条核验，不要只看 ATS 分数。
4. 将自动化限制在搜索、排序和草稿；发送邮件、提交申请、接受 offer、记录 hired/declined 等决定保留人工确认。

## 参考资料

- [上游 README / 命令、工作流与安全说明](https://github.com/MadsLorentzen/ai-job-search)
- [上游 SETUP.md / 依赖与安装](https://github.com/MadsLorentzen/ai-job-search/blob/master/SETUP.md)
- [上游 SECURITY.md / 不可信职位描述与门户边界](https://github.com/MadsLorentzen/ai-job-search/blob/master/SECURITY.md)
- [GitHub API 元数据](https://api.github.com/repos/MadsLorentzen/ai-job-search)
- [GitHub Trending](https://github.com/trending)
