<!-- markdownlint-disable MD013 -->

# app-store-compliance

## 定位

面向 iOS / Android 发布的规则手册、静态 guard 与 Coding Agent 技能，把源码问题、商店后台动作和地区规则分开记录。适合在提交前检查权限声明、隐私清单、原生配置及人工待办；不提供商店通过保证，也不是法律意见。

- 上游：[mjmirza/app-store-compliance](https://github.com/mjmirza/app-store-compliance)，仓库 ID `1261204838`。
- 2026-11-19 07 时段：官方 Shell daily **+596**；API 快照 stars / forks / open issues（含 PR）为 **1,364 / 105 / 27**。[API](https://api.github.com/repos/mjmirza/app-store-compliance)
- 最新核到的非预发行版：[v2.4.0](https://github.com/mjmirza/app-store-compliance/releases/tag/v2.4.0)，UTC 2026-11-15；本页静态依据 main `d2156bab9d7189835631c0a99adcc2479d32138d`，不将主线与发行制品混同。
- 分类：`Agent 框架与技能生态`。2026-11-19 首次建档，不代表今天首发。

## 用法

先做一次手动扫描，理解输出后再接入宿主 hook；以下仅为使用示例，本轮没有安装或扫描用户项目。

```bash
git clone https://github.com/mjmirza/app-store-compliance.git
cd app-store-compliance
git checkout d2156bab9d7189835631c0a99adcc2479d32138d
bash agent-os/hooks/app-store-compliance-guard.sh "/path/to/your/app"
```

需要 git、bash；部分辅助功能及非 Claude 宿主安装器依赖可调用的 `python3`。本页运行 Python 脚本统一写 `python`，使用前须确认它指向合适解释器。不要据此推断上游脚本内部也已改名。

读 `Coverage.`、findings 和最后一行：`BLOCKED` 表示检出 critical；`CLEAR` 只表示代码扫描未检出 critical；`NOT CHECKED` 表示相关检查未完成。多应用用 `python scripts/fleet-sweep.py fleet.json --json fleet-result.json --scanning-export fleet.sarif`，先按模板声明每个 app 的平台、地区、功能与人工 readiness。[README](https://github.com/mjmirza/app-store-compliance/blob/d2156bab9d7189835631c0a99adcc2479d32138d/README.md)、[Fleet Sweep](https://github.com/mjmirza/app-store-compliance/blob/d2156bab9d7189835631c0a99adcc2479d32138d/docs/FLEET-SWEEP.md)

## 原理

1. **资料层**：拒审模式、期限与检测规则放在结构化数据和引用文档中，技能根据 app 类型选读材料。
2. **扫描层**：shell guard 识别提交命令和项目结构，静态扫描配置 / 源码并输出严重级别、覆盖和建议；不能证明运行时数据流。
3. **汇总层**：Fleet Sweep 对所有 app 取最差结论；`READY / READY_WITH_ACTIONS / NOT_CHECKED / BLOCKED` 的退出码依次为 `0 / 3 / 1 / 2`。超时、覆盖不全或报告不一致不能作为 ready。
4. **人工证据层**：Ruling Register 区分生效规则、未来规则、提案与指导；按文档，仅已核来源且当期生效的适用要求参与阻断。需要人工证明的内容仍由责任人提交 attestation，扫描本身不能代签。

豁免按 app、finding、严重级别和文件精确匹配，须有审核人、理由、证据及不超过 180 天的有效期；它不能把未扫描完成变成通过。[guard 源码](https://github.com/mjmirza/app-store-compliance/blob/d2156bab9d7189835631c0a99adcc2479d32138d/agent-os/hooks/app-store-compliance-guard.sh)、[汇总代码](https://github.com/mjmirza/app-store-compliance/blob/d2156bab9d7189835631c0a99adcc2479d32138d/scripts/fleet-sweep.py)、[规则登记设计](https://github.com/mjmirza/app-store-compliance/blob/d2156bab9d7189835631c0a99adcc2479d32138d/docs/RULING-REGISTER.md)

## 价值

- 将“项目有没有扫描”“有没有 critical”“后台和真机事项是否完成”转成不同结论，便于 CI 和负责人接续。
- 用 SARIF / JSON 保存具体 finding 与豁免证据，比一个通过徽章更有利于追踪版本变化。
- 对 Agent 生成的移动端项目，补上发布配置与人工清单；收益仍须以自己的拒审、漏检和处理时间记录评价，不能从 stars 或上游自测轮数推出。

## 风险边界

- **放行不等于检查通过。** 固定源码中，hook 模式在临时缓冲失败、扫描失败或找不到原生项目等路径会报告 `NOT CHECKED` 并退出 0；直接执行的对应未检查路径通常退出 1。`APP_STORE_GUARD_OK=1` 还可覆盖 critical 阻断。它是便利检查，不是对抗恶意 Agent 的不可绕过发布控制；正式 CI 应明确拒绝未知结果并核覆盖。
- **规则条目与扫描能力不同。** API 项目描述仍写 117 个模式 / 95 个期限；本轮解析固定 SHA 的 JSON 实际为 **123 个 patterns / 107 个 deadlines**，二者版本均写 2.4.0、updated 11-15。条目数不代表都有自动检测，更不代表所有法域规则已被本轮重新验证。[模式数据](https://github.com/mjmirza/app-store-compliance/blob/d2156bab9d7189835631c0a99adcc2479d32138d/data/rejection-patterns.json)、[期限数据](https://github.com/mjmirza/app-store-compliance/blob/d2156bab9d7189835631c0a99adcc2479d32138d/data/regulatory-deadlines.json)
- **安装有持久影响。** 安装器会复制 hook / skill 并修改所选宿主配置；`--tool all` 会遍历检测到的宿主。上游的 `Install verified` 是测试载荷被阻断的安装检查，不能证明真实商店、所有提交路径或宿主版本已验收。[安装器](https://github.com/mjmirza/app-store-compliance/blob/d2156bab9d7189835631c0a99adcc2479d32138d/scripts/install.sh)
- **许可须按当前版本核。** API 为 `NOASSERTION`，仓库当前声明整体采用 `LicenseRef-OpenRoots-ORA-2.3`，含规模相关收费、竞争性再包装及 AI 训练限制；不能当作 MIT / Apache 自由复用。仓库 LICENSE 是指针，本轮已访问并抽读其 canonical 文本，具体权利仍以对应发行的完整条款为准。[LICENSE](https://github.com/mjmirza/app-store-compliance/blob/d2156bab9d7189835631c0a99adcc2479d32138d/LICENSE)、[正式文本](https://openroots.org/licenses/ora/2.3/legalcode.txt)

## 补充建议

先用脱敏样例覆盖正常、critical、缺原生目录、超时和豁免过期五种情况，同时保存 Coverage 与退出码。CI 另外核真正的提交通道、账号协议、商店表单、真机权限及 SDK 实际数据流；地区规则的日期和适用性回到 Apple / Google 或主管机关当前原文确认。本轮仅核工具结构和上游证据，没有逐条法律复核或商店提交实验。

## 参考资料

- [固定版本技能流程](https://github.com/mjmirza/app-store-compliance/blob/d2156bab9d7189835631c0a99adcc2479d32138d/agent-os/skill/SKILL.md)
- [发行列表](https://github.com/mjmirza/app-store-compliance/releases)；本文各实现结论的固定 SHA 链接见相关段落。
