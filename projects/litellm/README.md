<!-- markdownlint-disable MD013 -->

# litellm

- 主上游：[BerriAI/litellm](https://github.com/BerriAI/litellm)
- 分类：模型、训练与推理基础设施。
- 核验日期：2026-10-23（Asia/Shanghai）；主线快照 `f2118fc7670b`。
- [API](https://api.github.com/repos/BerriAI/litellm) 快照：61,835 stars / 12,579 forks / 5,619 open issues；发行列表首项 [v1.106.2](https://github.com/BerriAI/litellm/releases/tag/v1.106.2)（UTC 2026-10-21，正式）。累计值不代表今日增量。

## 定位

LiteLLM 以统一接口连接多家模型服务，可作为 Python SDK 嵌入程序，也可作为集中 AI Gateway / Proxy 提供认证、virtual keys、路由、费用和观测能力。“兼容接口”主要减少接入适配，不保证各模型的工具调用、结构化输出和错误语义完全相同。[README](https://github.com/BerriAI/litellm/blob/f2118fc7670ba3fa736d9b8f4deef9077a45a720/README.md)

## 用法

先选 SDK 或团队网关：单应用优先小范围验证 SDK；多租户服务才引入网关、数据库、缓存和管理面。SDK 项目可从已核定版本的独立环境开始，例如：

```bash
python -m pip install "litellm==1.106.2"
```

随后按所选 provider 的文档配置模型标识与 key。上游建议服务制品选经过其负载测试的 `-stable` 镜像；生产应固定具体 tag / digest 并核签名，不能用滚动标签代替可复现版本。[正式发行](https://github.com/BerriAI/litellm/releases/tag/v1.106.2)

## 原理

适配层将统一请求转换为 provider API，整理响应、usage 与异常；Router 在部署间分配请求并执行重试 / fallback。Proxy 把这些能力集中为服务，再叠加租户 key、限额、缓存和观测回调。上游“100+ providers”是覆盖描述，本轮未逐一验证。[接口与部署说明](https://github.com/BerriAI/litellm/blob/f2118fc7670ba3fa736d9b8f4deef9077a45a720/README.md)

## 价值

适合已有多模型接入、希望集中管理密钥、追踪成本和做容灾的团队。评估应覆盖业务结果、总调用费用和故障行为，避免把统一接口的便利等同于模型质量或可用性的提升。

## 风险边界

- 网关成为请求正文、上游密钥和路由的集中信任点；日志、缓存、回调与 fallback provider 都可能扩展数据接收方。是否脱敏、哪些字段落盘应在所选配置中验证。
- 自动重试和 fallback 会影响费用、限流及工具副作用，需测试流式中断、超时和重复请求；预算统计不能自动覆盖网关外的直连调用。
- 发行列表首项为 v1.106.2，但采样主线 `pyproject.toml` 已为 1.108.0、Python `>=3.10,<3.15`。这些依赖要求属于主线快照，不应反推正式版完全相同。[manifest](https://github.com/BerriAI/litellm/blob/f2118fc7670ba3fa736d9b8f4deef9077a45a720/pyproject.toml)
- API 许可证识别为 NOASSERTION；根 LICENSE 明确主体 MIT，并将 `enterprise/` 排除到单独许可。根文件指向的 `enterprise/LICENSE` 返回 404，本轮从目录 tree 找到实际的 `LICENSE.md`：企业代码生产使用需相应协议与有效席位许可，开发 / 测试有单独允许范围，不能套主体 MIT。[根许可](https://github.com/BerriAI/litellm/blob/f2118fc7670ba3fa736d9b8f4deef9077a45a720/LICENSE)、[实际企业许可](https://github.com/BerriAI/litellm/blob/f2118fc7670ba3fa736d9b8f4deef9077a45a720/enterprise/LICENSE.md)
- README 已说明文档贡献迁至单独 litellm-docs 仓库；查文档需注意版本与代码同步。

## 补充建议

用 mock upstream 验 key scope、并发限额、计费更新、错误映射与流式取消，再对同一脱敏小集比较 provider 质量、延迟和费用。先关闭不需要的日志回调并固定数据出口。本轮未安装 SDK、启动代理、申请云资源或调用模型。

## 参考资料

- [README.md](https://github.com/BerriAI/litellm/blob/f2118fc7670ba3fa736d9b8f4deef9077a45a720/README.md)（固定 commit）。
- [LICENSE](https://github.com/BerriAI/litellm/blob/f2118fc7670ba3fa736d9b8f4deef9077a45a720/LICENSE)（固定 commit）。
- [pyproject.toml](https://github.com/BerriAI/litellm/blob/f2118fc7670ba3fa736d9b8f4deef9077a45a720/pyproject.toml)（固定 commit）。
- [enterprise/LICENSE.md](https://github.com/BerriAI/litellm/blob/f2118fc7670ba3fa736d9b8f4deef9077a45a720/enterprise/LICENSE.md)（固定 commit；修正根文件中的旧路径）。
- [正式发行列表](https://github.com/BerriAI/litellm/releases)、[仓库 API](https://api.github.com/repos/BerriAI/litellm)（动态状态）。
