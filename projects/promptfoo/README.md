<!-- markdownlint-disable MD013 -->

# promptfoo

- 主上游：[promptfoo/promptfoo](https://github.com/promptfoo/promptfoo)
- 分类：模型、训练与推理基础设施。
- 核验日期：2026-10-24（Asia/Shanghai）；默认分支 `main` 快照 `c0b88a324175`。
- [API](https://api.github.com/repos/promptfoo/promptfoo) 快照：26,351 stars / 2,565 forks / 840 open issues；发行列表首项 [0.125.0](https://github.com/promptfoo/promptfoo/releases/tag/0.125.0)（UTC 2026-10-23，正式）。累计量不是今日增长，主线也不等于发行版。

## 定位

Promptfoo 是以配置文件组织 LLM、Agent 与 RAG 评测的 CLI / 库，也提供针对 AI 应用的红队测试。适合把提示词、模型和工具版本的变化变成可重复比较的回归任务。 [README.md](https://github.com/promptfoo/promptfoo/blob/c0b88a324175c60019cc80de1b2e32b4c849d4c3/README.md)

## 用法

先在独立目录安装并锁定版本，运行入门样例；主线 package 声明 Node.js `>=22.22.0`，选择正式包时再核相应 tag 的要求。下面命令来自上游入门流程，安装示例固定为本轮发行版本；执行评测可能调用收费模型，本轮未执行。

```sh
npm install -g promptfoo@0.125.0
promptfoo init --example getting-started
cd getting-started
promptfoo eval
promptfoo view
```

先使用合成测试数据，显式指定 provider、预算、断言与缓存策略，再接入 CI。 [README.md](https://github.com/promptfoo/promptfoo/blob/c0b88a324175c60019cc80de1b2e32b4c849d4c3/README.md)、[package.json](https://github.com/promptfoo/promptfoo/blob/c0b88a324175c60019cc80de1b2e32b4c849d4c3/package.json)

## 原理

由配置枚举 prompts、providers、tests 和 assertions，对模型输出作代码断言、相似度或模型裁判评分，再汇总比较矩阵。红队另有攻击生成、被测目标调用与评分三段数据流；目标评测由本地程序发起，不代表目标模型在本机运行。 [README.md](https://github.com/promptfoo/promptfoo/blob/c0b88a324175c60019cc80de1b2e32b4c849d4c3/README.md)、[site/docs/red-team/configuration.md](https://github.com/promptfoo/promptfoo/blob/c0b88a324175c60019cc80de1b2e32b4c849d4c3/site/docs/red-team/configuration.md)

## 价值

价值在于将“看起来更好”转换成有样本、有阈值和可追溯版本的比较，适合做提示词回归与安全用例持续测试。通过率只对选定数据集和评分器成立，不能换算成所有真实用户场景的可靠率。

## 风险边界

- README 的本地评测表述需要结合 provider 和红队生成配置理解。红队文档分别描述本地 key / API 代理与默认远程生成，Cloud 登录还会改变优先路径；应显式配置 provider，并按需要设置 `PROMPTFOO_DISABLE_REDTEAM_REMOTE_GENERATION=true`，再检查实际出口。关闭远程生成也不自动把云 provider 变成本地模型。 [site/docs/red-team/configuration.md](https://github.com/promptfoo/promptfoo/blob/c0b88a324175c60019cc80de1b2e32b4c849d4c3/site/docs/red-team/configuration.md)
- 默认收集使用遥测；配置中有账号信息时可含用户 ID、邮箱与登录状态。文档给出 `PROMPTFOO_DISABLE_TELEMETRY=1` 和独立的 `PROMPTFOO_DISABLE_UPDATE=1`。本轮主线代码在关闭遥测后仍有一次 “telemetry disabled” 事件进入发送函数的静态路径，因而不把该开关写成已验证完全断网；未实测网络行为。 [site/docs/configuration/telemetry.md](https://github.com/promptfoo/promptfoo/blob/c0b88a324175c60019cc80de1b2e32b4c849d4c3/site/docs/configuration/telemetry.md)、[src/telemetry.ts](https://github.com/promptfoo/promptfoo/blob/c0b88a324175c60019cc80de1b2e32b4c849d4c3/src/telemetry.ts)
- 模型裁判有偏好、随机性和额外费用；自定义 provider、断言与脚本也会执行代码。红队测试应限于授权的测试目标。根许可为 MIT。 [LICENSE](https://github.com/promptfoo/promptfoo/blob/c0b88a324175c60019cc80de1b2e32b4c849d4c3/LICENSE)

## 补充建议

先用小型人工金标集校准评分器，再固定独立保留集、模型版本、随机种子、重试、缓存和 token 成本。将误报、漏报与任务完成率分别报告；用 mock provider 核配置后再做低预算真实调用。本轮只读文档与部分实现，未运行扫描、发送评测数据或复现性能。

## 参考资料

- [README.md](https://github.com/promptfoo/promptfoo/blob/c0b88a324175c60019cc80de1b2e32b4c849d4c3/README.md)（固定 commit）。
- [package.json](https://github.com/promptfoo/promptfoo/blob/c0b88a324175c60019cc80de1b2e32b4c849d4c3/package.json)（固定 commit）。
- [site/docs/configuration/telemetry.md](https://github.com/promptfoo/promptfoo/blob/c0b88a324175c60019cc80de1b2e32b4c849d4c3/site/docs/configuration/telemetry.md)（固定 commit）。
- [site/docs/red-team/configuration.md](https://github.com/promptfoo/promptfoo/blob/c0b88a324175c60019cc80de1b2e32b4c849d4c3/site/docs/red-team/configuration.md)（固定 commit）。
- [src/telemetry.ts](https://github.com/promptfoo/promptfoo/blob/c0b88a324175c60019cc80de1b2e32b4c849d4c3/src/telemetry.ts)（固定 commit）。
- [LICENSE](https://github.com/promptfoo/promptfoo/blob/c0b88a324175c60019cc80de1b2e32b4c849d4c3/LICENSE)（固定 commit）。
- [发行列表](https://github.com/promptfoo/promptfoo/releases)、[仓库 API](https://api.github.com/repos/promptfoo/promptfoo)（动态状态）。
