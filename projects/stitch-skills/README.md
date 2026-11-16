<!-- markdownlint-disable MD013 -->

# Stitch Design Skills（google-labs-code/stitch-skills）

- GitHub：<https://github.com/google-labs-code/stitch-skills>
- 核查：2026-11-17（Asia/Shanghai）07 时段；9,718 stars / 1,241 forks / 19 open issues（含 PR）；仓库 ID `1135847870`。
- 热度：官方综合 / TypeScript daily +540；原位更新 2026-10-17 旧页，不新增目录。
- 固定 main：`0337446dadde6f8c94210444e2aa9d546126480f`；最新 Release 仍为 [v1.0](https://github.com/google-labs-code/stitch-skills/releases/tag/v1.0)，UTC 2026-05-18；本轮上榜不表示今天升级版本。
- 许可与证据：Apache-2.0；README 明确不是正式支持的 Google 产品。相关文档 / 上传 / 快照 / 校验源码静态抽样，未安装技能、登录或操作 Stitch。

## 定位

Google Stitch 的设计、资产上传、设计系统与组件工作流技能集合，沿 Agent Skills 标准组织为 `stitch-design`、`stitch-build`、`stitch-utilities`。它依赖宿主 Agent 和 Stitch 服务，并不提供离线设计模型。[固定 README](https://github.com/google-labs-code/stitch-skills/blob/0337446dadde6f8c94210444e2aa9d546126480f/README.md)

## 用法

先按上游说明配置 Stitch MCP，再选择需要的插件。Codex 的 marketplace / sparse 路径、Claude Code / Cursor 的项目级安装和 OpenCode 的手工复制不同，应固定仓库 SHA 与实际宿主版本，不把 README 的 `--ref main` 当冻结版本。先用无敏感数据的测试 project 检查最小设计或组件任务；本轮未安装。

设计、build 与 utilities 有跨技能依赖，选择性安装后需核对工具名和资源路径。Remotion walkthrough、React / React Native 生成也需要各自运行环境；能显示设计图不保证组件已编译或视频已验收。

## 原理

设计工作流把文字 / 图片转为 screen，管理 design system，并在 `DESIGN.md`、HTML、screen 与组件之间转接。上传器本地读取文件、base64 编码，通过带 `X-Goog-Api-Key` 的 POST 调用 `screens:batchCreate`，会创建远端资源。[上传实现](https://github.com/google-labs-code/stitch-skills/blob/0337446dadde6f8c94210444e2aa9d546126480f/plugins/stitch-design/skills/upload-to-stitch/scripts/upload_to_stitch.py)、[上传技能](https://github.com/google-labs-code/stitch-skills/blob/0337446dadde6f8c94210444e2aa9d546126480f/plugins/stitch-design/skills/upload-to-stitch/SKILL.md)

静态 HTML 提取推荐 Puppeteer 启动浏览器，加载页面、执行可选 auth script、抓取 DOM / CSS / 图片后再移除脚本等内容。移除的是导出物中的脚本，不能倒推源页在采集时没有执行脚本或联网。[提取工作流](https://github.com/google-labs-code/stitch-skills/blob/0337446dadde6f8c94210444e2aa9d546126480f/plugins/stitch-design/skills/extract-static-html/SKILL.md)、[快照实现](https://github.com/google-labs-code/stitch-skills/blob/0337446dadde6f8c94210444e2aa9d546126480f/plugins/stitch-design/skills/extract-static-html/scripts/snapshot.ts)

## 价值

把视觉设计、规范与代码分成可检查的中间产物，适合定位 tokens、布局和组件输出的漂移。可复用工作流有助于减少重复操作；“production-ready”“anti-generic”等是目标文案，需要额外的交互、可访问性、内容和工程验收。

## 风险边界

- 上传支持图片、HTML 和 Markdown；自包含 HTML 可含内联数据、图片和页面状态。上传前检查实际文件，不把“本地提取”当“不外发”。
- 上传器允许 `--api-url` 自定义 endpoint，key 用命令参数提供；源码还打印响应体前 1,000 字符或 HTTP 错误体。应核对目标、凭据可见性与日志，不把只读文件当无远端写入。
- 快照实现启动参数含 `--no-sandbox` / `--disable-setuid-sandbox`；`--auth-script` 会动态 import 并执行本地模块。使用专用环境、测试身份和受控页面；静态导出不构成浏览器隔离承诺。
- React `validate.js` 主要解析 TSX、寻找以 `Props` 结尾的 interface、检查部分 JSX className 的硬编码十六进制颜色。它不是完整 TypeScript 编译、业务测试、无障碍扫描或视觉验收。[组件校验源码](https://github.com/google-labs-code/stitch-skills/blob/0337446dadde6f8c94210444e2aa9d546126480f/plugins/stitch-build/skills/react-components/scripts/validate.js)
- Apache-2.0 覆盖仓库代码，Stitch 服务、模型、配额、凭据和素材权利另有条件；本轮未核云服务内部实现或删除行为。

## 补充建议

固定插件版本、输入 screen 与设计规范，用最小脱敏页面核导出 / 上传 diff。分别验收采集前的网络和脚本行为、导出物的敏感信息、云端资源、组件编译、移动布局与键盘访问；不要把单个 validator 通过作为交付结论。

## 参考资料

- [仓库 API](https://api.github.com/repos/google-labs-code/stitch-skills)、[v1.0](https://github.com/google-labs-code/stitch-skills/releases/tag/v1.0)、[Apache-2.0](https://github.com/google-labs-code/stitch-skills/blob/0337446dadde6f8c94210444e2aa9d546126480f/LICENSE)。
- README、上传器、快照与校验源码均固定本轮 SHA，见正文；完整树用于定位文件，源码核读为抽样，未执行上游。
