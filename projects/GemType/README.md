<!-- markdownlint-disable MD013 -->

# GemType

## 定位

`riponcm/GemType` 是一个开源 AI 写作助手和 Grammarly 替代品，覆盖 Chrome、Edge、Firefox、Microsoft Word，并计划支持 Safari 与移动键盘。它的核心卖点是 BYOK：用户用自己的 Google Gemini API key，项目本身不做中转服务器、账号体系或订阅收费。

## 用法

普通用户可以从浏览器商店安装扩展，再填入 Google AI Studio API key。开发者可克隆仓库，根据扩展目录和 README 中的说明构建对应浏览器版本或 Word task-pane add-in。

功能包括实时语法/拼写检查、一键修正、选中文本改写、正式/ casual 风格转换、按站点关闭、模型选择和语言设置。

## 原理

GemType 作为浏览器扩展监听网页文本输入区域，在用户暂停输入后将待检查文本发送到 Gemini API。它使用句子级上下文判断，而不是纯规则匹配；接受修正后会再次检查周围句子，避免单词级替换破坏句意。

隐私模型是“用户浏览器直接访问 Google Gemini API”，项目方声称不收集文本、不插入跟踪和分析。

## 价值

- 把 AI 写作助手从订阅 SaaS 转成开源 BYOK 工具。
- 对多语言写作、GitHub issue、邮件、社交平台输入都有直接实用价值。
- 相比传统语法工具，更容易自定义模型和成本。
- 对“浏览器扩展 + LLM API + 隐私承诺”的产品形态有参考价值。

## 风险边界

- 文本仍会发给 Google Gemini API；不经过项目服务器不等于完全本地隐私。
- BYOK 会把配额、账单、API key 泄露风险转给用户。
- 扩展需要较高网页输入权限，企业环境应先审计源码和发布包。
- Google Docs 等受平台限制的场景可能无法支持。

## 补充建议

- 企业内使用时建议通过浏览器策略统一安装、限制域名和管理 API key。
- 对敏感字段、内部系统和受监管数据默认关闭。
- 后续关注 Safari、移动键盘和 Word add-in 是否与主扩展保持同等隐私边界。

## 参考资料

- GitHub: <https://github.com/riponcm/GemType>
- Website: <https://gemtype.matily.org>
- Chrome Web Store: <https://chromewebstore.google.com/detail/linnnamnhkciekgpnegkcajcafmjlhgh>
- YouTube tutorial: <https://www.youtube.com/watch?v=j7Su-4hvigU>
