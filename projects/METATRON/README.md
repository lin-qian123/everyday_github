<!-- markdownlint-disable MD013 -->

# METATRON（sooryathejas/METATRON）

> 记录日期：2026-09-07（Asia/Shanghai）。本页依据上游 README、源码、Modelfile、LICENSE 与 GitHub REST API 做静态整理；本轮未安装侦察工具、未启动扫描、未下载模型，也未对任何网络目标执行测试。

## 定位

`METATRON` 是面向 Parrot OS 的本地 CLI 渗透测试助手，把 nmap、whois、whatweb、curl、dig、nikto 等侦察结果交给 Ollama 中的本地模型分析，并把扫描历史保存到 MariaDB。它只适用于教育、CTF/实验室或具有书面授权的安全测试。

2026-09-07 的 GitHub 官方 Python Trending 抓取显示约 `+73 stars today`；REST API 快照为 `3,962 stars / 792 forks / 18 open issues`。许可证为 MIT；没有 GitHub release，最新 push 停在 2026-04-11。

## 用法

上游要求安装 Python 依赖、系统级侦察工具、MariaDB 与 Ollama 模型，然后在两个终端分别运行模型和 CLI。下列命令只应在隔离靶场中使用：

```bash
git clone https://github.com/sooryathejas/METATRON.git
cd METATRON
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
ollama create metatron-qwen -f Modelfile
python metatron.py
```

不要对互联网域名、他人设备、生产网络或未写入授权范围的端口执行扫描。

## 原理

- **侦察工具编排**：用户选择目标和 nmap、WHOIS、Web/DNS/HTTP 检查，Python 进程收集输出。
- **本地模型分析**：通过 Ollama 使用项目定义的 `metatron-qwen`，对工具结果生成漏洞、利用和修复建议。
- **Agentic loop**：模型可以请求更多工具调用，形成分析—补充侦察循环。
- **CVE/网页入口**：README 声称可用 DuckDuckGo 搜索和 CVE lookup 补充上下文。
- **MariaDB 历史**：扫描、结果和分析被写入关联表，可在 CLI 查看、修改或删除。
- **本地优先边界**：核心模型不要求云 API，但 Web 搜索、目标扫描、系统包下载仍会联网。

## 价值

- 把原始侦察输出与解释层放在同一 CLI，适合教学工具链与报告流程。
- 本地模型减少把漏洞数据直接发送给商业 LLM provider 的必要性。
- 明确列出系统工具和数据库 schema，便于静态审计与替换组件。
- MIT 许可降低学习和改造门槛，但不改变扫描授权与数据保护义务。

## 风险边界

- 未经授权的扫描或利用可能违法、触发告警或造成中断；README disclaimer 不能替代书面 scope、时间窗和联系人。
- Agentic loop 允许模型扩大工具调用；必须在网络、命令、速率、目标和凭据层做确定性限制。
- 项目使用标为 `abliterated` 的模型变体；更少拒绝不代表更准确，反而可能降低安全闸门。
- LLM 的漏洞判断、CVE 映射和修复建议可能幻觉或过时，不能替代版本核对、手工复现和专业审核。
- “100% offline”只适用于所选模型推理的上游描述；DuckDuckGo/CVE lookup、扫描目标和安装过程并非离线。
- MariaDB 会集中保存目标、服务、漏洞和分析，数据库权限、日志、备份与删除需要按敏感安全数据治理。

## 补充建议

- 仅在专用靶场、CTF 或复制的测试资产上使用，授权文件明确 IP/CIDR、域名、端口、时间和禁止动作。
- 容器/VM 中运行并用 egress allowlist、速率限制、只读工具 wrapper 与 command audit 阻止越界。
- 把模型输出标记为 hypothesis；CVE 必须核对产品、版本、可达路径和官方公告，再决定是否验证。
- 数据库使用独立低权限账号与加密磁盘，设置短保留期，并从报告中删除凭据、cookie 和个人信息。
- 在启用 agentic loop 前用 mock tool 测试目标继承、参数注入、超时、取消和重复扫描行为。

## 参考资料

- [GitHub 仓库](https://github.com/sooryathejas/METATRON)
- [GitHub REST API](https://api.github.com/repos/sooryathejas/METATRON)
- [README](https://github.com/sooryathejas/METATRON/blob/main/README.md)
- [工具执行源码](https://github.com/sooryathejas/METATRON/blob/main/tools.py)
- [Modelfile](https://github.com/sooryathejas/METATRON/blob/main/Modelfile)
- [MIT License](https://github.com/sooryathejas/METATRON/blob/main/LICENSE)
