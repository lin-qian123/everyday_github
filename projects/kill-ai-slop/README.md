# kill-ai-slop

## 定位

`kill-ai-slop` 是一个反“AI 味”设计工具包：一部分是多语言网站，系统整理 AI 生成产品常见的视觉与文案套路；另一部分是 agent skill，可扫描 Web 项目并给出或执行去除 slop 的修改建议。

截至 2026-07-18 抓取时，仓库约 `598` stars、`22` forks，主要语言为 TypeScript，许可证为 `Apache-2.0`。

## 用法

- 直接访问 `killaislop.com` 阅读 33 类 AI-slop 特征与 before/after 示例。
- 本地运行网站：

```bash
cd website
npm install
npm run dev
```

- 安装 skill：

```bash
npx skills add yetone/kill-ai-slop
```

- 直接运行扫描器：

```bash
node skill/scripts/scan.mjs path/to/project
node skill/scripts/scan.mjs path/to/project --json
```

## 原理

项目把“AI 生成产品的默认审美”拆成可检测的 tell：例如滥用渐变、发光卡片、emoji、吉祥物、全大写指标卡等。网站负责建立 taxonomy，skill 复用这些规则，通过代码级信号扫描项目，并把发现映射到解释和 remediation playbook。

## 价值

- 把主观的“AI 味”转成可讨论、可扫描、可修复的工程对象。
- 对 coding agent 生成前端后的质量复核有直接价值。
- 适合接入 UI 审查、设计系统收敛和发布前检查流程。

## 风险边界

- 审美判断并非绝对规则，扫描结果需要结合品牌、受众和业务语境人工判断。
- 当前更偏 Web 项目和可静态识别的前端模式，对原生移动端或设计稿层面覆盖有限。
- 自动修复若缺少视觉回归检查，可能破坏原有品牌表达。

## 补充建议

- 与 `ui-ux-pro-max-skill`、`gzh-design-skill`、`design-md` 一起观察，判断 agent UI 质量控制是否会形成稳定 skill 套件。
- 若用于真实项目，建议把扫描结果作为 review 输入，再配合截图验收。

## 参考资料

- GitHub: <https://github.com/yetone/kill-ai-slop>
- Website: <https://killaislop.com>
