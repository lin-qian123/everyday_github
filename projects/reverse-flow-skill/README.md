# reverse-flow-skill

<!-- markdownlint-disable MD013 -->

## 定位

`reverse-flow-skill` 是一个面向 AI Agent / Codex 的本地 CTF 逆向工程流程 skill。它把样本分诊、工具链检查、静态分析、深度逆向、漏洞研判和报告输出组织成固定流程，默认面向本地沙盒、CTF、crackme、wargame、训练靶场和授权离线样本。

截至 2026-07-11，GitHub API 显示该仓库约 490 stars，创建于 2026-06-30，许可证为 MIT。它属于近期“专用安全/逆向 skill”热潮的一部分，和 `security-audit-skill`、`SkillSpector`、`VulnClaw`、`T3MP3ST` 一起说明 agent 能力正在向更专业的安全流程拆分。

## 用法

README 中定义的触发词是：

```text
真心为你
```

典型使用方式：

```text
使用 $reverse-flow 分析这个样本。真心为你
```

仓库给出的示例脚本包括：

```powershell
python ".\skills\reverse-flow\scripts\create_case.py" --case-name sample-audit --goal "local CTF reverse analysis" --out ".\work"
python ".\skills\reverse-flow\scripts\triage_artifact.py" ".\sample.bin" --out ".\work\sample-audit\triage"
python ".\skills\reverse-flow\scripts\tool_audit.py" --profile native --out ".\work\sample-audit\tools\native-tool-audit.md"
python ".\skills\reverse-flow\scripts\report_from_triage.py" ".\work\sample-audit\triage\*.json" --out ".\work\sample-audit\reports\initial-report.md"
```

## 原理

项目采用“英文内核提示词 + 中文用户交互”的设计：内部流程、工具选择和约束用英文写，以提高模型执行稳定性；启动词、报告和下一步菜单默认中文，方便中文用户操作。

工作流是“分析 -> 报告 -> 逆向 -> 深度逆向 -> 漏洞研判 -> 用户选择下一步”。对于“解锁”“绕过反调试”“拿 flag”等口语化需求，skill 会先归一化为本地样本分析、校验逻辑恢复、patch 思路或调试配置，而不是直接扩展到现实目标。

## 价值

- 把逆向任务拆成稳定步骤，降低 agent 在复杂二进制任务中跳步的概率。
- 强制保留工具审计、triage JSON 和报告路径，便于复盘。
- 对中文 CTF / crackme 用户友好，不需要每轮重复声明上下文。
- MIT 许可证便于学习、改造和团队内安全训练使用。

## 风险边界

- 只能用于本地、授权、CTF 或训练靶场；不能用于未授权系统、恶意软件投放或真实绕过访问控制。
- 自动化逆向可能误判样本行为，关键结论需要人工复核。
- README 顶部含有接单频道宣传，工程团队引入时应先审查 skill 内容、脚本和依赖。
- 逆向工具链可能执行未知样本，必须使用隔离目录、虚拟机或容器。

## 补充建议

- 与 `T3MP3ST` 区分：本项目偏本地逆向流程，`T3MP3ST` 偏授权红队 meta-harness。
- 与 `security-audit-skill` 区分：本项目处理二进制/样本分析，后者偏代码审计。
- 建议后续观察是否补充 Ghidra、radare2、Binary Ninja、APK、固件等 profile 的可复现实例。

## 参考资料

- GitHub 仓库：<https://github.com/lingbol088-spec/reverse-flow-skill>
- MIT License：<https://github.com/lingbol088-spec/reverse-flow-skill/blob/main/LICENSE>
- Cloudflare security-audit-skill：<https://github.com/cloudflare/security-audit-skill>
- T3MP3ST：<https://github.com/elder-plinius/T3MP3ST>
