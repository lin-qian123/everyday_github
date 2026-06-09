# Evolver

- GitHub: https://github.com/EvoMap/evolver
- 官网: https://evomap.ai
- 记录日期: 2026-04-17 (Asia/Shanghai)

## 这是什么

Evolver 是一个给 AI Agent 用的“自演化引擎”，核心目标不是直接改代码，而是把“临时 prompt 微调”变成可审计、可复用、可回滚的协议化资产。

它围绕 GEP（Genome Evolution Protocol）做了三件事：

1. 从 `memory/` 日志里抽取失败信号和模式。
2. 自动匹配 Gene/Capsule（演化策略资产）。
3. 生成严格约束的演化提示，并记录 EvolutionEvent 审计事件。

一句话：它更像“Agent 进化控制平面”，不是“自动改代码机器人”。

## 为什么今天值得关注

- GitHub Trending（2026-04-17）显示：`EvoMap/evolver` 当日新增约 `866 stars today`，总星约 `3.1k`。
- 热点方向与行业趋势一致：从“单次对话效果”转向“可持续演进 + 可治理 + 可追责”的 Agent 工程范式。
- 对团队场景有现实意义：日志驱动、协议约束、审计留痕，适合做组织级 Agent 规范化。

## 怎么用（最短路径）

## 1) 本地离线跑通

```bash
git clone https://github.com/EvoMap/evolver.git
cd evolver
npm install
node index.js
```

执行后会扫描 `memory/`，输出一条 GEP 约束演化提示（stdout）。

## 2) 人工审核模式

```bash
node index.js --review
```

适合你希望“先看建议，再决定是否执行下一步”的工作流。

## 3) 持续演化模式

```bash
node index.js --loop
```

适合做后台守护式演化循环（根据信号周期运行）。

## 4) 接入 EvoMap 网络（可选）

在 `.env` 增加：

```env
A2A_HUB_URL=https://evomap.ai
A2A_NODE_ID=your_node_id_here
```

不配也能离线工作；仅网络共享能力（skill sharing/leaderboard/worker pool）需要该配置。

## 原理拆解（工程视角）

## 1) 日志驱动的演化闭环

- 输入：`memory/` 与历史信号
- 选择器：`src/gep/selector.js` 进行 Gene/Capsule 匹配
- 输出：`src/gep/prompt.js` 生成协议约束提示
- 留痕：记录 EvolutionEvent，保证可审计

## 2) “生成建议”而非“直接改代码”

README 明确：Evolver 默认是 prompt generator，不自动改源码。
这让它在高风险代码库里更容易被采纳，因为变更仍可由人类或宿主系统把关。

## 3) 与宿主运行时的关系

在 OpenClaw 这类宿主中，stdout 里的 `sessions_spawn(...)` 文本可被解释为后续动作；
在独立模式下它只是文本输出，不会自动执行。

## 4) 可配置策略

`EVOLVE_STRATEGY=balanced|innovate|harden|repair-only`

- `balanced`：均衡
- `innovate`：探索新解
- `harden`：稳健强化
- `repair-only`：优先修复

## 安全模型（这个项目最关键）

README 的 Security Model 给了明确边界：

- 大部分核心模块只做读取/分析/文本生成。
- 只有 Gene 的 `validation` 命令会触发受控执行。
- 执行限制：
  - 仅允许 `node`/`npm`/`npx` 前缀
  - 禁止命令替换（反引号、`$()`）
  - 禁止管道与重定向等高风险 shell 操作符
  - 单命令 180 秒超时
  - 在仓库根目录受限执行

这意味着它尝试在“可自动验证”与“不放开任意命令执行”之间做平衡。

## 典型应用场景

1. Agent 项目经常重复出错，希望把修复经验沉淀成可复用 Gene。
2. 团队需要“谁改了什么演化策略、为什么改”的审计链。
3. 想把 Agent 行为治理从“凭经验调 prompt”升级到“协议化进化”。

## 风险与注意点

1. 协议成本：对小脚本或一次性项目可能偏重。
2. 信号质量依赖日志：日志脏、缺失、噪声大时，演化建议质量会下降。
3. 外部资产引入需审计：A2A 资产虽有验证闸门，仍需人工校验业务安全边界。
4. 自动 issue 上报要注意隐私：虽有脱敏逻辑，仍应二次检查合规要求。

## 我对它的判断

Evolver 值得关注的点不是“模型多强”，而是把 Agent 的演化过程产品化、制度化。对正在搭建团队级 AI 开发流的组织，这是比“再快一点生成代码”更长期的能力。

## 参考

- https://github.com/EvoMap/evolver
- https://github.com/trending
- https://evomap.ai
