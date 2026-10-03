<!-- markdownlint-disable MD013 -->

# User Scanner（kaifcodec/user-scanner）

> 上游仓库：<https://github.com/kaifcodec/user-scanner> · 归类：办公、商业与行业应用 · 本页基于 2026-10-04 的 GitHub API、README、cross-scan / proxy 文档、Python manifest、Release 与 LICENSE 静态整理，未扫描任何用户名、邮箱、账号、泄露数据或第三方平台。

- 抓取快照：5,208 stars、528 forks、18 open issues。
- 热度信号：GitHub Python Trending 抓取时约 +70 当日 stars。
- 版本与许可：MIT；latest Release / tag 为 `v1.5.2`，Python manifest 已写 `1.5.2.1`，存在制品口径时差。

## 定位

User Scanner 是邮箱与用户名 OSINT CLI / Python 库，并可作为 stdio MCP server 接入 Agent。它在大量网站上检查注册与公开档案，抓取头像、简介、关注量和标识符，再从公开链接、别名与邮箱做多跳 pivot；还可查询 Hudson Rock infostealer breach intelligence。

## 用法

可从 PyPI 安装 `user-scanner`，用 `-u` / `-e` 扫描单个目标，按 category / module 限定范围，或对文件批量处理；`--cross-scan` 进行别名 / 邮箱 / profile link 递归，结果可导出 PDF、JSON、CSV。安装 `user-scanner[mcp]` 后运行 `user-scanner-mcp`，向 Agent 暴露用户名扫描、邮箱扫描和模块枚举工具。

## 原理

引擎以每个平台模块构造请求，并用 `httpx` / `curl_cffi` 并发检查响应、提取公开 metadata 和判断账号状态；cross-scan 把可信链接与新标识符规范化为后续任务。代理池、TLS fingerprint impersonation 和模块目录扩大覆盖面，MCP 层则把这些参数化扫描能力交给模型调用。

## 价值

对经授权的数字足迹调查、账号冒用排查、威胁情报和事件响应，统一 CLI、结构化结果和多跳证据能减少手工逐站查询；模块化目录与 JSON / CSV 输出也方便把原始命中交给人工复核，而不是只看一段模型总结。

## 风险边界

- 邮箱、用户名、头像、社交关系和 breach 线索都可能是个人数据；“公开可访问”不自动等于允许批量聚合、画像、长期保存或交给 LLM。
- 响应启发式、站点改版、同名账号、代理 / 地区差异和反爬页面会造成 false positive / false negative；命中不证明目标本人拥有账号或遭到感染。
- `--cross-scan`、批量文件和 MCP 自主调用会迅速扩大查询范围与请求量；必须设书面目的、allowlist、深度、速率、保留期和人工确认，不应默认全网 pivot。
- TLS impersonation、代理轮换和 2,710+ 模块可能触发平台条款、封禁或法律限制；上游免责声明不能代替目标授权、隐私影响评估与当地法律意见。
- Hudson Rock 数据属于第三方 breach intelligence；来源、时效、许可、误报、通知义务与访问条款应独立核验。
- Release `v1.5.2` 与 manifest `1.5.2.1` 不一致；PyPI、tag 和源码不能混写成一个已验证版本。

## 补充建议

仅对自有或书面授权标识符运行，默认单 module、小并发、无 cross-scan、无第三方 breach 查询；保存每条命中的 URL、时间、状态码与人工复核结论，并及时删除不相关个人数据。接入 MCP 时为扫描工具增加 allowlist、预算、审批和不可递归上限，永不把未核实关联写成身份事实。

## 参考资料

- [GitHub 仓库](https://github.com/kaifcodec/user-scanner)
- [GitHub REST API](https://api.github.com/repos/kaifcodec/user-scanner)
- [README 与 CLI 用法](https://github.com/kaifcodec/user-scanner/blob/main/README.md)
- [Cross-scan 文档](https://github.com/kaifcodec/user-scanner/blob/main/docs/CROSS_SCAN.md)
- [CLI flags（含 proxy / delay）](https://github.com/kaifcodec/user-scanner/blob/main/docs/FLAGS.md)
- [Python manifest](https://github.com/kaifcodec/user-scanner/blob/main/pyproject.toml)
- [v1.5.2 Release](https://github.com/kaifcodec/user-scanner/releases/tag/v1.5.2)
- [LICENSE](https://github.com/kaifcodec/user-scanner/blob/main/LICENSE)
