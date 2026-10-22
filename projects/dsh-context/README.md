<!-- markdownlint-disable MD013 -->

# dsh-context

- 主上游：[bowenliang123/dsh-context](https://github.com/bowenliang123/dsh-context)
- 分类：记忆层与个人 AI 基础设施。
- 核验日期：2026-10-23（Asia/Shanghai）；主线快照 `16c5c0fb3a00`。
- [API](https://api.github.com/repos/bowenliang123/dsh-context) 快照：3,396 stars / 134 forks / 5 open issues；发行列表首项 [v0.74.0](https://github.com/bowenliang123/dsh-context/releases/tag/v0.74.0)（UTC 2026-10-21，正式）。累计值不代表今日增量。

## 定位

dsh-context 是 DeepSeek Harness 的上下文可视化插件，提供 Context Insights、会话 Context / Fleet 标签、侧栏和 `/context` 弹窗。它帮助定位工具 schema、技能注入、长工具输出与压缩事件的上下文占用，不是独立模型或自动压缩算法。[README](https://github.com/bowenliang123/dsh-context/blob/16c5c0fb3a00b41804af5c6e192ae457bbe7ea2f/README.md)

## 用法

已有 Harness 的用户可在 Add plugin 搜索 `dsh-context`；CLI 路径为：

```bash
dsh plugin --profile web add dsh-context
dsh web
```

随后打开会话 Context 或输入 `/context`，先比较当前组成、历史请求和 provider 实报。当前 manifest 为 0.74.0，Node 范围 `^22.19.0 || >=24.0.0`，Harness engines 声明及 README 兼容矩阵需与已安装版本一起核对。[manifest](https://github.com/bowenliang123/dsh-context/blob/16c5c0fb3a00b41804af5c6e192ae457bbe7ea2f/package.json)

## 原理

插件消费 Harness 官方 token-meter 投影与会话请求记录，按 system、tools、messages、注入与工具结果等类别汇总，关联压缩 / 裁剪事件和文件操作；Fleet 将父子会话与累计用量关联。上下文组成使用固定密度启发式，另展示 provider 报告的实际 prompt / output / cache 数字。旧于压缩的部分请求会从移除消息档案重建，并标注近似。[计量说明](https://github.com/bowenliang123/dsh-context/blob/16c5c0fb3a00b41804af5c6e192ae457bbe7ea2f/README.md)

## 价值

能把“上下文为何突然变大、缓存命中为何变化、哪个工具输出过长”转成逐请求可回查的问题。最直接的收益是辅助调试与解释成本构成；没有证据证明安装插件本身就能提高任务成功率或降低账单。

## 风险边界

- 分类估算、窗口占用、provider billed total 和估算费用是不同量；models.dev 标价、缓存和峰谷规则不等于账户实际结算。
- Context Browser 展示实际系统提示、工具参数、结果与附件；截图、导出和远程 Harness 访问应按其中的数据敏感度治理。
- 它不只读图表：配置支持全局系统提示 prefix / suffix，会影响全部会话及子 Agent 的后续步骤；两项默认空字符串。源码按 prompt section 注册并禁用模板插值，空白内容不注入。[配置](https://github.com/bowenliang123/dsh-context/blob/16c5c0fb3a00b41804af5c6e192ae457bbe7ea2f/src/host/config.ts)、[提示注入](https://github.com/bowenliang123/dsh-context/blob/16c5c0fb3a00b41804af5c6e192ae457bbe7ea2f/src/host/promptInjection.ts)
- 历史保存有界，例如默认最多 1,500 request steps、300 kept turns、400 events；不能把插件显示当成无限期完整审计档案。[默认上限](https://github.com/bowenliang123/dsh-context/blob/16c5c0fb3a00b41804af5c6e192ae457bbe7ea2f/src/host/config.ts)

## 补充建议

用合成会话对照一次工具调用、一次压缩和一个子会话，分别核实际请求计数、估算构成与 provider usage。费用应与账单独立核账；提示前后缀先留空，修改后保留版本记录。本轮未安装插件或读取用户 Harness 会话。

## 参考资料

- [README.md](https://github.com/bowenliang123/dsh-context/blob/16c5c0fb3a00b41804af5c6e192ae457bbe7ea2f/README.md)（固定 commit）。
- [package.json](https://github.com/bowenliang123/dsh-context/blob/16c5c0fb3a00b41804af5c6e192ae457bbe7ea2f/package.json)（固定 commit）。
- [src/host/config.ts](https://github.com/bowenliang123/dsh-context/blob/16c5c0fb3a00b41804af5c6e192ae457bbe7ea2f/src/host/config.ts)（固定 commit）。
- [src/host/promptInjection.ts](https://github.com/bowenliang123/dsh-context/blob/16c5c0fb3a00b41804af5c6e192ae457bbe7ea2f/src/host/promptInjection.ts)（固定 commit）。
- [正式发行列表](https://github.com/bowenliang123/dsh-context/releases)、[仓库 API](https://api.github.com/repos/bowenliang123/dsh-context)（动态状态）。
