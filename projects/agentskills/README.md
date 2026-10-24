<!-- markdownlint-disable MD013 -->

# agentskills：Agent Skills 开放格式与渐进加载规范

- 主上游：[agentskills/agentskills](https://github.com/agentskills/agentskills)；repository ID `1117639997`。
- 采样日期：2026-10-25（Asia/Shanghai）；分类：Agent 框架与技能生态。
- API 累计快照：26,571 stars / 1,956 forks / 104 open issues（含 PR 口径）；与榜单日增分开。
- 默认分支 `main`，本页静态依据固定在 `69ef37e9424c0a7ea9dd2293b559e43ec8176379`。公开 Release 列表为空，不据此推断没有 tag 或包发行。
- 核验层级：直接读取上游文档、许可、元数据和下列部分实现；未安装运行、调用模型或复现性能。

## 定位

这是 Agent Skills 格式的规范与文档仓库，定义怎样把领域知识、操作流程和可选脚本打包成技能。它不是某个宿主的技能全集，也不是 Agent 执行器。README 说明格式源自 Anthropic，面向多种兼容客户端开放发展；具体支持程度仍需逐产品检查。

## 用法

从一个最小目录开始，将下面内容保存为 `my-skill/SKILL.md`，然后按目标宿主的本地技能发现方式接入：

```markdown
---
name: my-skill
description: 检查示例数据表的列名与单位，在用户要求数据检查时使用。
---
读取输入表，列出缺列与单位不一致的问题；保留原始文件。
```

`name` 与 `description` 必填，目录名须与 name 一致。规范还定义 license、compatibility、metadata 和实验性的 allowed-tools。不要把格式示例直接当成跨客户端通用安装命令。

## 原理

渐进披露分三步：发现时读取名称与描述，任务匹配时加载完整 SKILL.md，执行时才按需读取 references、assets 或运行 scripts。这样把可复用程序性知识从主提示分离，并降低常驻上下文体积。格式约束与宿主的匹配、加载和工具实现是不同层；实验性字段能否真正执行必须在宿主验证。

## 价值

适合把已有稳定工作流、领域术语、模板与验收条件版本化，也便于在多个 Agent 之间共享。最有价值的是清晰的触发条件、输入输出和来源边界，不能仅用技能数量评价团队能力或成功率。

## 风险边界

SKILL.md 和引用文件可以包含不可信指令，脚本还可能执行代码、写入文件或联网。allowed-tools 是实验性元数据，不构成 OS 沙箱或通用授权证明；符合格式也不证明来源可信。根代码为 Apache-2.0，docs 为 CC BY 4.0，第三方技能拥有各自许可；复用时应按实际目录与资源核对。

## 补充建议

先用纯说明和只读 fixture 验证触发、误触发、引用加载和输出格式，再逐项加入脚本。记录宿主版本、依赖、所需权限、网络出口、失败恢复和禁止自动执行的动作；将格式校验与真实任务评估分开维护。

## 参考资料

- [README.md](https://github.com/agentskills/agentskills/blob/69ef37e9424c0a7ea9dd2293b559e43ec8176379/README.md)。
- [docs/specification.mdx](https://github.com/agentskills/agentskills/blob/69ef37e9424c0a7ea9dd2293b559e43ec8176379/docs/specification.mdx)。
- [LICENSE](https://github.com/agentskills/agentskills/blob/69ef37e9424c0a7ea9dd2293b559e43ec8176379/LICENSE)。
- [docs/LICENSE](https://github.com/agentskills/agentskills/blob/69ef37e9424c0a7ea9dd2293b559e43ec8176379/docs/LICENSE)。
- [仓库 API](https://api.github.com/repos/agentskills/agentskills)、[发行 API](https://api.github.com/repos/agentskills/agentskills/releases?per_page=3)；动态元数据只代表本轮采样。
- 事实来源为以上固定文件；价值、风险评估和验证建议为本库工程判断，未作为上游实测结果。
