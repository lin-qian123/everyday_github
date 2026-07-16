<!-- markdownlint-disable MD013 -->

# coder_eval

## 定位

`UiPath/coder_eval` 是一个用于评估 AI coding agents 及其 skills 的框架。它强调 sandbox、可复现任务、连续评分、agent 抽象、实验对照和 telemetry，目标不是做又一个排行榜，而是帮助 CLI/skill 作者验证 agent 和 skill 是否真的有效。

## 用法

README 给出 `uv` 工作流：安装依赖、配置 `.env`，用 `coder-eval plan` 校验任务，再用 `coder-eval run` 执行评估，并通过 `coder-eval report` 查看结果。它支持 Claude Code、Codex、Antigravity 等 agent，后续可通过 plugin SPI 扩展。

## 原理

框架用 YAML 描述任务、依赖和成功条件，在隔离环境中运行 agent，并按文件检查、代码相似度、LLM rubric、skill trigger 等 criterion 给出加权分数。它还记录工具调用、token、成本和实时流，以便对不同模型、prompt、skill 和配置做 A/B 测试。

## 价值

- 把 agent skill 从“感觉有用”推进到可回归、可比较、可 CI gate。
- 适合 skill 作者验证模型更新后 skill 是否仍会触发、是否仍能完成任务。
- 支持连续评分，比纯 pass/fail 更能描述部分完成和退化。
- 对团队内部构建真实任务 benchmark 有直接参考价值。

## 风险边界

- README 标注 telemetry 默认开启，虽然声明不采集 prompt/file/path，但使用前仍应按组织政策决定是否关闭。
- Python 3.13+ 和 uv 要求可能提高接入成本。
- LLM rubric 与 sandbox scoring 都需要审查，不能把分数直接等同生产质量。
- 评估任务如果过窄，可能导致 skill 过拟合。

## 补充建议

- 为关键 agent skills 建立最小 CI suite，覆盖触发、成功输出、失败回退和成本上限。
- 固定模型、工具版本和任务数据，避免结果不可复现。
- 与 `bridgebench` 区分使用：coder_eval 更适合自有 agent/skill 回归测试。

## 参考资料

- GitHub: <https://github.com/UiPath/coder_eval>
- PyPI: <https://pypi.org/project/coder-eval/>
