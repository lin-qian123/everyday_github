# toolpermit

## 定位

ToolPermit 是本地 MCP client 与 `stdio` server 之间的权限策略、一次性审批和脱敏审计层。它用 YAML 实现可解释的 `allow / ask / deny`，并可离线 replay 已记录调用。

## 用法

```bash
python -m venv .venv
.venv/bin/python -m pip install "toolpermit==0.1.1"
.venv/bin/toolpermit init
.venv/bin/python examples/demo_client.py --mode observe --demo-dir demo-workspace
```

先在一次性 demo 目录以 observe 记录调用，再以 enforce 模式、CLI 或 loopback UI 对写操作做审批。

## 原理

首个匹配的 versioned YAML 规则做决定并解释原因；批准绑定 canonical request、policy、session 和过期时间且原子消费。识别出的 secret/敏感键会在 SQLite/JSONL 存储、展示、导出前不可逆替换，replay 不执行工具。

## 价值

将 MCP 调用的最小权限、人工闸门和审计从自然语言习惯变为可复现的策略。

## 风险边界

v0.1 只支持单本地用户、`stdio` 与 YAML policy v1；不是 OS sandbox、远程认证或绕过代理调用的拦截器，不能撤销已执行动作，也不保证消除所有 TOCTOU 风险。脱敏依赖识别模式，不能当作秘密绝不外泄的证明。

## 补充建议

先建立只读观察和 replay 基线，再逐步收紧默认拒绝；为删除、网络发送、生产数据库设独立人工批准，另行落实审计库加密、留存和清理。

## 参考资料

- [GitHub 仓库](https://github.com/sunhao123456sun-svg/toolpermit)
- [README：quickstart 与支持范围](https://github.com/sunhao123456sun-svg/toolpermit/blob/main/README.md)
- [安全模型](https://github.com/sunhao123456sun-svg/toolpermit/blob/main/docs/security.md)
