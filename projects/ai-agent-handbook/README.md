<!-- markdownlint-disable MD013 -->

# ai-agent-handbook（AI Agent Handbook）

- 上游：[aliyun/ai-agent-handbook](https://github.com/aliyun/ai-agent-handbook)；分类：**AI 学习与教育资源**。
- 核验：2026-11-18（Asia/Shanghai）07 时段；仓库 ID `1365520317`，main `ce08fbc496fadf4066c4e1036c418826e6ae2c99`。本轮抽样阅读章节与练习实现，未通读全书或运行练习。
- 热度：官方 JavaScript daily **+71**；[API](https://api.github.com/repos/aliyun/ai-agent-handbook)累计 **3,442 stars / 426 forks / 6 open issues（含 PR）**；本轮 [Releases](https://github.com/aliyun/ai-agent-handbook/releases) 列表为空，不把持续更新书稿写成已发布的稳定软件包。

## 定位

阿里云维护的中文企业 Agent 工程手册，围绕架构、构建、运行、治理、调优、实践和展望组织内容，并附开发者调研与浏览器代码练习。适合开发者、架构师、运维和业务负责人建立共同概念；它是持续修订的知识项目，不是一个统一可部署的 Agent runtime。[固定 README](https://github.com/aliyun/ai-agent-handbook/blob/ce08fbc496fadf4066c4e1036c418826e6ae2c99/README.md)

## 用法

先在[在线书站](https://aliyun.github.io/ai-agent-handbook/)按任务选读：需要明确责任时看 Harness / Runtime / Sandbox；准备上线时看权限、观测、行为仿真；改进质量时看黄金集、轨迹与 Badcase。

本地阅读站的脚本要求 Node `>=22`；固定源码后可安装依赖并运行：

```bash
git clone https://github.com/aliyun/ai-agent-handbook.git
cd ai-agent-handbook
git checkout ce08fbc496fadf4066c4e1036c418826e6ae2c99
npm ci
npm run dev
```

`dev` 先生成 challenges 再启动仅监听 loopback 的 VitePress；`npm run check` 包括书稿结构、四组 challenge 和游戏检查，`npm test` 是 Playwright。以上为静态读取脚本，不代表本轮执行成功。[package.json](https://github.com/aliyun/ai-agent-handbook/blob/ce08fbc496fadf4066c4e1036c418826e6ae2c99/package.json)

## 原理

- 以 Model + Harness 解释 Agent：Harness 组织任务、上下文、能力、状态和控制；Runtime 承载运行，Sandbox 限制行动。第 03 章列出不同构建起点，不把它们排列成统一成熟度阶梯。[第 03 章](https://github.com/aliyun/ai-agent-handbook/blob/ce08fbc496fadf4066c4e1036c418826e6ae2c99/02-build/%E7%AC%AC%2003%20%E7%AB%A0%E3%80%80%E8%8C%83%E5%BC%8F%EF%BC%9AHarness%20%E7%9A%84%E4%B8%BB%E6%B5%81%E6%9E%84%E5%BB%BA%E6%96%B9%E5%BC%8F%E5%92%8C%E8%B4%A3%E4%BB%BB%E8%BE%B9%E7%95%8C.md)
- 第 16 章将场景、版本化资产、执行记录、事实观测、证据与评估分开；仿真提供受控材料，评价再判断任务是否成功。真实请求也可能属于隔离测试，关键是授权、数据和业务副作用边界。[第 16 章](https://github.com/aliyun/ai-agent-handbook/blob/ce08fbc496fadf4066c4e1036c418826e6ae2c99/04-governance/%E7%AC%AC%2016%20%E7%AB%A0%E3%80%80Agent%20%E8%A1%8C%E4%B8%BA%E7%94%9F%E6%88%90%E4%B8%8E%E8%B4%A8%E9%87%8F%E9%AA%8C%E8%AF%81.md)
- 浏览器练习把退款超时、恢复、记忆和效率等问题化为可执行的任务。抽查的退款题用 Sval 解释玩家 JavaScript，并暴露约定 hooks；测试文件另比较解释器与原生执行结果。它是限定规则下的教学环境。[退款题 sandbox](https://github.com/aliyun/ai-agent-handbook/blob/ce08fbc496fadf4066c4e1036c418826e6ae2c99/challenges/01-refund-timeout/sandbox.js)、[配套测试](https://github.com/aliyun/ai-agent-handbook/blob/ce08fbc496fadf4066c4e1036c418826e6ae2c99/challenges/01-refund-timeout/tests/run-tests.mjs)

## 价值

把“能调用工具”延伸到任务恢复、权限、成本和质量验证，适合转为团队设计评审与实验清单。尤其值得使用的是“记录与判断分层”及黄金集逐题比较的方法，而不是把厂商案例或平均分直接当成自己的生产结果。

## 风险边界

- **调研不是总体普查**：报告自述在线下开发者沙龙回收 **1,906 份有效问卷**，其中生产部署为 18%、人工抽查评估为 55%、轨迹自动评估为 6%。这些是该样本的自报统计；正文未给出随机抽样框、完整题级分母、权重与原始数据，不能外推为所有企业的采用率，也不能由相关关系推出工程投入的因果收益。[调研正文](https://github.com/aliyun/ai-agent-handbook/blob/ce08fbc496fadf4066c4e1036c418826e6ae2c99/2026-agent-survey-report.md)
- **案例有产品语境**：章节会使用 AgentScope、QwenPaw、AgentCore、AgentLoop 等具体产品说明方法；抽象原则与该产品当时的界面、价格、权限和可用性分别核实。厂商维护不等于结论无价值，也不等于独立对照评测。
- **教学过关不等于生产正确**：退款题有明确工具、时钟、状态和判分条件；不代表真实支付系统的幂等、长延迟、外部副作用与合规已经验证。浏览器解释器也不能当作任意不可信代码的系统安全证明。
- **黄金集需冻结与人工复核**：第 21 章说明当前控制台的历史版本用于查看，发起实验回到最新数据；可建立独立黄金集，在比较期间停止追加和修改。参考答案、rubric、来源版本和关键失败应逐题核对，不能仅看均分。[第 21 章](https://github.com/aliyun/ai-agent-handbook/blob/ce08fbc496fadf4066c4e1036c418826e6ae2c99/05-optimization/%E7%AC%AC%2021%20%E7%AB%A0%E3%80%80Agent%20%E9%BB%84%E9%87%91%E6%95%B0%E6%8D%AE%E9%9B%86.md)
- **文档与云操作分开**：本地书站不需要因此连接生产账户；章节内云资源、模型和第三方服务可能收费并产生真实写入。仓库 Apache-2.0 不自动覆盖外部服务与所有引用材料。

## 补充建议

选择一个重复任务，把书中方法落实为一页契约：输入和权限、完成证据、超时恢复、最大费用、人工接管点。固定一版脱敏黄金集，以当前实现为基线，分别记录成功、失败、未完成、质量、延迟和成本，再做变更实验。对调研数字保留样本来源；对案例只采用已经在本地条件下验证的部分。

## 参考资料

- [官方 JavaScript daily](https://github.com/trending/javascript?since=daily)、[仓库 API](https://api.github.com/repos/aliyun/ai-agent-handbook)、[在线书站](https://aliyun.github.io/ai-agent-handbook/)。
- [固定 Apache-2.0 许可](https://github.com/aliyun/ai-agent-handbook/blob/ce08fbc496fadf4066c4e1036c418826e6ae2c99/LICENSE)。
- 章节、调查、脚本和退款练习的固定 SHA 链接见各段；未完整审校全书、运行其测试、答题、调用云服务或验证业务收益。
