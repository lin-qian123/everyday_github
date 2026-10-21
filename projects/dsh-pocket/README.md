<!-- markdownlint-disable MD013 -->

# DSH Pocket

> 更新：2026-10-22（Asia/Shanghai）。分类：前端、UI 与 Agent 交互层。主上游 `shaobeichen/dsh-pocket`；默认分支快照 `aee3ae7e9751`。官方资料与源码静态研究；热度、发行及社媒口径见[当日日报](../../daily/2026-10-22/ai-hotspots.md)。

## 定位

把电脑上的 DeepSeek Harness Web 通过局域网或 Cloudflare Tunnel 接到手机。手机可发任务、看流式输出和点审批，连接的是电脑上的同一宿主，并非手机端独立模型或只读监视器。[README.md](https://github.com/shaobeichen/dsh-pocket/blob/aee3ae7e97516206049394c7a37dc38778ffb6da/README.md)

## 用法

需要 Node.js `>=22` 和已经可用的 Harness。插件入口 `dsh plugin --profile web add dsh-pocket -w`，重启 `dsh web` 后到“设置 → 手机访问”扫码；先用局域网，公网访问另行启用。Desktop 的 compatibility 模式可用，README 标注 advanced 模式不支持。[README.md](https://github.com/shaobeichen/dsh-pocket/blob/aee3ae7e97516206049394c7a37dc38778ffb6da/README.md) [package.json](https://github.com/shaobeichen/dsh-pocket/blob/aee3ae7e97516206049394c7a37dc38778ffb6da/package.json)

局域网访问和局域网密码默认均开启；公网默认生成 8 位随机密码，每次开启换新，自定义固定密码后不再轮换。CLI 也默认生成 PIN，`--no-auth` 会取消认证；CLI 和插件设置的最小密码长度口径不同，不混写。[README.md](https://github.com/shaobeichen/dsh-pocket/blob/aee3ae7e97516206049394c7a37dc38778ffb6da/README.md) [lib/settings.mjs](https://github.com/shaobeichen/dsh-pocket/blob/aee3ae7e97516206049394c7a37dc38778ffb6da/lib/settings.mjs) [bin/dsh-pocket.mjs](https://github.com/shaobeichen/dsh-pocket/blob/aee3ae7e97516206049394c7a37dc38778ffb6da/bin/dsh-pocket.mjs)

## 原理

代理把入站 Host / Origin 等改为 loopback 权威，向 `127.0.0.1:3080` 转发 HTTP 与 WebSocket；移动端适配负责窄屏布局。公网由 cloudflared 建隧道，CLI 默认监听 `0.0.0.0`；因此代理自身的认证承担关键边界。[lib/proxy.mjs](https://github.com/shaobeichen/dsh-pocket/blob/aee3ae7e97516206049394c7a37dc38778ffb6da/lib/proxy.mjs) [bin/dsh-pocket.mjs](https://github.com/shaobeichen/dsh-pocket/blob/aee3ae7e97516206049394c7a37dc38778ffb6da/bin/dsh-pocket.mjs)

## 价值

工程判断：适合个人查看长任务与远程接续操作，复用现有会话和订阅。部署简单的收益来自复用宿主权限，也意味着手机会成为该权限的另一个入口。

## 风险边界

- QR 中可包含 `?token=`，应视同凭据；URL、终端输出、截图与分享链均需管理。代码使用 HttpOnly Cookie，sessionKey 随宿主进程变化；这不能替代设备或账号隔离。[bin/dsh-pocket.mjs](https://github.com/shaobeichen/dsh-pocket/blob/aee3ae7e97516206049394c7a37dc38778ffb6da/bin/dsh-pocket.mjs) [lib/proxy.mjs](https://github.com/shaobeichen/dsh-pocket/blob/aee3ae7e97516206049394c7a37dc38778ffb6da/lib/proxy.mjs)
- LAN 密码可关闭；陌生域名按公网认证的规则不等于已证明所有反向代理拓扑安全。本轮未做绕过、Host 混淆或公网渗透测试。[README.md](https://github.com/shaobeichen/dsh-pocket/blob/aee3ae7e97516206049394c7a37dc38778ffb6da/README.md) [lib/proxy.mjs](https://github.com/shaobeichen/dsh-pocket/blob/aee3ae7e97516206049394c7a37dc38778ffb6da/lib/proxy.mjs)
- 公网数据经过隧道服务；固定域名和自定义密码的轮换行为不同。自动下载 cloudflared 使用多个来源，安装前需核实际二进制来源。[README.md](https://github.com/shaobeichen/dsh-pocket/blob/aee3ae7e97516206049394c7a37dc38778ffb6da/README.md)
- 根许可为 GPL-2.0；README 图片的 alt 含旧 MIT 文案，不能拿它覆盖真实 LICENSE。移植的移动适配部分保留 MIT 版权声明。[LICENSE](https://github.com/shaobeichen/dsh-pocket/blob/aee3ae7e97516206049394c7a37dc38778ffb6da/LICENSE) [README.md](https://github.com/shaobeichen/dsh-pocket/blob/aee3ae7e97516206049394c7a37dc38778ffb6da/README.md)

## 补充建议

在可丢弃宿主分别验 LAN / 公网 / CLI：未登录拒绝、登录成功、改密码失效、宿主重启失效、关闭 LAN、HTTP 与 WS 行为一致。先用无敏感工作区和低权限账号，本轮未安装插件或开放端口。

## 参考资料

- [README.md](https://github.com/shaobeichen/dsh-pocket/blob/aee3ae7e97516206049394c7a37dc38778ffb6da/README.md)
- [LICENSE](https://github.com/shaobeichen/dsh-pocket/blob/aee3ae7e97516206049394c7a37dc38778ffb6da/LICENSE)
- [package.json](https://github.com/shaobeichen/dsh-pocket/blob/aee3ae7e97516206049394c7a37dc38778ffb6da/package.json)
- [lib/settings.mjs](https://github.com/shaobeichen/dsh-pocket/blob/aee3ae7e97516206049394c7a37dc38778ffb6da/lib/settings.mjs)
- [lib/proxy.mjs](https://github.com/shaobeichen/dsh-pocket/blob/aee3ae7e97516206049394c7a37dc38778ffb6da/lib/proxy.mjs)
- [bin/dsh-pocket.mjs](https://github.com/shaobeichen/dsh-pocket/blob/aee3ae7e97516206049394c7a37dc38778ffb6da/bin/dsh-pocket.mjs)
- [仓库 API](https://api.github.com/repos/shaobeichen/dsh-pocket)
- [v2.12.0 Release](https://github.com/shaobeichen/dsh-pocket/releases/tag/v2.12.0)
