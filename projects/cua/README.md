# cua（trycua/cua）

- GitHub: https://github.com/trycua/cua
- 官网: https://cua.ai
- 记录日期: 2026-06-16 (Asia/Shanghai)

## 定位

`cua` 是一套面向 computer-use agent 的开源基础设施，核心想法不是只做一个“会点鼠标的模型”，而是把沙箱、桌面驱动、基准测试和 macOS 虚拟化打成一条完整工具链。

## 热度信号

1. GitHub 仓库页在 2026-06-16 抓取时约有 `18.1k stars`、`1.2k forks`。
2. GitHub Trending 当日页面把它列为热门项目之一，说明“让 agent 真正操作桌面”这条路线仍在升温。
3. 仓库最近发布记录显示最新 release 为 `cua-computer-server v0.3.41`，发布时间为 `2026-06-15`，迭代节奏很快。

## 用法

### 1) 先装桌面驱动

macOS / Linux：

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/trycua/cua/main/libs/cua-driver/scripts/install.sh)"
```

Windows：

```powershell
irm https://raw.githubusercontent.com/trycua/cua/main/libs/cua-driver/scripts/install.ps1 | iex
```

### 2) 作为 MCP 接到 agent

```bash
claude mcp add --transport stdio cua-driver -- cua-driver mcp
```

这类配置思路同样适合接到 Codex、Cursor 或自定义 agent 客户端。

### 3) 直接用沙箱 SDK

```bash
pip install cua
```

```python
from cua import Sandbox, Image

async with Sandbox.ephemeral(Image.macos()) as sb:
    await sb.keyboard.type("hello from cua")
    await sb.mouse.click(100, 200)
    screenshot = await sb.screenshot()
```

## 原理

1. `cua-driver` 负责真实桌面控制，强调后台运行，不强抢当前鼠标焦点。
2. `cua-sandbox` 提供统一抽象，让 Linux、macOS、Windows、Android 的沙箱与 VM 尽量走同一 API。
3. `cua-bench` 把评测和训练环境标准化，方便比较不同 computer-use agent 的效果。
4. `lume` 补上 Apple Silicon 上的 macOS / Linux 虚拟化能力，使本地实验与复现更可控。

## 价值

- 对做 GUI Agent、桌面自动化、浏览器外工作流自动化的团队很有吸引力。
- 比“单个 demo agent”更完整，因为它把运行环境、驱动层和 benchmark 一起提供了。
- 对研究者也有价值，尤其是需要评测 OSWorld、ScreenSpot 一类任务时。

## 风险边界

- computer-use agent 的权限半径天然比普通 API 工具更大，误点、误删、误发消息都更现实。
- 背景桌面控制虽然更顺手，但也更容易让人忽视执行中的高风险动作。
- 若引入第三方视觉模型或远程沙箱，还要额外审计数据出境、截图留存和访问控制。

## 补充建议

1. 在生产场景里默认把高风险动作放进审批闸门。
2. 优先区分“实验环境”和“真实工作环境”，不要混用同一账号与同一桌面。
3. 做基准时同时记录成功率、耗时和恢复能力，避免只盯单次演示效果。

## 参考资料

- https://github.com/trycua/cua
- https://cua.ai/docs
- https://github.com/trending
