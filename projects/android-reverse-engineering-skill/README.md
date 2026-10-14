<!-- markdownlint-disable MD013 -->

# Android Reverse Engineering Skill（SimoneAvogadro/android-reverse-engineering-skill）中文解读

> 上游仓库：<https://github.com/SimoneAvogadro/android-reverse-engineering-skill> · 归类：Coding Agents 与终端助手 · 本页基于 2026-10-15 的 README、`SKILL.md`、Privacy、安装脚本入口、Release / tag、第三方工具说明、许可证与 GitHub REST API 静态整理；未下载依赖、反编译 APK 或将反编译内容交给 Claude。

## 定位

Android Reverse Engineering Skill 是 Claude Code 插件 / skill，用本地脚本编排 jadx、Vineflower / Fernflower、dex2jar、Apktool、adb 等工具，完成 APK / XAPK / JAR / AAR 指纹、反编译、Kotlin 名称恢复、调用链追踪与 HTTP API 清单。它主要是工作流与脚本集合，不包含作者运行的分析服务器。

## 用法

先对自有或明确授权样本执行 `fingerprint.sh`，识别 native、Flutter、React Native、Cordova / Xamarin 与混淆程度；Java / Kotlin 样本再检查 JDK 17+ 与 jadx，按需安装可选工具。反编译后先产出全部 endpoint 的轻量 Tier 1 清单，只对 auth、支付或用户指定路径做最多约 10 个 Tier 2 深挖。

## 原理

- fingerprint 直接扫描 DEX / native / framework 标记，先判断正确的逆向工具路线。
- wrapper 处理普通、split 和 XAPK，并可同时运行 jadx 与 Vineflower 对比 warning 和输出文件。
- 对混淆 Kotlin 使用 metadata 恢复命名；以 Retrofit、OkHttp、Ktor、URL 字符串与 `BuildConfig` 为锚点追踪调用。
- skill 把结构、endpoint、headers、request / response 与 UI → repository → network 调用链整理成固定交付结构。

## 价值

- 在成本较高的全量反编译前做框架分诊，可避免对 Flutter / RN 样本盲跑 jadx。
- 双 decompiler 与分层 endpoint 清单兼顾覆盖和人工复核成本。
- 上游明确列出本地处理、依赖下载、第三方许可证与 Claude 数据边界，便于合规评估。

## 风险边界

- 仅限安全研究、授权测试、互操作、恶意软件分析、教育 / CTF 等合法范围；工具 Apache-2.0 不授予目标 APK、服务或数据的分析权。
- 插件脚本不上传文件、不收 telemetry，但 Claude 会读取并按 Anthropic 条款处理用户提供的反编译源码；“本地反编译”不等于端到端本地。
- 自动安装会访问 GitHub / 包管理器，必要时可能请求 sudo 或修改用户 PATH；依赖及下载制品需要独立校验。
- API 字符串、`BuildConfig` secret、反编译控制流和恢复名称都可能误导或泄露敏感信息，不能直接用于未授权访问。
- API 最新 Release 仍为 `v1.1.0`，而 tags 已出现 `v1.7.0`；版本、插件 payload 与文档须以固定 commit 对齐。

## 补充建议

- 用隔离 VM、样本 hash 和书面 scope，禁用外网后分析；依赖安装与样本分析分成两个可审计阶段。
- 先用自建小 APK 建 ground truth，统计 endpoint recall、误报、调用链正确率和不同 decompiler 差异。
- 输出只保留必要片段，对 token / PII / 商业秘密脱敏；任何动态测试、证书绕过、hook 或请求重放另行授权。

## 参考资料

- GitHub 仓库：<https://github.com/SimoneAvogadro/android-reverse-engineering-skill>
- GitHub REST API：<https://api.github.com/repos/SimoneAvogadro/android-reverse-engineering-skill>
- `v1.1.0` Release：<https://github.com/SimoneAvogadro/android-reverse-engineering-skill/releases/tag/v1.1.0>
- `v1.7.0` tag：<https://github.com/SimoneAvogadro/android-reverse-engineering-skill/releases/tag/v1.7.0>
- Skill：<https://github.com/SimoneAvogadro/android-reverse-engineering-skill/blob/master/plugins/android-reverse-engineering/skills/android-reverse-engineering/SKILL.md>
- Privacy：<https://github.com/SimoneAvogadro/android-reverse-engineering-skill/blob/master/PRIVACY.md>
- LICENSE：<https://github.com/SimoneAvogadro/android-reverse-engineering-skill/blob/master/LICENSE>
