<!-- markdownlint-disable MD013 -->

# Stitch Design Skills（google-labs-code/stitch-skills）中文解读

> 上游仓库：<https://github.com/google-labs-code/stitch-skills> · 归类：前端、UI 与 Agent 交互层 · 证据快照：2026-10-17（Asia/Shanghai）。API：8,525 stars / 1,114 forks / 17 open issues；GitHub Release / tag `v1.0`；当前 main 已采用三插件布局；Apache-2.0；README 声明并非正式支持的 Google 产品。本页为上游资料与相关代码的静态整理，未安装运行、复测性能或完成全面安全审计。

## 定位

Stitch Design Skills 是 google-labs-code 提供的 Google Stitch 工作流技能与插件集合，覆盖设计生成、设计系统、资产上传、组件构建和视频 walkthrough。它遵循 Agent Skills 形式，依赖配置好的 Stitch MCP / 账号，并不自带离线设计模型。

## 用法

先完成 README 链接的 Stitch MCP setup，再按宿主安装需要的 `stitch-design`、`stitch-build` 或 `stitch-utilities`。Codex 使用上游 marketplace 布局；Claude Code / Cursor 可以项目级安装；OpenCode 须手工复制并按其规则适配 skill 名称 / tool 名。先用一个无敏感数据的 screen 验证生成或 HTML 上传，避免一次性导入整个私有前端。

## 原理

- design 插件从文本 / 图片生成或编辑 screen，提取 DESIGN.md、静态 HTML，并上传到目标 Stitch project。
- build 插件将 screen 转成 React / React Native 等组件，也可用 Remotion 制作 walkthrough；utilities 负责提示改写、设计规范与页面循环。
- 上传脚本在本地读取文件、base64 编码后直接 POST 到 Stitch API，绕过模型重输出大文件导致截断的问题；这是实际文件外发和远端 screen 创建。

## 价值

- 设计系统、静态页面、设计 screen 与组件之间有明确中间产物，有助于团队定位视觉漂移。
- 把复杂设计任务拆成可重用技能，适合与现有前端工程结合；只装所需插件可减少上下文与权限面积。
- “production-ready”“anti-generic”是工作流目标，仍需要工程和用户体验验收。

## 风险边界

- upload-to-stitch 技能指导读取现有 MCP 凭据，脚本使用 API key、project ID 和文件路径；私有代码、内联图片、用户数据与设计素材可随 HTML 一并外发。
- 脚本允许自定义 `--api-url`，应核对 endpoint 与凭据用途；示例把 key 作为参数时还要考虑终端历史 / 进程参数暴露。
- 选择性安装有技能依赖，宿主间 frontmatter / 工具兼容性不同；统一标准不能保证相同行为。
- Apache-2.0 覆盖仓库代码，不替代 Stitch 服务、模型、配额和输入素材权利的条件；README 明确不是正式支持的 Google 产品。

## 补充建议

固定仓库版本、宿主与插件清单，上传前检查自包含 HTML 中的图片 / 数据，使用专用测试 project。分别验收设计 tokens、组件编译、键盘访问与移动布局；登记云端资源、费用和删除路径。

## 参考资料

- 上游仓库：<https://github.com/google-labs-code/stitch-skills>
- GitHub REST API：<https://api.github.com/repos/google-labs-code/stitch-skills>
- 安装 / 插件目录：<https://github.com/google-labs-code/stitch-skills/blob/main/README.md>
- 上传工作流：<https://github.com/google-labs-code/stitch-skills/blob/main/plugins/stitch-design/skills/upload-to-stitch/SKILL.md>
- 实际上传实现：<https://github.com/google-labs-code/stitch-skills/blob/main/plugins/stitch-design/skills/upload-to-stitch/scripts/upload_to_stitch.py>
- 许可：<https://github.com/google-labs-code/stitch-skills/blob/main/LICENSE>
- Releases：<https://github.com/google-labs-code/stitch-skills/releases>
