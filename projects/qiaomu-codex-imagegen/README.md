<!-- markdownlint-disable MD013 -->

# 乔木 Codex ImageGen（joeseesun/qiaomu-codex-imagegen）

> 上游仓库：<https://github.com/joeseesun/qiaomu-codex-imagegen> · 归类：语音、视频与多模态 · 本页基于 2026-10-06 的 GitHub API、README、Skill / MCP / CLI 说明、设计资料、Release、manifest 与 LICENSE 静态整理，未调用 Codex image generation、处理参考图或复验 24 类模板样图。

- 抓取快照：94 stars、5 forks、0 open issues；仓库创建于 2026-10-04 08:47 UTC。
- 热度信号：GitHub Search 按新建仓库 stars 排序的早期开发者信号；不是 GitHub Trending 或社媒互动量。
- 版本与许可：MIT；GitHub Release / tag 与 manifest 均为 `v0.3.0` / `0.3.0`，要求 Node.js 18+ 与已登录且有生图权限的 Codex CLI。

## 定位

该项目把 Codex 内置 image generation 封装成 Agent Skill、stdio MCP server 与 CLI，并提供中文内容场景预设、24 类设计模板、风格库和验收条件，用于海报、视频封面、小红书卡片、文章插图、肖像、产品视觉与参考图编辑。

## 用法

可以用 `npx skills add joeseesun/qiaomu-codex-imagegen` 安装 skill，再把 `scripts/mcp-server.mjs` 注册给 MCP 客户端；也可直接运行 `node scripts/cli.mjs`。推荐先用 `suggest / compose / --show-prompt` 免费检查方向、变量和验收项，再用 `generate` 调用生图；`--ref` 接收绝对路径参考图，输出旁会保存 JSON metadata。

## 原理

工具启动独立的 `codex app-server --listen stdio://` JSON-RPC 会话，要求回合调用 image generation，监听完成事件后把 Codex 保存的图片复制到指定目录。Prompt 层把场景比例、安全区、模板变量、文字模式、风格关系与失败条件组合起来；生成会话只允许写输出目录，审批策略为 never，交互请求直接拒绝。

## 价值

它把“先列方向—再选模板—填变量—生成—按条件验收”做成可调用工具，避免只给一句风格词就直接耗额度。中文平台比例、短文案、透明通道检查和可追溯 JSON 对内容生产比单次聊天生图更易复用。

## 风险边界

- 每张图消耗用户 Codex / OpenAI 账号额度，`count` 并行会成倍消耗；本地 CLI 仍通过 Codex 服务处理 prompt 与参考图，不是离线生成。
- 参考图可能含肖像、客户素材和未公开产品；上传前必须获得授权并确认 provider 的保留、训练、地区与删除政策。
- 风格模板、Mondo 设计师名称与第三方提示词语料存在版权、商标和近似复刻风险；项目也明确 689 条原始参考提示词 / 图片没有开放授权，因此不随仓库分发。
- 沙箱只限制当前 app-server 会话写输出目录，不证明 Codex、Node、MCP host 或用户安装的其他能力受到完整 OS / 网络隔离。
- 图内中文、小字号、比例、透明通道与参考图身份仍可能失败；作者样图和 22 项离线测试不能替代逐张视觉 / 权利检查。
- 本轮未运行 `npm test`、核验账号权限、生成尺寸、provider 数据流或 Release 制品与源码一致性。

## 补充建议

先固定 `v0.3.0`，用无权利争议的合成图和 `--show-prompt` 验证模板，再以单张、低额度方式生成；记录输入哈希、prompt、模型 / provider、尺寸、metadata 与人工验收。商业交付不要直接使用设计师姓名做最终提示，参考图与输出分别做肖像、品牌、字体、素材和第三方语料审查。

## 参考资料

- [GitHub 仓库](https://github.com/joeseesun/qiaomu-codex-imagegen)
- [GitHub REST API](https://api.github.com/repos/joeseesun/qiaomu-codex-imagegen)
- [README 与使用示例](https://github.com/joeseesun/qiaomu-codex-imagegen/blob/main/README.md)
- [Agent Skill](https://github.com/joeseesun/qiaomu-codex-imagegen/blob/main/SKILL.md)
- [设计系统 Agent guide](https://github.com/joeseesun/qiaomu-codex-imagegen/blob/main/references/design-system/agent-guide.md)
- [Codex app-server 接入代码](https://github.com/joeseesun/qiaomu-codex-imagegen/blob/main/scripts/lib/codex.mjs)
- [`v0.3.0` Release](https://github.com/joeseesun/qiaomu-codex-imagegen/releases/tag/v0.3.0)
- [npm manifest](https://github.com/joeseesun/qiaomu-codex-imagegen/blob/main/package.json)
- [MIT LICENSE](https://github.com/joeseesun/qiaomu-codex-imagegen/blob/main/LICENSE)
