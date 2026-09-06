<!-- markdownlint-disable MD013 -->

# Konnect（mixelpixx/Konnect）

> 记录日期：2026-09-07（Asia/Shanghai）。本页依据上游 README、工具目录、roadmap、release、LICENSE 与 GitHub REST API 做静态整理；本轮未安装 KiCAD 插件、未打开 PCB、未运行 ERC/DRC，也未生成或制造任何电路板。

## 定位

`Konnect` 是 KiCAD 10 的 AI-assisted PCB design 插件与 MCP server，以单个 Rust 二进制把原理图、布局、布线、ERC/DRC、设计审查、零件搜索和制造文件导出暴露给 Claude 或其他 LLM。上游明确标记为 beta。

2026-09-07 的 GitHub 官方 Rust Trending 抓取显示约 `+31 stars today`；REST API 快照为 `469 stars / 74 forks / 63 open issues`，最新 release 为 `v0.11.0`，许可证为 AGPL-3.0，并提供商业许可路径。

## 用法

上游推荐从 release 下载对应平台的 KiCAD Plugin and Content Manager 包，在 KiCAD 10 中使用 “Install from File” 安装。源码构建入口为：

```bash
cargo build --release -p konnect
```

大多数 PCB 工具要求 KiCAD 打开目标 board 并启用 IPC API；正式试用应复制工程到独立目录、禁用自动制造下单，并把每个变更保留在可撤销/可 diff 的步骤中。

## 原理

- **原理图编辑**：直接操作 `.kicad_sch` S-expression，并采用 write、fsync、rename 的原子写入与 UUID 保留。
- **PCB 实时编辑**：通过 KiCAD 10 IPC API（NNG + protobuf）修改打开的 board，并结合 undo/redo。
- **按需工具集**：把大量工具拆成 toolsets，减少一次性暴露给模型的 schema/context。
- **检查与导出**：调用 `kicad-cli` 完成 ERC、DRC、Gerber、drill、BOM、pick-and-place、PDF 等输出。
- **布线路径**：支持 DSN/SES 与本地 Freerouting 组合，并在导入前做 revision/manifest 检查。
- **MCP transport**：默认 stdio，也可配置 Streamable HTTP；后者会增加网络服务安全面。

## 价值

- 将 KiCAD 编辑、检查和制造交接步骤组织为结构化、可追踪工具调用。
- Rust 单二进制与 KiCAD 官方 IPC 方向减少旧版多语言/SWIG 调用链的依赖表面。
- ERC/DRC、BOM health 和审查工具有机会把 agent 生成与确定性检查放在同一流程。
- 原子写入、UUID 保留、undo/redo 与 revision-bound import 是面向可恢复编辑的重要设计点。

## 风险边界

- ERC/DRC 通过、文件可打开或 Gerber 可导出，都不证明电气安全、信号完整性、EMC、热、绝缘、可制造性或法规合规。
- LLM 可能选择错误器件、封装、引脚、额定值、stack-up 或布线；参考电路和 JLCPCB 库不能替代 datasheet、库存与生命周期核对。
- 上游标记 beta，Windows 最充分测试，Linux 仅有 CI、macOS 路径也需按实际版本验证；跨平台结果不能互相外推。
- 自动修改真实工程、导入 autorouter 结果或暴露 HTTP transport 可能造成不可逆设计偏差、并发冲突或未授权访问。
- AGPL 与商业许可边界需按内部工具、修改版网络服务和分发方式由法务判断；README 的概括不是法律意见。
- 生成制造文件不能直接下单；至少需要独立工程师审图、版本冻结、生产检查和样板测试。

## 补充建议

- 在复制工程上固定 KiCAD/Konnect 版本，逐工具保存 Git diff、截图、ERC/DRC 输出和调用日志。
- 建立带故意错误的 golden boards，验证引脚、net、clearance、差分对、stack-up、BOM 与回滚是否可靠。
- 对关键元件逐项核对 datasheet、footprint、3D model、封装方向、额定值、库存和替代料。
- 将制造导出与下单彻底分离；Gerber、drill、BOM、pick-and-place 必须由独立 reviewer 和 fab DFM 工具复核。
- 只使用 stdio/loopback 或经鉴权的 HTTP，并限制 agent 只能访问测试工程与允许的工具集。

## 参考资料

- [GitHub 仓库](https://github.com/mixelpixx/Konnect)
- [GitHub REST API](https://api.github.com/repos/mixelpixx/Konnect)
- [v0.11.0 Release](https://github.com/mixelpixx/Konnect/releases/tag/v0.11.0)
- [工具目录](https://github.com/mixelpixx/Konnect/blob/main/tool-directory.md)
- [Roadmap](https://github.com/mixelpixx/Konnect/blob/main/ROADMAP.md)
- [AGPL-3.0 License](https://github.com/mixelpixx/Konnect/blob/main/LICENSE)
