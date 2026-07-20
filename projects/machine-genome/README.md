<!-- markdownlint-disable MD013 -->

# machine-genome

## 定位

`machine-genome` 是 Pax Labs 发布的开放身份与 provenance 协议实现，用来给模型、agent、harness、数据集和中间产物建立可验证的身份记录与谱系关系。它不是推理框架，而是试图回答“这个 agent / 模型 / 数据产物到底由哪些组件、声明和签名构成”的基础设施项目。

## 今日信号

- GitHub：<https://github.com/paxlabs-inc/machine-genome>
- 官网/Registry：<https://machinegenome.org/>
- 创建时间：2026-07-20。
- 抓取时约 269 stars、7 forks。
- 语言 / 许可证：Go，Apache-2.0。

## 用法

项目提供 Go library、CLI、registry、Explorer、JSON Schema 与 OpenAPI 文档。典型流程是生成控制器密钥，初始化 genesis record，签名后用 CLI 验证并生成 Gene；registry 侧则负责接收、验证、保存记录，并提供可审计的 inclusion / consistency proof。

适合的使用场景包括：

- 为内部 agent、模型包装、数据集版本或工具链产物建立 signed identity。
- 在多 agent / 多模型系统中记录组件来源、父子关系和第三方 attestations。
- 为 agent 安全、模型供应链和审计系统提供 provenance 层。

## 原理

Machine Genome 把不可变 genesis record 做 canonicalization 后计算 content-addressed Gene，并用 W3C Data Integrity / EdDSA JCS proof 绑定签名身份。后续变更不改写 genesis，而是通过 amendments、attestations 和 lineage edges 追加证据。registry 使用 ACID 存储、Merkle log、signed checkpoints 和 tombstones 来支撑公开审计。

## 价值

- 把 agent / 模型身份从“名字和 README 声明”提升到“字节级记录 + 签名 + 谱系图”。
- 与当前 agent harness、skill、MCP server 爆发相呼应，为“谁构建了什么、谁声明了什么、证据是否变过”提供可验证基础。
- 不绑定区块链或特定模型厂商，工程落地门槛相对低。

## 风险边界

- 项目 README 明确声明 MGS 仍是实验性互操作 profile。
- 签名记录只能证明某个声明由某个 controller 签过、对应字节未变；不能证明能力、合法所有权、厂商背书或伦理状态。
- 需要配合组织内的密钥管理、命名空间控制和入库策略，否则 provenance 层也会被错误声明污染。

## 补充建议

- 后续跟踪其 registry 是否出现真实第三方生态使用，而不只是 reference implementation。
- 可与 `brain0`、`conversation-steganography`、`SkillSpector`、`open-kritt` 放在同一条“AI 供应链 / 安全 provenance”线索下观察。
- 若用于内部系统，先限制为离线验签和内部 registry，不宜直接依赖公共命名空间做强信任判断。

## 参考资料

- GitHub 仓库：<https://github.com/paxlabs-inc/machine-genome>
- 官网：<https://machinegenome.org/>
- README：<https://github.com/paxlabs-inc/machine-genome#readme>
- API：<https://github.com/paxlabs-inc/machine-genome/blob/main/api/openapi.json>
