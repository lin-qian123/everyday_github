<!-- markdownlint-disable MD013 -->

# DSH-IM

> 更新：2026-10-22（Asia/Shanghai）。分类：Agent 框架与技能生态。主上游 `xmanrui/dsh-im`；默认分支快照 `7e91c247fa95`。官方资料与源码静态研究；热度、发行及社媒口径见[当日日报](../../daily/2026-10-22/ai-hotspots.md)。

## 定位

社区维护的 DeepSeek Harness 插件，把飞书、微信、钉钉、Slack、Telegram、Discord 等渠道接入同一本机 Agent，并支持多机器人、工作区及会话绑定。README 自述获官方 Token 赞助，同时明确为社区独立开发；赞助不等于官方产品身份或安全认证。[README.md](https://github.com/xmanrui/dsh-im/blob/7e91c247fa953b75eec74b030fdf4742aafc9f2e/README.md)

## 用法

Node.js 最低 `22.19`。Desktop / Web 应安装到对应 profile；准确包名为 `@xmanrui/dsh-im`，例如 Web 入口 `dsh plugin --profile web add -w @xmanrui/dsh-im`，随后重启宿主，在“设置 → IM机器人”按渠道配凭据。不能用名称相似的包替代。[README.md](https://github.com/xmanrui/dsh-im/blob/7e91c247fa953b75eec74b030fdf4742aafc9f2e/README.md) [package.json](https://github.com/xmanrui/dsh-im/blob/7e91c247fa953b75eec74b030fdf4742aafc9f2e/package.json)

先接一个专用测试机器人，核响应范围、工作区和工具权限，再扩大渠道。Telegram 默认 Compatible：私聊可响应、群聊需提及或回复；Safe mode 才强制私聊 User ID 白名单，空白名单拒绝全部输入。WhatsApp 默认 Only me，另有指定联系人和开放模式。[docs/access-modes.md](https://github.com/xmanrui/dsh-im/blob/7e91c247fa953b75eec74b030fdf4742aafc9f2e/docs/access-modes.md)

## 原理

渠道适配器接收平台消息，映射为 Harness 会话，再把流式状态、文字和附件回送原聊天；宿主执行工具，插件负责接入和路由。群记录另存 SQLite / 文件目录，模型按需调用查询或文件工具，不是每条保存都调用模型。[README.md](https://github.com/xmanrui/dsh-im/blob/7e91c247fa953b75eec74b030fdf4742aafc9f2e/README.md) [docs/group-history.md](https://github.com/xmanrui/dsh-im/blob/7e91c247fa953b75eec74b030fdf4742aafc9f2e/docs/group-history.md)

## 价值

工程判断：能复用已有 IM 入口做异步协作、进度查询与结果交付，减少反复切换客户端。价值取决于“谁可发任务、可读什么、可向谁回传”是否能在具体渠道配置和验收。

## 风险边界

- 六渠道的群记录采集默认开启，包含实际收到的未 @ 消息与附件，没有逐群开关；默认滚动保留 14 天。仅修改保留天数不会删除已经进入 AI 会话的副本，也不能用 `0` 关闭采集。平台没有投递的数据不会自动补齐。[docs/group-history.md](https://github.com/xmanrui/dsh-im/blob/7e91c247fa953b75eec74b030fdf4742aafc9f2e/docs/group-history.md)
- README 声明，支持回传的渠道可发送 Harness 能读取的已有文件，插件不额外限制来源、工作区、扩展名等；因此回传权限不能只靠“生成文件”这一口头约定。[README.md](https://github.com/xmanrui/dsh-im/blob/7e91c247fa953b75eec74b030fdf4742aafc9f2e/README.md)
- 扫码新建的飞书 / QQ 机器人默认允许所有用户聊天及执行内置命令；需主动配置白名单。Matrix 加密仍为实验功能，未实现完整设备验证和密钥备份，作者也未完成真实 homeserver / Element 互通验证。[README.md](https://github.com/xmanrui/dsh-im/blob/7e91c247fa953b75eec74b030fdf4742aafc9f2e/README.md)
- 工具运行、模型请求、平台消息和本地归档各有数据边界；MIT 代码许可不代表平台账号、通信内容或第三方依赖可任意使用。[LICENSE](https://github.com/xmanrui/dsh-im/blob/7e91c247fa953b75eec74b030fdf4742aafc9f2e/LICENSE) [README.md](https://github.com/xmanrui/dsh-im/blob/7e91c247fa953b75eec74b030fdf4742aafc9f2e/README.md)

## 补充建议

用合成群消息和随机字段测试“未 @ 保存 → 按权限查询 → 过期排除 → 副本保留”四步；用工作区内外两个无敏感文件检查回传范围。渠道验收需分别记录，不能把作者标注的 QQ / WhatsApp 实测外推为所有渠道已通过。本轮只读资料，未接账号或发消息。

## 参考资料

- [README.md](https://github.com/xmanrui/dsh-im/blob/7e91c247fa953b75eec74b030fdf4742aafc9f2e/README.md)
- [package.json](https://github.com/xmanrui/dsh-im/blob/7e91c247fa953b75eec74b030fdf4742aafc9f2e/package.json)
- [LICENSE](https://github.com/xmanrui/dsh-im/blob/7e91c247fa953b75eec74b030fdf4742aafc9f2e/LICENSE)
- [docs/access-modes.md](https://github.com/xmanrui/dsh-im/blob/7e91c247fa953b75eec74b030fdf4742aafc9f2e/docs/access-modes.md)
- [docs/group-history.md](https://github.com/xmanrui/dsh-im/blob/7e91c247fa953b75eec74b030fdf4742aafc9f2e/docs/group-history.md)
- [plugin-src/host/rpc-authority.mjs](https://github.com/xmanrui/dsh-im/blob/7e91c247fa953b75eec74b030fdf4742aafc9f2e/plugin-src/host/rpc-authority.mjs)
- [仓库 API](https://api.github.com/repos/xmanrui/dsh-im)
- [v5.4.0 Release](https://github.com/xmanrui/dsh-im/releases/tag/v5.4.0)
