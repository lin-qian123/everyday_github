<!-- markdownlint-disable MD013 -->

# DesktopCommanderMCP

## 定位

Desktop Commander 将文件读写、搜索、定点编辑和长任务进程控制暴露给 MCP 客户端；它是受信 AI 客户端操作主机的工具层，权限来自运行它的账户。Remote MCP 则另加托管转发服务和本机 Remote Device。[固定 README](https://github.com/wonderwhy-er/DesktopCommanderMCP/blob/9a101b17e44577f0baefa4c7120f087881c5cc56/README.md)、[安全模型](https://github.com/wonderwhy-er/DesktopCommanderMCP/blob/9a101b17e44577f0baefa4c7120f087881c5cc56/SECURITY.md)

- 上游：[wonderwhy-er/DesktopCommanderMCP](https://github.com/wonderwhy-er/DesktopCommanderMCP)，仓库 ID `898345892`。
- 2026-11-23（Asia/Shanghai）07 时段：官方 JavaScript daily **+12**；API stars / forks / open issues（含 PR）**10,398 / 1,306 / 356**。[API](https://api.github.com/repos/wonderwhy-er/DesktopCommanderMCP)
- 最新核到非预发行版 [v0.3.4](https://github.com/wonderwhy-er/DesktopCommanderMCP/releases/tag/v0.3.4)，UTC 2026-11-18；固定主干 `9a101b17e44577f0baefa4c7120f087881c5cc56`，包元数据同为 0.3.4。
- 分类：`Coding Agents 与终端助手`。本轮仅核资料及少量实现，未安装、接入 MCP、授权远程设备或执行主机任务。

## 用法

包元数据要求 **Node.js >=22.12.0**，npm 对应版本也如此；Remote 子目录指南仍写 Node 18+，两者存在漂移，部署按实际包要求核验。[package.json](https://github.com/wonderwhy-er/DesktopCommanderMCP/blob/9a101b17e44577f0baefa4c7120f087881c5cc56/package.json)、[npm 版本元数据](https://registry.npmjs.org/@wonderwhy-er%2Fdesktop-commander/0.3.4)、[Remote 指南](https://github.com/wonderwhy-er/DesktopCommanderMCP/blob/9a101b17e44577f0baefa4c7120f087881c5cc56/src/remote-device/README.md)

支持 stdio 的客户端可参考以下固定版本配置；这只是待实施示例，本轮未写入任何客户端：

```json
{
  "mcpServers": {
    "desktop-commander": {
      "command": "npx",
      "args": ["-y", "@wonderwhy-er/desktop-commander@0.3.4"]
    }
  }
}
```

先用可丢弃目录核 `get_config`，再读文件、做一次可回滚替换；长命令通过 `start_process`、输出读取、交互和停止接口接续。固定版本应与实际启动配置一起确认：README 多种安装方式使用 `@latest`，并声明在客户端重启时自动更新；只给 setup 命令固定版本不必然固定以后启动的包。[安装与工具表](https://github.com/wonderwhy-er/DesktopCommanderMCP/blob/9a101b17e44577f0baefa4c7120f087881c5cc56/README.md)

远程方式还需账户、设备授权和持续运行的 Remote Device。首次配对会开浏览器，保存 `~/.desktop-commander-device/device.json`；本页只说明流程，不替用户授权。[Remote 指南](https://github.com/wonderwhy-er/DesktopCommanderMCP/blob/9a101b17e44577f0baefa4c7120f087881c5cc56/src/remote-device/README.md)

## 原理

MCP 请求被映射为本机文件、编辑和进程操作，长任务保留 session 与输出分页以减少单次上下文占用。配置管理器提供目录、命令、读写行数和 telemetry 设置；固定默认配置包含 `allowedDirectories: []`、`telemetryEnabled: true`。[配置实现](https://github.com/wonderwhy-er/DesktopCommanderMCP/blob/9a101b17e44577f0baefa4c7120f087881c5cc56/src/config-manager.ts)、[字段说明](https://github.com/wonderwhy-er/DesktopCommanderMCP/blob/9a101b17e44577f0baefa4c7120f087881c5cc56/src/config-field-definitions.ts)

Remote 路径为“AI 客户端 → Remote MCP 服务 → 本机 Remote Device → 本机 MCP server”，命令依然按本机用户身份执行。授权持久化、后端 endpoint 绑定和设备撤销属于另一控制面，不能从“本地执行”推断全程离线。[Remote 架构](https://github.com/wonderwhy-er/DesktopCommanderMCP/blob/9a101b17e44577f0baefa4c7120f087881c5cc56/src/remote-device/README.md)

## 价值

- 在同一会话中串联源码检查、表格 / 文档处理与进程管理，减少人工复制工具输出。
- 可观察并接续长命令；但工具返回、文件存在与内容正确应分别核验。
- 支持多类 MCP 客户端；本轮没有测跨客户端兼容性、任务成功率或相对 IDE 的效率，视频标题中的替代结论不作独立效果证据。

## 风险边界

- **护栏与隔离。** 上游明确：目录限制、命令黑名单和防 symlink 穿越不是抵御恶意客户端的 sandbox。终端可以访问目录白名单以外的文件；空目录列表默认允许整个文件系统的文件操作。若需要限制主机可达范围，需核实外部 VM / 容器权限、挂载、网络与宿主接口。[SECURITY](https://github.com/wonderwhy-er/DesktopCommanderMCP/blob/9a101b17e44577f0baefa4c7120f087881c5cc56/SECURITY.md)、[默认值](https://github.com/wonderwhy-er/DesktopCommanderMCP/blob/9a101b17e44577f0baefa4c7120f087881c5cc56/src/config-manager.ts)
- **注入与配置。** 安全模型假设客户端和 AI 账户可信，不判断请求来自用户还是提示注入；配置工具本身也能改限制。不能把一次确认或小范围目录设置当作持续授权边界。[安全模型](https://github.com/wonderwhy-er/DesktopCommanderMCP/blob/9a101b17e44577f0baefa4c7120f087881c5cc56/SECURITY.md)
- **三类数据出口。** 本地 tool history 会记录调用和参数；连接的模型可能接收文件及工具结果；默认开启的 telemetry 是第三条路径。隐私政策声明统计用途、不收文件内容 / 完整路径 / 命令参数，可设 `telemetryEnabled: false`；这是政策与配置证据，未做流量核验，也不能外推到 Remote 服务全部数据处理。[README](https://github.com/wonderwhy-er/DesktopCommanderMCP/blob/9a101b17e44577f0baefa4c7120f087881c5cc56/README.md)、[PRIVACY](https://github.com/wonderwhy-er/DesktopCommanderMCP/blob/9a101b17e44577f0baefa4c7120f087881c5cc56/PRIVACY.md)
- **远程会话生命周期。** Ctrl+C 只令设备离线，保留凭据与授权；`remote --logout`、服务端 revoke、客户端断开各有不同效果。POSIX 文件 0600 与 Windows 用户目录 ACL 也不同。默认持久会话及可信 endpoint 绑定须按部署版本确认。[Remote 指南](https://github.com/wonderwhy-er/DesktopCommanderMCP/blob/9a101b17e44577f0baefa4c7120f087881c5cc56/src/remote-device/README.md)
- **更新与修复。** [v0.3.3 说明](https://github.com/wonderwhy-er/DesktopCommanderMCP/releases/tag/v0.3.3)称修复 Remote MCP 认证漏洞；v0.3.4 增加 transport feature flags。这不证明所有远程场景已无漏洞，本轮没有复现漏洞、验证修复制品或审计托管服务。
- **许可。** 仓库代码 MIT，模型订阅、客户端、远程服务与第三方依赖分别适用各自条款。[LICENSE](https://github.com/wonderwhy-er/DesktopCommanderMCP/blob/9a101b17e44577f0baefa4c7120f087881c5cc56/LICENSE)

## 补充建议

固定包版本、客户端配置和目录，先验证读取、精确编辑、超时、停止和回滚；再按需要启用长任务或远程控制。对本地 history、模型输入、统计数据和设备凭据分别建立保留 / 撤销办法；把“工具已调用”与产物内容验收分开。

## 参考资料

- [固定 README](https://github.com/wonderwhy-er/DesktopCommanderMCP/blob/9a101b17e44577f0baefa4c7120f087881c5cc56/README.md)、[安全政策](https://github.com/wonderwhy-er/DesktopCommanderMCP/blob/9a101b17e44577f0baefa4c7120f087881c5cc56/SECURITY.md)、[隐私政策](https://github.com/wonderwhy-er/DesktopCommanderMCP/blob/9a101b17e44577f0baefa4c7120f087881c5cc56/PRIVACY.md)。
- [包元数据](https://github.com/wonderwhy-er/DesktopCommanderMCP/blob/9a101b17e44577f0baefa4c7120f087881c5cc56/package.json)、[默认配置实现](https://github.com/wonderwhy-er/DesktopCommanderMCP/blob/9a101b17e44577f0baefa4c7120f087881c5cc56/src/config-manager.ts)、[配置字段](https://github.com/wonderwhy-er/DesktopCommanderMCP/blob/9a101b17e44577f0baefa4c7120f087881c5cc56/src/config-field-definitions.ts)、[Remote MCP](https://github.com/wonderwhy-er/DesktopCommanderMCP/blob/9a101b17e44577f0baefa4c7120f087881c5cc56/src/remote-device/README.md)。
- [v0.3.4](https://github.com/wonderwhy-er/DesktopCommanderMCP/releases/tag/v0.3.4)、[v0.3.3 认证修复说明](https://github.com/wonderwhy-er/DesktopCommanderMCP/releases/tag/v0.3.3)。
