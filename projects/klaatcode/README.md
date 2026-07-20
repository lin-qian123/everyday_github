<!-- markdownlint-disable MD013 -->

# klaatcode

## 定位

`klaatcode` 是 KlaatAI 的终端原生开源 coding agent，定位接近 Claude Code、OpenAI Codex CLI、opencode 和 Aider。它的核心卖点是通过服务端 Klaatu 路由模型，把不同请求分配到不同成本和能力层级，并用代码知识图谱减少 agent 阅读仓库的 token 开销。

## 用法

```bash
npm install -g klaatcode
klaatcode
```

安装后在项目目录运行 CLI，让 agent 读取代码、编辑文件、运行命令和执行验证。项目 README 声称支持 Claude、GPT、Gemini、DeepSeek 等模型生态，并提供可复现实验基准。

## 原理

客户端是终端 agent 壳，关键智能层在 KlaatAI 托管服务：Klaatu 先判断请求复杂度，再路由到 `nano`、`fast`、`code`、`reason`、`heavy` 等层级。项目还宣称维护代码知识图谱，用符号、调用关系和语义搜索辅助 plan exploration，减少全仓库无差别读取。上下文压缩、成本监控、卡循环检测和验证流程被作为产品差异点。

## 价值

- 代表“开源客户端 + 托管路由服务”的 coding agent 商业化路线。
- 对成本敏感团队有参考价值：不是只换模型，而是把模型选择变成每次请求的动态决策。
- 可与 `opencode`、`grok-build`、`qwen-code`、`MiMo-Code` 做横向比较。

## 风险边界

- 智能路由和代码图谱关键能力在服务端，开源仓库不等于完全本地可复现。
- README 的成本优势来自项目自测 benchmark，需等待第三方复测。
- 使用托管服务意味着代码片段、提示和工具轨迹的隐私边界需要单独评估。
- license 元数据需复核仓库实际文件，不能只依赖 GitHub API。

## 补充建议

- 试用时应记录同一任务在 Codex、Claude Code、opencode 和 Klaat Code 上的成本、修改质量和测试结果。
- 对私有仓库使用前先确认数据保留、模型路由日志和企业合规条款。
- 如果团队已有本地 MCP/索引体系，需评估它的代码图谱是否可替代或只是叠加成本。

## 参考资料

- GitHub：<https://github.com/KlaatAI/klaatcode>
- 项目主页：<https://klaatai.com>
- benchmark 说明：<https://github.com/KlaatAI/klaatcode#benchmarks>
