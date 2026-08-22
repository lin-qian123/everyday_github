<!-- markdownlint-disable MD013 -->

# clipfactory

> 上游仓库：[feyzilim/clipfactory](https://github.com/feyzilim/clipfactory) · 归类：语音、视频与多模态 · 本页基于 2026-08-23 的上游 README 与 GitHub API 快照整理。

## 定位

`clipfactory` 是一个自托管短竖屏视频流水线：用户提供主题、模板和自有 B-roll 后，系统可用 LLM 生成脚本与镜头计划、用语音服务生成配音和时间戳、生成字幕，并由 FFmpeg 渲染。独立的 AI Lab 支持由提示词到 storyboard、关键帧和视频片段的路径；项目声明不会自动发布到社媒平台。

API 快照：约 44 stars、7 forks、0 个开放 issue；创建于 2026-08-22。GitHub API 的 SPDX 字段为 `NOASSERTION`，而 README 与仓库 LICENSE 标示 Elastic License 2.0；本文以 README 的许可证说明描述为准，实际适用范围仍须阅读 LICENSE 并由使用方核验。该项目是早期开发者信号，不能据此推断产出质量或平台传播度。

## 用法

上游推荐 Docker 部署；先以离线 fake provider 跑通，不要一开始输入生产 API key：

```sh
git clone https://github.com/feyzilim/clipfactory.git
cd clipfactory
docker compose up -d

# 浏览器打开 http://localhost:3000 后，选择 Offline dry run
make doctor
make generate TEMPLATE=story_v1 TOPIC="团队如何审阅 AI 视频草稿"
```

内容流水线需要自有 B-roll；生产模式至少需要 LLM 与语音 provider 的 key。AI Lab 还需要图像/视频 provider。README 明确指出 API 没有认证，因而仅应部署在本机或受控局域网，不能直接暴露到公网。

## 原理

- content factory 将 topic/template 依次拆为脚本、真实时长的配音、镜头计划、B-roll 匹配、已验证的视频 JSON、字幕、渲染与质量检查；每一件中间产物可版本化、替换和重渲染。
- B-roll 库按 persona、类别和批准状态管理，并用相关性、质量和近期使用度选择片段；未覆盖的镜头可以人工补拍或另走 AI 生成路径。
- AI Lab 将生成过程与主流水线隔离：提示词先得到 storyboard 和串联关键帧，再按所选供应商生成片段、拼接为 9:16 MP4，并保留重做、编辑和 A/B 比较入口。

## 价值

- 把短视频制作的可编辑中间层显式保存，允许重写脚本、换一个片段或只重渲染一幕，而不是把生成结果当作不可追溯黑箱。
- 自带 offline dry run 与 synthetic clips 测试路径，利于先验证编排、失败恢复和渲染环境，而非先消耗云端额度。
- 默认人工审核与手动发布，有助于把内容责任和平台发布权限留在操作者手中。

## 风险边界

- 项目并非零成本：README 的粗略估计为内容流水线每条约 0.05--0.20 美元，AI Lab 约 1--15 美元；重试、供应商定价和模型选择会改变实际成本。
- 配置的外部 provider 会收到提示词、脚本、B-roll 描述、抽帧或关键帧等数据；密钥、个人画像、肖像、地点与商业素材需要按供应商条款和数据政策审查。
- API 无认证；容器端口、数据库、上传素材和生成结果若暴露到网络，可能泄露密钥或未发布内容。仅“Docker 本地运行”不自动解决此问题。
- Elastic License 2.0 对托管/管理服务有额外限制；README 的“视频归用户”表述也不覆盖上游模型、声音、音乐、肖像与平台条款。

## 补充建议

1. 先在隔离网络以 fake provider、合成素材和最小 Docker 权限跑一条端到端流程，记录端口、卷挂载、日志和失败恢复。
2. 将 key 放入受控 secret store 或本机环境，不写入 UI 截图、项目文件或 Git；为每个 provider 设置可撤销的低额度 key。
3. 对人物、客户素材和音乐建立授权清单；发布前人工审阅事实准确性、字幕、肖像同意、水印和平台政策。
4. 若需多人协作，先在反向代理、认证、备份加密、RBAC 和审计日志完善后再开放访问。

## 参考资料

- [上游 README / 部署与安全说明](https://github.com/feyzilim/clipfactory)
- [GitHub API 元数据](https://api.github.com/repos/feyzilim/clipfactory)
- [Elastic License 2.0](https://www.elastic.co/licensing/elastic-license)
- [Docker Compose 文档](https://docs.docker.com/compose/)
