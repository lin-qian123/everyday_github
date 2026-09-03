<!-- markdownlint-disable MD013 MD034 -->

# Humanizer：用可审阅规则减少 AI 写作痕迹的 Agent Skill

## 项目概览

- 上游仓库：https://github.com/blader/humanizer
- GitHub API 快照（2026-09-04）：41,425 stars、3,546 forks、31 个开放 issue
- 当前 GitHub release：`v2.11.1`；README 版本记录已写到 `2.11.2`
- 主要形态：Markdown `SKILL.md`、35 类写作模式、Claude Code / Codex / Cursor 等 skill 宿主
- 许可证：MIT

## 定位

Humanizer 是一个纯 Markdown 的写作 skill，用 35 类可读规则识别和改写常见的 AI 腔，包括空泛升格、营销语气、机械排比、过度小标题、虚假引语、模板化转折和不必要的聊天式收尾。

它是编辑规则与 agent 提示，不是 AI 文本检测器、事实核验器或“绕过检测”保证。上游要求保留姓名、数字、日期、引文与来源事实，但最终语义和作者责任仍需人工复核。

## 用法

可通过 Skills CLI 安装，也可把根目录 `SKILL.md` 手动复制到宿主的 skills 目录：

```bash
npx skills add blader/humanizer --global
```

安装后可直接调用 `/humanizer`，粘贴文本，或要求 agent 只改某个文件中的 prose。需要贴近个人声口时可额外提供自己的写作样本；处理代码、frontmatter、表格或引文时应先用副本确认保留边界。

## 原理

Skill 的规则来源之一是 Wikipedia WikiProject AI Cleanup 总结的“Signs of AI writing”。工作流先做一轮不受原段落结构约束的改写，再批评仍显机械的部分并给出最终稿；个人样本可覆盖部分默认风格偏好。

核心机制仍是宿主模型执行自然语言指令，没有独立 parser、事实数据库或确定性验证器。不同模型、上下文和宿主版本可能对同一规则做出不同解释。

## 价值

- 规则和示例都可直接审阅、版本化和局部修改。
- 把“更自然”拆成具体模式，方便编辑者指出问题而非只给模糊风格词。
- 纯 Markdown 便于在多个支持 Agent Skills 的宿主间复用。
- 明确要求不发明事实，并支持按作者样本调整声口。

## 风险边界

- 更像人写不等于事实正确、原创、无抄袭、符合披露政策或不会被检测工具标记。
- 规则可能抹平学术、法律、技术写作所需的精确重复与固定术语。
- 给 skill 输入未可信网页或长文时，仍可能把其中的提示注入带入宿主上下文。
- 安装第三方 skill 会影响 agent 行为；应固定 commit/release 并审查 `SKILL.md` 变更。
- README 的“保留事实”是行为约束，不是确定性证明；数字、引用、链接与否定词仍需逐项对照。
- 本页只核验上游 README、skill 与 API，没有对不同模型做盲评或语义保持测试。

## 补充建议

1. 用带数字、引用、术语、否定句和代码块的金标文本做回归，逐项比较语义与格式。
2. 把“删模板腔”“保留作者声口”“不得新增事实”拆成独立验收项，不用单一检测分数代替人工审稿。
3. 在项目内固定版本，升级前审查 35 类规则和安装脚本的 diff。
4. 对论文、法律材料、新闻和对外声明保留原始稿、改写稿与变更记录。
5. 若组织要求披露 AI 辅助写作，不因文本被改得自然就省略披露。

## 参考资料

- 仓库与 README：https://github.com/blader/humanizer
- Skill 源文件：https://github.com/blader/humanizer/blob/main/SKILL.md
- Releases：https://github.com/blader/humanizer/releases
- Skills 页面：https://skills.sh/blader/humanizer
- Wikipedia 写作模式来源：https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing
