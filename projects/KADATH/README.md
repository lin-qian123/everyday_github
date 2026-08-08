<!-- markdownlint-disable MD013 -->

# KADATH

- 仓库：[i3T4AN/KADATH](https://github.com/i3T4AN/KADATH)
- 快照：2026-08-09 抓取；GitHub API 显示其创建于 2026-08-08，约 145 stars、1 fork，Apache-2.0。数字会随时间变化。
- 分类：Agent 框架与技能生态

## 定位

一个以“进化”而非单次提示为核心的多 agent runtime。KADATH 为给定目标创建一组可变异的 agent 框架，在多个 epoch 中执行、独立评分、选择、保留或淘汰，从而寻找在明确基准上更优的方案。

## 用法

README 的入口是 `./kadath.sh`。首次启动会要求配置 OpenAI API key 和模型，并准备 Docker、PostgreSQL、MinIO、LiteLLM 与 SearXNG 等本地服务；随后在终端界面设置目标、epoch 时长、种群规模和代数。先审阅 Architect 生成的可测量 rubric，确认后才启动实验。

## 原理

它把不可变的 kernel 与可进化 organism 分离：kernel 锁定目标、运行时、评分公式、容器与证据边界；每个 organism 的系统提示、代码、工具声明和依赖可作为 genome 变异。执行期的 genome 只读，结束后由冻结证据驱动评分；内核校验引用并计算分数，防止 agent 自己改写基准或自报成绩。

## 价值

对可量化、可重复的复杂任务，这种种群搜索可比押注单一 agent/prompt 更系统地探索策略空间。版本化 genome、容器隔离、哈希锁定和证据冻结也为复跑、对比和事后审计提供了结构。

## 风险边界

高 stars 仍只是首日开发者信号。它会消耗大量模型 token，并引入 Docker、数据库、对象存储、搜索和可能的浏览器/网络能力；错误或被操纵的 benchmark 会把优化推向错误目标。作者的 live-verification 说明是仓库自述，不能替代本地安全、成本和性能验收。

## 补充建议

先在无敏感数据、无生产凭据的隔离主机上运行极小种群和短 epoch，并设账户级模型预算与出站网络 allowlist。把 benchmark、评分脚本和失败条件交给独立人员审阅；检查镜像固定、密钥权限、证据留存期限和删除流程，再考虑接入真实任务。

## 参考资料

- [项目 README](https://github.com/i3T4AN/KADATH)
- [系统架构与验证说明](https://github.com/i3T4AN/KADATH/tree/main/docs)
- [GitHub API 元数据快照](https://api.github.com/repos/i3T4AN/KADATH)
