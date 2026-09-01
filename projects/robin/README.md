<!-- markdownlint-disable MD013 MD034 -->

# robin：用 Tor、搜索与 LLM 组织暗网 OSINT 调查

## 项目概览

- 上游仓库：https://github.com/apurvsinghgautam/robin
- GitHub API 快照（2026-09-02）：6,921 stars、1,299 forks、15 个开放 issue
- 当前 release：`v2.8`
- 主要技术：Python、Streamlit、Tor、搜索/抓取模块、多模型 LLM 接口
- 许可证：MIT

## 定位

Robin 是面向合法暗网 OSINT 的调查辅助工具。它通过 Tor 访问搜索入口，利用 LLM 改写查询、过滤结果、汇总材料，并在 Streamlit 中支持基于同一调查数据的追问和线索跳转。

它不是执法数据库、漏洞利用器或事实判定系统。暗网内容的合法性、真实性、时效、来源身份和证据可采性都不能由摘要自动证明。

## 用法

上游推荐在已运行 Tor 的环境中使用 Docker：

```bash
docker pull apurvsg/robin:latest
docker run --rm \
  -v "$(pwd)/.env:/app/.env" \
  --add-host=host.docker.internal:host-gateway \
  -p 8501:8501 \
  apurvsg/robin:latest
```

开发方式要求 Python 3.10+，安装依赖后用 `streamlit run ui.py` 启动。真实调查前必须获得书面授权，明确法律辖区、允许访问的来源、数据保存、升级报告和停止条件。

## 原理

Robin 将流程拆成搜索、抓取与 LLM 三层：搜索层经 Tor 获取候选结果，抓取层收集文本，LLM 层改写查询、过滤和生成调查摘要；已保存调查可用于 grounded follow-up，并从建议问题启动新的 pivot。

“基于调查数据回答”能缩小上下文范围，但不能排除抓取错误、诱导内容、重复来源、伪造身份、提示注入或模型幻觉。

## 价值

- 把暗网搜索、材料筛选、摘要和追问集中到一个可审阅界面。
- 多模型与 OpenAI-compatible 接口便于比较本地和云端处理边界。
- 保存调查工件有助于复盘查询、来源和分析过程。
- 模块化搜索/抓取/LLM 结构适合在授权实验室中替换组件。

## 风险边界

- 访问、下载或保存某些内容可能违法或违反机构政策；“OSINT”标签不是普遍授权。
- 恶意页面可能含 exploit、追踪、非法材料和 prompt injection；Tor 只改变网络路径，不提供完整安全隔离。
- 把敏感查询、实体名或原始材料发送到第三方 LLM 会形成新的数据披露链。
- 摘要可能合并同名实体、夸大弱线索或丢失否定语义，不能直接作为指控或执法结论。
- Docker 命令暴露本地 `.env`、网络和 Web 端口；镜像来源、哈希、更新与日志保留需单独治理。
- 本页依据上游 README、release 和 API，未连接 Tor、未访问暗网，也未验证调查准确率。

## 补充建议

1. 仅在书面授权和法律顾问确认的范围内运行；优先使用离线、合成或公开训练样本。
2. 在隔离 VM 中固定镜像 digest，限制下载类型、文件大小、脚本执行和对内网访问。
3. 默认用本地模型处理原始材料；如需云模型，先脱敏并记录 provider、地区和保留政策。
4. 为每条结论保存 URL、时间、哈希、原文片段和独立复核状态，区分线索与已证实事实。
5. 对网页内容做纯文本化和提示注入标记，不让抓取内容直接决定工具调用或外部动作。

## 参考资料

- 仓库与 README：https://github.com/apurvsinghgautam/robin
- Releases：https://github.com/apurvsinghgautam/robin/releases
- Docker Hub：https://hub.docker.com/r/apurvsg/robin
- 上游架构图：https://github.com/apurvsinghgautam/robin/blob/main/.github/assets/robin-workflow.png
- README 引用的原始 X 演示：https://x.com/fr0gger_/status/1908051083068645558
