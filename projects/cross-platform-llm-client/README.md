<!-- markdownlint-disable MD013 -->

# cross-platform-llm-client（PrivateLM）

- 更新：2026-11-07（Asia/Shanghai）；官方 C++ daily +137，为读取快照，不是自然日结算。
- GitHub API：1,580 stars / 329 forks / 23 open issues（含 PR）；仓库 ID `1220937125`。
- 核读基线：`8a5f3b0c0ca8c2108b76ac9619fe5faf6a6a098e`；仅文档与抽样实现核验，未安装运行或独立评测。

## 定位

PrivateLM 是 Flutter 移动端 AI 客户端，结合本地模型、云 provider、聊天持久化、图像能力和 OpenAI 兼容服务。仓库语言榜标 C++，来自其中的原生推理代码；不能因此把整个应用写成 C++。Android / iOS 可用本地后端，Web 当前是云端路径。[README](https://github.com/orailnoor/cross-platform-llm-client/blob/8a5f3b0c0ca8c2108b76ac9619fe5faf6a6a098e/README.md)

## 用法

发行页最新项目为 [1.0.7-cluster](https://github.com/orailnoor/cross-platform-llm-client/releases/tag/1.0.7-cluster)（UTC 2026-11-04），GitHub 标记非 prerelease，但 APK 文件名含 cluster-test，仍应按实验功能验证。先确认 APK 架构、签名、剩余内存和 GGUF 模型许可，从小模型开始。源码构建示例为：

```bash
flutter pub get
flutter build apk --debug
```

Android 实际 Gradle 的 minSdk 为 28，README 构建前提却写 API 26+，本页采用实现条件并保留文档差异。iOS 发行采用侧载 IPA，需签名 / Developer Mode；真实安装与平台能力未复现。Web 不能当本地离线体验。[Android 配置](https://github.com/orailnoor/cross-platform-llm-client/blob/8a5f3b0c0ca8c2108b76ac9619fe5faf6a6a098e/android/app/build.gradle.kts)

## 原理

Flutter / GetX 管界面和状态，Hive 存储聊天与设置，原生插件封装 llama.cpp、Vulkan / Metal 等后端。云服务适配多种 provider，模型下载与推理是不同数据流。

Cluster 由 Android 作 master，Android / iOS worker 分担模型层；当前源码只允许 Android master，iOS worker 的停止需要关闭应用。发行文档的四设备 26B 约 4–5 tokens/s 是作者预期，缺少本轮固定设备、模型量化、上下文与网络实验，不能当独立测速。[Cluster 实现](https://github.com/orailnoor/cross-platform-llm-client/blob/8a5f3b0c0ca8c2108b76ac9619fe5faf6a6a098e/lib/services/cluster_service.dart)

## 价值

便于比较手机本地推理、云端 API 和局域网服务，亦可研究移动设备的内存、散热与网络瓶颈。实际价值应由任务质量、首 token、持续吞吐、峰值内存、耗电和断网行为共同判断；“uncensored”只是模型 / 产品描述，不代表回答正确。

## 风险边界

- README 的“除云模式外不离机”不能涵盖所有网络流量：启动路径注册 CrashReportingService；Firebase 可初始化时调用 `setCrashlyticsCollectionEnabled(true)`，收集设备、模型 / 生成状态和筛选日志；缺配置时禁用。源码有脱敏逻辑，但本轮未核二进制配置、完整字段或实际外发。[启动路径](https://github.com/orailnoor/cross-platform-llm-client/blob/8a5f3b0c0ca8c2108b76ac9619fe5faf6a6a098e/lib/main.dart)、[崩溃上报](https://github.com/orailnoor/cross-platform-llm-client/blob/8a5f3b0c0ca8c2108b76ac9619fe5faf6a6a098e/lib/services/crash_reporting_service.dart)
- 设置控制器把 provider key 写 Hive，抽样 openBox 未传 encryptionCipher；不能将“本地保存”写成系统钥匙串或已证实的静态加密。[设置](https://github.com/orailnoor/cross-platform-llm-client/blob/8a5f3b0c0ca8c2108b76ac9619fe5faf6a6a098e/lib/controllers/settings_controller.dart)、[存储](https://github.com/orailnoor/cross-platform-llm-client/blob/8a5f3b0c0ca8c2108b76ac9619fe5faf6a6a098e/lib/services/hive_service.dart)
- HTTP 服务默认绑定 loopback，首次开启局域网访问需非空 API key；这是应用服务入口规则，不等于 cluster 通道已有相同认证或传输加密。[服务监听](https://github.com/orailnoor/cross-platform-llm-client/blob/8a5f3b0c0ca8c2108b76ac9619fe5faf6a6a098e/lib/services/openai_server_service_io.dart)
- 软件根许可 MIT，模型、图像权重和依赖另核。签名历史曾变化，卸载可能丢模型；不要用不明 APK 或真实敏感文档试验。

## 补充建议

先对授权短文本做单机冷 / 热启动和断网测试，再测试多设备加入、掉线、停止、内存不足和温控。使用临时 key，检查备份、导出和删除是否带走凭据；以网络抓取和实际发行包配置验证云调用、更新检查、崩溃上报分别何时发生。本轮未安装 APK / IPA、下载模型、连接 cluster 或运行推理。

## 参考资料

- [仓库](https://github.com/orailnoor/cross-platform-llm-client)、[Cluster 发行](https://github.com/orailnoor/cross-platform-llm-client/releases/tag/1.0.7-cluster)。
- [README](https://github.com/orailnoor/cross-platform-llm-client/blob/8a5f3b0c0ca8c2108b76ac9619fe5faf6a6a098e/README.md)、[MIT 许可](https://github.com/orailnoor/cross-platform-llm-client/blob/8a5f3b0c0ca8c2108b76ac9619fe5faf6a6a098e/LICENSE)、[平台条件](https://github.com/orailnoor/cross-platform-llm-client/blob/8a5f3b0c0ca8c2108b76ac9619fe5faf6a6a098e/android/app/build.gradle.kts)。
- [Cluster](https://github.com/orailnoor/cross-platform-llm-client/blob/8a5f3b0c0ca8c2108b76ac9619fe5faf6a6a098e/lib/services/cluster_service.dart)、[API server](https://github.com/orailnoor/cross-platform-llm-client/blob/8a5f3b0c0ca8c2108b76ac9619fe5faf6a6a098e/lib/services/openai_server_service_io.dart)。
- [启动](https://github.com/orailnoor/cross-platform-llm-client/blob/8a5f3b0c0ca8c2108b76ac9619fe5faf6a6a098e/lib/main.dart)、[Crashlytics](https://github.com/orailnoor/cross-platform-llm-client/blob/8a5f3b0c0ca8c2108b76ac9619fe5faf6a6a098e/lib/services/crash_reporting_service.dart)、[设置存取](https://github.com/orailnoor/cross-platform-llm-client/blob/8a5f3b0c0ca8c2108b76ac9619fe5faf6a6a098e/lib/controllers/settings_controller.dart)、[Hive](https://github.com/orailnoor/cross-platform-llm-client/blob/8a5f3b0c0ca8c2108b76ac9619fe5faf6a6a098e/lib/services/hive_service.dart)。
