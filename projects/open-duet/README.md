<!-- markdownlint-disable MD013 -->

# Open Duet：带记忆、审批与可选电脑的 AI 同事工作区

- 上游：[Anil-matcha/open-duet](https://github.com/Anil-matcha/open-duet)；repository ID `645381450`。
- 更新：2026-11-05（Asia/Shanghai）；分类：Agent 框架与技能生态。
- 固定 main SHA：`601282f77d9d6566929d62572400daf88e0c230c`；API 6,771 stars / 868 forks / 8 open issues（含 PR）；Python daily +105。
- Apache-2.0；发行含 mobile-v0.3.0（UTC 2026-11-04）与 v0.8.1（UTC 2026-11-02），手机与主应用版本分开。
- 范围：API、完整树、固定 README、认证、审批与电脑文档静态核读；未启动桌面 / server、配对、连接服务或调用模型。

## 定位

为有名字、角色、记忆和工作目录的 AI agents 提供聊天、团队房间、任务、routine 与审批工作台。可用桌面源码、自托管 server 或单独运营的 Suparagent 托管服务；项目本身不包含模型或模型订阅。

## 用法

桌面源码路径需要 Node.js 22+、uv 和一个可用 engine；使用 CLI engine 时须先安装并登录：

```sh
git clone https://github.com/Anil-matcha/open-duet.git
cd open-duet
git checkout 601282f77d9d6566929d62572400daf88e0c230c
cd desktop
npm run app
```

首次选择 engine、独立 workspace 和 Ask first，再创建一个简单 agent。Docker 只在启用可选隔离电脑时需要。按固定认证文档，桌面入口除本地 launch token 之外还要求已验证应用账号；自托管 server 则为单 owner 的 passphrase / 配对体系，不能把两种身份流程互换。

## 原理

- 工作台把 engine、对话、笔记、workspace、任务与定时 routine 关联，团队 lead 协调其他 agent；当前 lead 要求 Claude 或 Codex。
- `ask` 默认等待 engine 要求的审批；`accept_edits` 放行 workspace 编辑；`approve_for_me` 由支持 engine 的原生安全审查处理；`plan` 对应计划模式。实现没有跳过所有权限的 full access 模式。
- 可选 Docker computer 挂载指定目录到 `/workspace`，默认网络 `none`，可改 bridge；容器调用仍经过审批，电脑不可用时文档规定不回退 host。
- 自托管请求先解析 owner / browser / device 身份，设备按 chat、files、manage、admin 分范围；Host / Origin 检查与默认关闭的 loopback trust 另成边界。
- 应用保存记忆、会话和配置；turn 会把问题、相关笔记与 engine 读取的文件传给所选 engine，远程模型按其服务条款处理。

## 价值

适合把重复任务、代理记忆和待审批动作集中到一个个人工作区，并保留人的处理入口。任务板和审批记录有助于追踪执行，但最终产物质量、engine 权限执行和外部结果仍需独立核验。

## 风险边界

- self-hosted 当前实验性、单 owner，不是多租户组织隔离方案；桌面本地 profile 不代表零外网依赖，账号校验缓存到期而服务不可用时按文档拒绝访问，CLI 凭据另存于 engine。
- 默认 host agent 使用真实 workspace。Docker、云电脑和 native macOS preview 是不同的 opt-in 路径；bind mount 中写入直接影响主机文件，容器存在不保证所有网络 / 凭据风险消失。
- `LOOPBACK_TRUST=programs` 会信任本机非浏览器进程，也可能让有 shell 的 agent 以 owner 操作设置或回答自己的审批；默认 `off` 应保留。
- mobile-v0.3.0 的 manage 配对可改 agents / rooms，但不等同 admin。局域网 HTTP 配对是 HTTPS 的例外路径，token 每次随请求发送，须评估链路与设备撤销。
- README 与 mobile 文档对“是否已在真 Android 手机验证”表述不一致；iOS、商店发行和推送仍未建立当前验收证据。不能把发行标签当全平台通过。
- 上游明确桌面安装器未签名且验证有限；Composio 连接应用仅有 fake service 测试，Marketplace、托管云电脑与音频转写等缺 live-service / packaged-app qualification。
- 托管计算、模型和第三方集成分别计费；演示视频的“Free / Unlimited / No Restrictions”是宣传标题，不代表模型调用免费、无限资源或免审批。

## 补充建议

先用非敏感文件和 Ask first，核对拒绝、超时、断线与重试。再分别验证 engine、电脑 provider、网络、workspace 写入与设备 scope；启用 routine 前确认失败可见、停止有效且不存在自我审批路径。

## 参考资料

- [README 与已知限制](https://github.com/Anil-matcha/open-duet/blob/601282f77d9d6566929d62572400daf88e0c230c/README.md)、[认证与桌面账号](https://github.com/Anil-matcha/open-duet/blob/601282f77d9d6566929d62572400daf88e0c230c/docs/AUTH.md)。
- [审批模式实现](https://github.com/Anil-matcha/open-duet/blob/601282f77d9d6566929d62572400daf88e0c230c/backend/app/services/approval_modes.py)、[可选电脑](https://github.com/Anil-matcha/open-duet/blob/601282f77d9d6566929d62572400daf88e0c230c/docs/COMPUTERS.md)、[手机说明](https://github.com/Anil-matcha/open-duet/blob/601282f77d9d6566929d62572400daf88e0c230c/docs/MOBILE.md)。
- [mobile-v0.3.0](https://github.com/Anil-matcha/open-duet/releases/tag/mobile-v0.3.0)、[v0.8.1](https://github.com/Anil-matcha/open-duet/releases/tag/v0.8.1)、[API](https://api.github.com/repos/Anil-matcha/open-duet)。
