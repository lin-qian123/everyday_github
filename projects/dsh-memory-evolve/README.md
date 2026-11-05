<!-- markdownlint-disable MD013 -->

# dsh-memory-evolve（csyangwen/dsh-memory-evolve）

- 更新：2026-11-06（Asia/Shanghai）；官方 JavaScript daily +32，为读取快照，不是自然日结算。
- GitHub API：628 stars / 70 forks / 37 open issues（含 PR）；仓库 ID `1323731026`。
- 核读基线：`44b6b3eb65a1d50ceba0afb2c13acdd4a8b81423`；文档与抽样实现核验，不是安装运行、安全或性能认证。

## 定位

DeepSeek Harness（DSH）的插件，为全局、用户、项目、Git 分支与每日记录组织长期记忆，并扩展技能、待办、会话搜索、外部 CLI 调度和评审面板。适合已使用 DSH、希望跨会话保留决策与经验的开发者；不是独立模型或通用零配置记忆服务。

## 用法

README 当前安装方式是 profile 级插件注册：

```bash
dsh plugin --profile web add github:csyangwen/dsh-memory-evolve
```

安装后重启 `dsh web`。包声明 bundle patch，会自动注册 host；旧版手动 insert 记录应先清除，重复同 id 会导致加载失败。异常时可按文档在 profile patch 以 id 设置 `disabled: true`，而非再插入一份。

回合内审查、记忆同步和 Advisor 默认关闭；`reviewMode` 默认 `suggest`。先固定宿主与插件版本，再从本地记忆开始；不要把 package 的 `0.1.0` 当真实发行序列，项目使用日期 / 语义 git tag，最新 Release 为 `v26092802`。本轮未安装或运行插件。

## 原理

插件在宿主挂载工具和 UI，对 Markdown / 日志 / 建议队列分轨读写、注入上下文；审查流程可提议记忆或写入全局记忆，Git 同步用项目身份分支协调多设备。Advisor 读取可见会话内容、调用独立模型并可投递提醒，外部 CLI 和 IM 通知则是另外的数据 / 执行出口。它们都建立在宿主 API 与权限之上，“纯插件”不意味着没有系统影响。

## 价值

把“记住什么、从哪里来、何时确认、在哪个项目生效”做成可检查资产，有助于减少重复解释。价值应由有来源的正确召回、错误记忆撤回、跨分支隔离和迁移恢复来检验；“越用越懂你 / 自我进化”是产品描述，不是已验证学习效果。

## 风险边界

- **确认不是所有写入的硬门**：README 强调 AI 提议、用户确认；源码的 `suggest` 是默认审查模式，但主会话的部分记忆写入不经过同一门控，`auto` 又允许直接写入全局记忆。子会话的全局写入有单独拒绝 / approval 分支。不能将提示词约定写成所有写入的强制审批保证。
- **同步可能公开**：同步模块与逐项目开关默认关闭；启用后未填共享仓库地址时使用主代码仓库的专属分支，代码仓库公开则记忆也公开。全局记忆另需共享仓库和独立轨开关，分支名并不提供保密。
- **额外模型与指令**：Advisor 默认关闭，文档强调完整可见上下文重放并把提醒作为用户指令注入；开启前应核模型出口、token 成本、来源标识与谁有权改变主会话行为。评审员只能看到部分证据，不能替代对工具结果的验证。
- **版本与清理**：9 月 Release 针对特定 DSH 预发行适配，main 已继续演进；README 的“卸载即净”不等同已删除远端 Git 分支、模型留存、外部消息或所有历史资产。根许可 MIT。

## 补充建议

用合成资料测试一次正确提议、错误提议拒绝、主 / 子会话写入差异、Git 分支切换、删除撤回和重复同步；开同步前显式检查远端可见性，优先独立私有记忆仓库。备份本地正本，记录哪些文件和外部副作用需要另行清理，再逐项开启 Advisor、外部 CLI 或通知。

## 参考资料

- [README.md](https://github.com/csyangwen/dsh-memory-evolve/blob/44b6b3eb65a1d50ceba0afb2c13acdd4a8b81423/README.md)
- [package.json](https://github.com/csyangwen/dsh-memory-evolve/blob/44b6b3eb65a1d50ceba0afb2c13acdd4a8b81423/package.json)
- [cordis.patch.yml](https://github.com/csyangwen/dsh-memory-evolve/blob/44b6b3eb65a1d50ceba0afb2c13acdd4a8b81423/cordis.patch.yml)
- [lib/index.js](https://github.com/csyangwen/dsh-memory-evolve/blob/44b6b3eb65a1d50ceba0afb2c13acdd4a8b81423/lib/index.js)
- [lib/review.js](https://github.com/csyangwen/dsh-memory-evolve/blob/44b6b3eb65a1d50ceba0afb2c13acdd4a8b81423/lib/review.js)
- [lib/advisor/runtime.js](https://github.com/csyangwen/dsh-memory-evolve/blob/44b6b3eb65a1d50ceba0afb2c13acdd4a8b81423/lib/advisor/runtime.js)
- [docs/记忆同步.md](https://github.com/csyangwen/dsh-memory-evolve/blob/44b6b3eb65a1d50ceba0afb2c13acdd4a8b81423/docs/记忆同步.md)
- [仓库与 API 快照](https://api.github.com/repos/csyangwen/dsh-memory-evolve)；[发行列表](https://github.com/csyangwen/dsh-memory-evolve/releases)。
