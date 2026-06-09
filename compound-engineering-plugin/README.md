# compound-engineering-plugin（EveryInc/compound-engineering-plugin）

- GitHub: https://github.com/EveryInc/compound-engineering-plugin
- 更新日期: 2026-05-31（Asia/Shanghai）

## 定位

`compound-engineering-plugin` 是面向多种 AI 编码助手的统一插件层，目标是把一套工程化能力复用到 Claude Code、Codex、Cursor、Copilot 等不同运行环境。

## 用法

### 1) Copilot CLI 安装（仓库示例）

```bash
copilot plugin marketplace add EveryInc/compound-engineering-plugin
copilot plugin install compound-engineering@compound-engineering-plugin
```

### 2) Qwen Code 安装（仓库示例）

```bash
qwen extensions install EveryInc/compound-engineering-plugin:compound-engineering
```

### 3) 多目标安装（仓库示例）

```bash
bunx @every-env/compound-plugin install compound-engineering --to codex
bunx @every-env/compound-plugin install compound-engineering --to opencode
```

## 原理（工程视角）

1. 统一分发：通过兼容层把同一插件能力映射到多客户端。
2. 标准化流程：规范安装、清理、升级、迁移动作，减少环境差异。
3. 生态复用：将团队沉淀能力从“工具绑定”转向“协议绑定”。

## 价值

- 降低跨助手迁移成本。
- 便于团队统一最佳实践与操作规范。
- 适合需要多工具并行试验的 AI 工程团队。

## 风险边界

- 多版本矩阵可能引入兼容性回归。
- 插件执行链条增加供应链与权限风险。
- 各客户端能力不一致，可能导致行为偏差。

## 补充建议

1. 固定团队内“主版本 + 已验证客户端矩阵”。
2. 在核心工作流（规划、改码、测试）上做最小回归集。
3. 定期清理历史插件与缓存，避免残留冲突。

## 参考资料

- https://github.com/EveryInc/compound-engineering-plugin
- https://github.com/trending
