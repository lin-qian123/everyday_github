<!-- markdownlint-disable MD013 -->

# courses

- 主上游：[anthropics/courses](https://github.com/anthropics/courses)
- 分类：AI 学习与教育资源。
- 核验日期：2026-10-24（Asia/Shanghai）；默认分支 `master` 快照 `f4dbb137d7b0`。
- [API](https://api.github.com/repos/anthropics/courses) 快照：22,921 stars / 2,519 forks / 94 open issues；公开发行列表为空；按固定默认分支 commit 阅读。累计量不是今日增长，主线也不等于发行版。

## 定位

Anthropic courses 是 Anthropic 的教育仓库，包含 API 基础、交互式提示工程、真实场景提示、提示评测和工具使用五条课程。它适合学习请求 / 响应与评测设计；内容带历史模型示例，不能作为当前模型可用性清单。 [README.md](https://github.com/anthropics/courses/blob/f4dbb137d7b02dddaf3cc73e32e20a702d3b5e77/README.md)

## 用法

按上游建议顺序学习五门课程，每门在独立 notebook 环境中安装所需依赖。API 入门 notebook 使用 `anthropic`、`python-dotenv` 与本地 `.env` 的 `ANTHROPIC_API_KEY`；先审阅所有 cell 和输出，再决定是否实际调用。评测课程共有九课，后半段接入 Promptfoo。 [anthropic_api_fundamentals/01_getting_started.ipynb](https://github.com/anthropics/courses/blob/f4dbb137d7b02dddaf3cc73e32e20a702d3b5e77/anthropic_api_fundamentals/01_getting_started.ipynb)、[prompt_evaluations/README.md](https://github.com/anthropics/courses/blob/f4dbb137d7b02dddaf3cc73e32e20a702d3b5e77/prompt_evaluations/README.md)

## 原理

通过可修改 notebook 展示 Messages API、参数、流式与多模态，再引入代码 / 人工 / 模型裁判评测。工具课把模型给出的 `tool_use` 交由应用执行，并用匹配的 `tool_use_id` 发送 `tool_result`；模型声明工具并不自行提供可信执行权限。 [tool_use/04_complete_workflow.ipynb](https://github.com/anthropics/courses/blob/f4dbb137d7b02dddaf3cc73e32e20a702d3b5e77/tool_use/04_complete_workflow.ipynb)

## 价值

适合掌握 LLM 应用协议和评测框架，尤其能与本轮 Promptfoo 项目形成“学习概念—搭建回归”的连续练习。平台官方教学仍需要用目标业务数据检验，不将示例输出当作实际运行验收。

## 风险边界

- 仓库没有公开 Release；API 基础示例仍写 `claude-3-haiku-20240307`，完整工具课使用 `claude-3-sonnet-20240229`。本轮未查询账号可用模型，运行前应按当前账号 / 官方文档更新模型与 SDK，不能直接照抄旧 ID。 [anthropic_api_fundamentals/01_getting_started.ipynb](https://github.com/anthropics/courses/blob/f4dbb137d7b02dddaf3cc73e32e20a702d3b5e77/anthropic_api_fundamentals/01_getting_started.ipynb)、[tool_use/04_complete_workflow.ipynb](https://github.com/anthropics/courses/blob/f4dbb137d7b02dddaf3cc73e32e20a702d3b5e77/tool_use/04_complete_workflow.ipynb)
- API 与模型裁判可能产生费用，notebook 历史输出不代表本轮成功。Wikipedia 等外部工具结果也可能无结果、歧义或含不可信内容；教程的简化工具分发不替代生产校验、超时、批准与多工具循环。 [tool_use/04_complete_workflow.ipynb](https://github.com/anthropics/courses/blob/f4dbb137d7b02dddaf3cc73e32e20a702d3b5e77/tool_use/04_complete_workflow.ipynb)
- 根许可为 CC BY-NC 4.0；部分子目录另带 LICENSE，改编或再发布时需按路径核对，不能把整仓库当成 MIT 软件包。 [LICENSE](https://github.com/anthropics/courses/blob/f4dbb137d7b02dddaf3cc73e32e20a702d3b5e77/LICENSE)

## 补充建议

优先使用公开合成问题，把工具实现换成可重复 mock，先验证 tool_use / tool_result 对应、错误返回和多轮终止，再以小预算做真实请求。记录模型 ID、SDK、提示词、测试集与费用。本轮仅阅读 README 和两个 notebook 的源单元，未执行课程、创建 API key 或复现其历史输出。

## 参考资料

- [README.md](https://github.com/anthropics/courses/blob/f4dbb137d7b02dddaf3cc73e32e20a702d3b5e77/README.md)（固定 commit）。
- [anthropic_api_fundamentals/01_getting_started.ipynb](https://github.com/anthropics/courses/blob/f4dbb137d7b02dddaf3cc73e32e20a702d3b5e77/anthropic_api_fundamentals/01_getting_started.ipynb)（固定 commit）。
- [prompt_evaluations/README.md](https://github.com/anthropics/courses/blob/f4dbb137d7b02dddaf3cc73e32e20a702d3b5e77/prompt_evaluations/README.md)（固定 commit）。
- [tool_use/04_complete_workflow.ipynb](https://github.com/anthropics/courses/blob/f4dbb137d7b02dddaf3cc73e32e20a702d3b5e77/tool_use/04_complete_workflow.ipynb)（固定 commit）。
- [LICENSE](https://github.com/anthropics/courses/blob/f4dbb137d7b02dddaf3cc73e32e20a702d3b5e77/LICENSE)（固定 commit）。
- [发行列表](https://github.com/anthropics/courses/releases)、[仓库 API](https://api.github.com/repos/anthropics/courses)（动态状态）。
