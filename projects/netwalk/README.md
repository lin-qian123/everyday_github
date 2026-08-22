<!-- markdownlint-disable MD013 -->

# netwalk

> 上游仓库：[ripmilla/netwalk](https://github.com/ripmilla/netwalk) · 归类：Agent 框架与技能生态 · 本页基于 2026-08-23 的上游 README 与 GitHub API 快照整理。

## 定位

`netwalk` 是一个供 Claude Code 及其他 agent 使用的只读网络巡检工具包：从一台已获授权的入口设备开始，收集拓扑、配置与健康信息，输出 SVG 拓扑图和离线 HTML 报告。它将命令按厂商 allowlist 校验，并把凭据输入放在本机一次性浏览器表单中，目标是避免 agent 对话或工具调用直接取得密码。

API 快照：约 39 stars、8 forks、0 个开放 issue；创建于 2026-08-22；许可证 MIT。该项目属于早期开发者信号；README 的只读承诺、厂商适配和测试数量均为项目方材料，必须在授权实验环境独立审计。

## 用法

仅可在资产所有者书面授权的范围内安装和运行；先执行环境检查，再对实验网络的一台设备开始：

```sh
git clone https://github.com/ripmilla/netwalk
cd netwalk
python install.py --check
python install.py --agent codex

# 在已安装的 agent 中按项目说明启动；先限定扫描范围与授权人
/netwalk
```

上游说明 Python 3.9+、SSH key auth 或指定的密码认证依赖是基础条件。若需要把指导文件写入某个工程，`--agent codex` 会写入该工程的 `AGENTS.md`；在已有项目中必须先审阅 diff，避免把第三方规则无意并入团队指令。

## 原理

- 运行器在执行前按厂商的只读命令 allowlist 拒绝配置写入、重启、重定向、命令分隔符等内容；地址扫描还要求范围预先按站点与授权人登记。
- 凭据通过绑定 `127.0.0.1`、随机 token 的本机表单提交到权限受限文件；agent 只取得路径。报告生成器会检查并拒绝含凭据材料的记录。
- workflow 迭代执行登录、邻居发现与诊断，利用 LLDP/CDP、ARP、路由表等信息补全拓扑；经过授权的范围可做 TCP connect sweep，最后生成带证据的地图和报告。

## 价值

- 将 agent 的“只读”要求落实到命令策略和测试，而不是只靠提示词，便于把巡检范围、证据和拒绝行为纳入审查。
- 把拓扑、健康、配置检查和报告组织成可交接产物，减少人工巡检中口头传递或漏记证据的风险。
- 明确将凭据从会话文本隔离，有助于降低 agent transcript、日志或提示注入直接泄露密码的概率。

## 风险边界

- “只读”不等于无风险：配置导出可能含密钥、访问令牌、拓扑和业务信息；扫描、SSH 连接及 TCP 探测仍会产生网络流量、告警或合规影响。
- allowlist 与解析代码可能存在遗漏或厂商差异，不能替代变更窗口、网络分段、跳板机、最小权限账户或人工网络工程师复核。
- 范围扫描尤其需要书面授权；绝不可用它探测公共地址、第三方环境、生产网段外资产或规避访问控制。
- 本机表单、报告文件、日志和临时配置本身都属于敏感资产。文件权限、终端记录、备份、共享目录和浏览器扩展必须纳入治理。

## 补充建议

1. 先在隔离 lab 用只读测试账号验证每个厂商命令、拒绝路径和报告脱敏；保留完整命令日志以供网络管理员复核。
2. 把授权范围、允许时间窗、联系人、出口 IP、扫描速率和停止条件写入变更单，且让工具配置与该记录一致。
3. 在容器/跳板机中运行，严格控制 SSH key、已导出配置与报告的访问权限、保留期和加密备份。
4. 对报告中的“未发现”保留覆盖边界：未响应 UDP、静默主机、未支持设备和未获授权的网段都不应被表述为安全或不存在。

## 参考资料

- [上游 README / 只读策略与安装说明](https://github.com/ripmilla/netwalk)
- [GitHub API 元数据](https://api.github.com/repos/ripmilla/netwalk)
- [NIST SP 800-115：信息安全测试技术指南](https://csrc.nist.gov/pubs/sp/800/115/final)
- [OWASP：网络服务测试](https://owasp.org/www-project-web-security-testing-guide/)
