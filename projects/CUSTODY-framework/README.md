# CUSTODY-framework

- 仓库：[malwarejake/CUSTODY-framework](https://github.com/malwarejake/CUSTODY-framework)
- 快照：2026-08-04；创建于 2026-08-03，约 16 stars、1 fork，Apache-2.0；名称与商标使用另受仓库 TRADEMARK 说明约束。
- 分类：Agent 框架与技能生态

## 定位

面向组织内自治 agent 的供应商中立 containment 控制框架。它关注被授予权限与实际可达权限之间的“capability accretion”，把边界从 prompt 移到 agent 无法自行修改的基础设施。

## 用法

先按 Level / Mandate / Reach 三轴盘点 agent，再依赖顺序推进：机器可读的授权条件、隔离通用基础设施、能力上限、短期身份、停止开关、观测与拆除。它是控制目标框架，不是可直接安装的安全产品。

## 原理

框架用 CUSTODY 七支柱覆盖释放条件、不可信输入、监督/停止、临时授权、可观测性、处置和网络出口；通过等级、任务属性与可达性决定每项控制所需强度，并为多 agent 委派设定约束。

## 价值

它将“agent 有工具”改写为可盘点、可撤销、可审计的权限问题，尤其适合 CI/CD、SOC、数据管道和支持系统的架构评审。

## 风险边界

框架自身不实施 sandbox、身份、网络隔离或 SOC 流程，落地质量取决于实际平台。其“稳定可实施”声明不是独立安全认证；附录控制矩阵仍在开发。不得把授权范围宽泛的工作站或 VPN 环境误当作低 reach。

## 补充建议

从一个现有 agent 的工具、凭据、网络和子 agent 路径开始做威胁建模，演练 kill switch、凭据轮换和故障拆除；采用前让安全、平台、法务和业务 owner 共审。

## 参考资料

- [项目 README](https://github.com/malwarejake/CUSTODY-framework)
- [GitHub API 元数据快照](https://api.github.com/repos/malwarejake/CUSTODY-framework)
