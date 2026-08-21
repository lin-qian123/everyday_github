<!-- markdownlint-disable MD013 -->

# modelprint

> 上游仓库：[unclecode/modelprint](https://github.com/unclecode/modelprint) · 归类：模型、训练与推理基础设施 · 本页基于 2026-08-22 的上游 README 与 GitHub API 快照整理。

## 定位

`modelprint` 是一个浏览器端工具，用九类基础设施探针对比 OpenAI 兼容 API 的 tokenizer、模板偏移、参数校验、错误码和 `finish_reason` 等响应特征。它试图回答“某端点背后可能是哪一类基础设施”，不是模型身份认证、质量评测、安全扫描器或供应商合规证明。

API 快照：约 29 stars、3 forks、1 个开放 issue；创建于 2026-08-21；许可证 MIT。README 的示例分析及“命中数”均为项目方材料，不能据此确认任何未公开模型、路由策略或供应商关系。

## 用法

上游提供静态页面，无需安装、构建或自建服务；浏览器从本机直接向选定 provider 发送请求。若要审计其探针逻辑，可克隆仓库后运行：

```sh
git clone https://github.com/unclecode/modelprint.git
cd modelprint
node smoke.mjs
node suspects.mjs
```

README 说明上述脚本需要 OpenRouter key。仅使用自己有权访问、允许该类测试的端点；在发送任何 key 或请求前，先阅读 provider 的条款、速率限制、数据处理与可接受使用政策。

## 原理

- 四项 tokenizer probe 对固定英文、中文、代码与 emoji/稀有 Unicode 输入读取 `usage.prompt_tokens`，并用单字符基线做归一化，降低隐藏 prompt template 的干扰。
- 其余 probe 观察超范围 `temperature`/`max_tokens` 的校验文本、错误码家族和 `finish_reason` 词表；同一 probe 的结果可并排比较。
- 对路由端点，工具尝试标记 router-reported 或 router-validated 情形，并对 tokenizer probe 重跑两次以发现后端漂移。自定义 probe 以单个 JavaScript 文件加入、由索引注册。

## 价值

- 让 API 兼容性排障从“回复风格猜测”转向可记录的请求/响应差异，便于比较 tokenizer、错误语义和接口形状。
- 纯浏览器架构减少了另起中转服务器保管 API key 的需要，但不代表请求不会被浏览器扩展、代理、provider 或本地日志暴露。
- 可扩展的 probe contract 有助于团队把发现过程写成可审查实验，而不是散落在社媒截图中的推测。

## 风险边界

- 相似 fingerprint 最多支持“共享某些基础设施特征”的推断，不能证明模型权属、训练来源、实际权重或供应商身份；路由、缓存、A/B 实验和网关都能造成误判。
- 错误探测可能触发配额、费用、告警或违反 API 条款。不得对第三方、生产或无授权端点进行枚举、压力测试或规避访问控制。
- API key 输入浏览器页面仍有泄露面：浏览器扩展、开发者工具、恶意脚本、公司代理和同步 profile 都应纳入威胁模型。
- 端点响应会随部署变化；单次结果没有时间稳定性。公开发布推断前应记录时间、区域、请求、响应、版本和不确定性。

## 补充建议

1. 在专用浏览器 profile 使用低权限、可撤销、限额的测试 key；关闭不必要扩展，避免在共享电脑或录屏中输入凭据。
2. 选取已知 provider 做盲测，测量在不同区域、时间、路由和温度下的稳定性及误归类率，再对未知端点做有限推断。
3. 将每条结论写成“观测到的响应特征 + 备选解释”，而不是“确认某模型身份”；保留原始响应并做好敏感字段脱敏。
4. 将 API 测试纳入书面授权、速率限制和成本预算；若目的是供应链审计，另配合合同、SBOM、源代码和官方声明验证。

## 参考资料

- [上游 README 与在线页面](https://github.com/unclecode/modelprint)
- [GitHub API 元数据](https://api.github.com/repos/unclecode/modelprint)
- [OpenAI API 数据使用政策](https://openai.com/policies/api-data-usage-policies/)
- [OpenRouter 文档](https://openrouter.ai/docs)
