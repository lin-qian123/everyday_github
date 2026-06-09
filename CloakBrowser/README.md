# CloakBrowser（CloakHQ/CloakBrowser）

- GitHub: <https://github.com/CloakHQ/CloakBrowser>
- 核心定位：通过 Chromium 源码级指纹修补实现“更难被风控识别”的自动化浏览器，主打 Playwright/Selenium 等生态的无缝接入。

## 1. 它解决什么问题

传统 stealth 方案常见问题：
- 依赖 JS 注入或启动参数，浏览器版本一变就容易失效；
- 自动化环境与本地环境表现不一致；
- 反爬系统会反向识别“伪装痕迹”。

`CloakBrowser` 的思路是把指纹修补下沉到浏览器二进制层，减少“补丁外露感”。

## 2. 快速使用（实践向）

```bash
git clone https://github.com/CloakHQ/CloakBrowser.git
cd CloakBrowser
# 按官方文档安装依赖并获取可执行文件
# 在 Playwright/Selenium 中替换浏览器启动路径或接入方式
```

落地建议：
- 先在测试目标站做 A/B 对照（普通浏览器 vs CloakBrowser）；
- 对关键抓取链路记录挑战率（验证码触发率、封禁率）；
- 与代理池和请求节流联动，避免把“浏览器伪装”当成唯一解。

## 3. 原理拆解（简化）

- 源码层指纹处理：在 Chromium C++ 层修改关键指纹输出路径；
- 运行环境一致性：减少“本地可过、容器失效”的配置漂移；
- 框架兼容：对接 Playwright/Selenium/browser-use 等自动化框架。

## 4. 为什么值得关注

- AI Agent + Browser Automation 场景正在爆发，稳定访问能力成为基础设施；
- 源码级方案相对更抗版本抖动，适合长期运营型采集任务；
- 对增长、竞品情报、价格监控等业务有直接工程价值。

## 5. 风险与边界

- 合规风险：必须遵守目标站 ToS、robots 与数据法规；
- 伦理风险：该能力可能被用于灰产爬取，需要明确用途边界；
- 技术风险：反爬策略持续演进，仍需持续迭代与监控。

## 6. 我的补充建议

- 建立“目标站画像”分层策略：普通站点用轻量方案，高防站点才启用高成本能力；
- 增加失败归因维度（IP、TLS、行为轨迹、指纹）而非只看是否过验证；
- 对每次浏览器升级做回归基准，避免 stealth 回退无人感知。

## 7. 参考资料

- 官方仓库：<https://github.com/CloakHQ/CloakBrowser>
- GitHub Trending：<https://github.com/trending>
- Trendshift：<https://trendshift.io/>
