<!-- markdownlint-disable MD013 MD034 -->

# ASC：面向 Agent 的按需 Android 反编译前端

> 上游仓库：https://github.com/MG1937/ASC · 归类：Agent 框架与技能生态 · 本页基于 2026-09-16 的 README、`pyproject.toml`、依赖、LICENSE、GitHub Trending 与 REST API 静态整理；未处理真实 APK，也未复现上游 benchmark。

## 定位

ASC（命令名 `droidasc`）是面向 agent 与移动安全研究者的 Android 反编译前端。它不先把整个 APK 膨胀、索引成重型数据库，而是把编译产物当作只读数据源，按查询提取需要的 DEX、类、manifest 或交叉引用。

2026-09-16 的 GitHub 官方综合 / Python Trending 抓取显示约 `+122 stars today`；REST API 快照为 `1,138 stars / 194 forks / 6 open issues`，Apache-2.0，main 最近 push 为 2026-09-15。包版本为 `0.1.0`，没有 GitHub Release。

## 用法

Python 要求 `>=3.10`，上游提供 PyPI 和源码安装路径：

```sh
pip install droidasc
droidasc getmanifest app.apk -o AndroidManifest.xml
droidasc getclass app.apk com.example.MainActivity -o MainActivity.java
droidasc findrefs app.apk string token -o string_refs.txt
```

`requirements.txt` 固定 `androguard==4.1.3`，而 `pyproject.toml` 写的是 `androguard>=4.1.3`；需要可复现环境时应自行锁定解析器版本。

## 原理

- 直接在压缩流和 DEX 结构上查找目标，避免预先完整展开与构建全局交叉引用索引。
- 利用 R8 编译优化留下的常量搬移与指令去重布局，定位跨 DEX 的字符串、类型、方法和字段引用。
- 命中后只抽取目标字节码及依赖，在内存中重建最小自洽 DEX，再交给反编译流程。
- 上游称方法定位可做到 O(1)，并在一个 352 MB 商业 APK 上报告 1.79 秒全局引用搜索、177 毫秒目标类反编译和 141 MB 内存；这些是作者演示数据，不是本仓库实测。

## 价值

- 给 agent 暴露粒度明确、文本可读的 CLI，适合先检索再精确展开，而不是把整个大型 APK 塞进上下文。
- 对移动研究中的 manifest、类和交叉引用提供同一入口，便于脚本化和保留命令证据。
- 无需长时间预处理，适合迭代式问题定位和临时分析环境。
- 代码、包元数据和 Apache-2.0 LICENSE 可审阅，工程边界比纯在线反编译服务清楚。

## 风险边界

- 反编译和安全分析只应针对自有、获授权或法律允许的样本；工具可用不等于绕过许可、版权或访问控制合法。
- APK 是不可信输入；解析器、压缩流、临时文件和外部反编译组件应放在无凭据、低权限、可丢弃环境中。
- 按需重建的最小 DEX、模糊类名和 R8 优化可能丢失语义或造成误关联，不能把反编译结果当作原始源码。
- 作者 benchmark 只有一个公开描述的商业 APK 场景，不能外推到多 DEX、壳、混淆、恶意压缩包或不同硬件。
- 目前没有 GitHub Release；PyPI 包、仓库 main 与安装依赖的供应链一致性仍需单独核验。
- 本页未执行 `droidasc`，也未验证 GUI、线程参数、性能、安全或对抗样本稳定性。

## 补充建议

1. 固定 ASC commit、Python、Androguard 与 Java/反编译器版本，并记录 APK SHA-256。
2. 从自建小 APK 开始建立金标：manifest、类、字符串、方法与字段引用都应和源码及 `jadx` 等独立工具交叉检查。
3. 对 zip bomb、异常 DEX、路径穿越和超大输入设置 CPU、内存、文件数、输出目录和超时限制。
4. 若接入 agent，先把 CLI 包成只读工具，只允许白名单样本目录和显式输出目录，不开放任意 shell。

## 参考资料

- 上游 README：https://github.com/MG1937/ASC
- 包元数据：https://github.com/MG1937/ASC/blob/main/pyproject.toml
- GitHub REST API：https://api.github.com/repos/MG1937/ASC
- LICENSE：https://github.com/MG1937/ASC/blob/main/LICENSE
- Black Hat Europe Arsenal 入口：https://blackhat.com/europe/arsenal/schedule/index.html#droid-asc-r8-compiler-optimization-as-a-decompiler-primitive-54834 （本轮直连返回 403，标题与 URL 由上游 README 交叉确认）
