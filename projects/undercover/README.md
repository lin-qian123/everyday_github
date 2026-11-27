<!-- markdownlint-disable MD013 -->

# undercover：通过虚构理赔业务学习 Agent 工程与部署

- 上游：[ed-donner/undercover](https://github.com/ed-donner/undercover)，repository ID `1377599321`；2026-11-28 新建档案。
- 快照：133 stars / 323 forks / 10 open issues（累计，含 PR）；Jupyter Notebook daily +3。forks 多于 stars 不能单独解释学习人数或项目质量。
- 默认 SHA `93c0867c4916c2a4ceef83849bbb441367fd8394`，2026-11-26；所见 Releases 为空。另核 `week3day5-end` 提交 `6d5005236a37bd6bd22402f1e160b0d8a42eabb0`，同日更新，不能把它的完整功能归给 main。
- 范围：两分支非截断 tree、固定课程说明 / manifest / 阶段状态，以及结束分支的鉴权、筛查、Gateway、checkpoint、API 和赔付计算局部源码；未安装、运行实验、登录云平台、调用模型或部署。

## 定位

Edward Donner 的 AI FDE / Agentic AI Architect 配套课程仓库。UnderCover 是虚构旅游保险公司，课程在三周内逐步构建理赔后台、处理 Agent、人工审核、评估和云部署，适合练习把模型接到有状态业务中。

main 的 `docs/STATUS.md` 明确仍为 hello-world 骨架；课末参考实现位于命名分支。README 的企业级描述属于课程目标，不代表主分支开箱提供完整产品，更不是可直接处理真实保险或付款的系统。

## 用法

1. 从 `setup/INSTRUCTIONS.md` 和前两天 notebook 开始。Python manifest 要求 ≥3.12；安装指南说 Node ≥24，`package.json` 则列出更细版本区间，需核对实际运行版本与锁文件。
2. 在独立学习目录固定 SHA，按天选择 `week…-start` 或 `week…-end`。保留自己的修改；README 提醒 `.env` 不进 Git，切换分支也会继续保留同一份凭据。
3. main 用于自己从骨架构建；若阅读课末实现，应明确选择本页结束分支 SHA。常见学习命令如下，仅列出，未执行：

   ```bash
   uv sync
   npm install
   npm run check
   npm run dev
   ```

4. `npm install` 的 prepare 脚本会安装 lefthook 和 Playwright Chromium，不只是下载普通 JS 依赖。先阅读 scripts，再决定允许的安装行为。
5. 课程有付费模型和名字带 `free` 的替代 notebook；作者约 10 美元的课程 API 估计不是费用上限。AWS / Render、Supabase、Langfuse、AgentCore、模型 provider 各自有账户、数据出口和动态额度。

## 原理

课程将业务规则、数据和产品要求写在文档中，再由学习者逐步实现 FastAPI 后端、React 仪表盘和 Agent。结束分支采用 LangGraph 保存执行进度，Postgres checkpointer 使用独立 schema 与每进程最多四条连接；这支持研究中断 / 恢复，但不单独保证业务操作只发生一次。

局部源码把赔付额度计算放在后端确定性函数中，按项目虚构保单规则生成分步计算；Agent 负责解释和调用工具。结束分支的 Agent API 只选择六个操作；早期安全产品 brief 曾要求八个，后来文档检索移到独立 context 层，阶段差异需分开。

结束分支 `screening.py` 用第二个模型对客户材料做结构化指令筛查；API key 比较采用 `secrets.compare_digest`，未设置预期 key 时拒绝匹配。Gateway 从环境读取 URL，未设置返回 None；设置后使用 AWS SigV4 凭据调用。源码具备这些机制，不等于任意部署都经过 Gateway 或已经抵御提示注入。

## 价值

它把技术选择放进具体业务约束：计算规则归后端、人工签核、重启恢复、版本化改进、评估与部署，各阶段都有 brief 和参考实现。学习者可对比同一需求在不同阶段如何落到状态、权限和工具边界。

完整阶段文档也适合检验 coding agent 是否真的完成用户要求。不过状态页记录的作者 live checks、课堂小样本和离线 tests，不能替代本轮环境复现、独立测试或生产审计。

## 风险边界

| 议题 | 已核事实与边界 |
| --- | --- |
| 分支与阶段 | main 是骨架，课末分支有完整实现；manifest 的 0.1.0 不是 GitHub 稳定发行标识。早期 brief 的要求与最终架构不宜混读。 |
| 课程数据 | 公司、保单和赔付为教学设计；不能当真实承保、监管、财务或支付系统。 |
| 审核与幂等 | Durable brief 描述的“签核后 Agent 付款”在后期改为后端签核直接记录付款；应按目标分支验证重复请求、重启、拒绝和恢复，不能仅凭 checkpoint 宣称 exactly-once。 |
| 安全筛查 | 第二模型筛查依赖模型和输入分布；教学样本通过不证明所有改写或跨字段注入都能检出，模型判断也不是权限控制。 |
| 路由与身份 | Gateway URL 缺省时不启用该对象；Agent key 与已登录 handler 是不同身份。要验实际路由、AWS policy 和后端授权，不只看函数名。 |
| 数据与费用 | 保单、客户材料、trace、memory 和云数据库会跨不同服务；先用合成材料，核实日志、留存、密钥及预算。免费替代不保证全部服务永远免费。 |
| 许可 | API license 为空；两分支 tree 未见 LICENSE / COPYING。公开可读不等于已获通用复制、分发或商业使用许可，复用前向作者确认。 |

## 补充建议

1. 固定课程阶段、提交、依赖锁和合成数据，先跑无需云 / 模型的检查，再按有限预算做少量 live 样本，分别记录结果。
2. 用独立隐藏理赔集评价决策、金额、解释与引用；不要只优化同一批课堂样本或只看模型裁判得分。
3. 为签核、重复付款、中途终止、服务不可达和数据库恢复设计故障实验；验清后端业务效果及审计身份。
4. 收集目标阶段的真实路由与授权证据，检查 key 缺失 / 错误、handler 操作和 Gateway 拒绝；需要复用时先解决许可证缺口。

## 参考资料

- [仓库 API](https://api.github.com/repos/ed-donner/undercover)、[固定 README](https://raw.githubusercontent.com/ed-donner/undercover/93c0867c4916c2a4ceef83849bbb441367fd8394/README.md)、[main 状态](https://raw.githubusercontent.com/ed-donner/undercover/93c0867c4916c2a4ceef83849bbb441367fd8394/docs/STATUS.md)、[安装说明](https://raw.githubusercontent.com/ed-donner/undercover/93c0867c4916c2a4ceef83849bbb441367fd8394/setup/INSTRUCTIONS.md)、[Python manifest](https://raw.githubusercontent.com/ed-donner/undercover/93c0867c4916c2a4ceef83849bbb441367fd8394/pyproject.toml)、[npm scripts](https://raw.githubusercontent.com/ed-donner/undercover/93c0867c4916c2a4ceef83849bbb441367fd8394/package.json)。
- 阶段 brief：[Durable](https://raw.githubusercontent.com/ed-donner/undercover/93c0867c4916c2a4ceef83849bbb441367fd8394/labs/week2day3_product_DURABLE.md)、[Secure](https://raw.githubusercontent.com/ed-donner/undercover/93c0867c4916c2a4ceef83849bbb441367fd8394/labs/week3day2_product_SECURE.md)。
- 结束分支固定文件：[状态](https://raw.githubusercontent.com/ed-donner/undercover/6d5005236a37bd6bd22402f1e160b0d8a42eabb0/docs/STATUS.md)、[技术栈](https://raw.githubusercontent.com/ed-donner/undercover/6d5005236a37bd6bd22402f1e160b0d8a42eabb0/docs/TECH_STACK.md)、[API key](https://raw.githubusercontent.com/ed-donner/undercover/6d5005236a37bd6bd22402f1e160b0d8a42eabb0/backend/api_key.py)、[六操作 API](https://raw.githubusercontent.com/ed-donner/undercover/6d5005236a37bd6bd22402f1e160b0d8a42eabb0/backend/agent_api.py)、[赔付计算](https://raw.githubusercontent.com/ed-donner/undercover/6d5005236a37bd6bd22402f1e160b0d8a42eabb0/backend/payout.py)、[筛查](https://raw.githubusercontent.com/ed-donner/undercover/6d5005236a37bd6bd22402f1e160b0d8a42eabb0/agent/screening.py)、[Gateway](https://raw.githubusercontent.com/ed-donner/undercover/6d5005236a37bd6bd22402f1e160b0d8a42eabb0/agent/gateway.py)、[checkpoint](https://raw.githubusercontent.com/ed-donner/undercover/6d5005236a37bd6bd22402f1e160b0d8a42eabb0/agent/checkpoints.py)。
