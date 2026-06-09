# NanoClaw

## 一句话简介
NanoClaw 是一个运行在 macOS 上、利用 Apple 容器与 Anthropic Agents SDK/Claude Code 的本地开发助手，主打“每个任务一个隔离容器”的安全工作流与一键启动体验。

## 适合解决的问题
- 需要在本机执行代码/命令但又担心安全隔离
- 快速开一个“可丢弃”的开发沙盒（每个任务独立容器）
- 使用 Claude Code 做代码生成、改动、测试的工程流

## 核心机制（原理简述）
- **容器隔离**：通过 Apple 的容器框架把每个任务放进独立容器中，减少对宿主系统的影响。
- **Agent 驱动**：基于 Anthropic 的 Agents SDK 与 Claude Code，让模型可以执行项目内任务（读写文件、运行命令等）。
- **任务级生命周期**：每个任务对应一个容器，任务结束即可销毁或保留快照，便于复现与回滚。

## 快速开始
### 前置条件
- macOS（建议较新版本）
- Apple 容器框架
- 安装并配置 Claude Code
- 有效的 Anthropic API Key

### 安装
```bash
# 使用 curl 安装（官方推荐）
curl -fsSL https://nanoclaw.bot/install.sh | sh
```

### 运行
```bash
nanoclaw
```

## 使用方式示例
- 让 Agent 读取项目上下文并生成补丁
- 在隔离容器内运行测试并汇总结果
- 针对某个任务建立可复现的沙盒环境

## 与常见工具的区别
- **更强隔离**：强调“每任务一个容器”的安全边界，而不是共享单一容器。
- **更贴近开发流**：天然围绕 Claude Code 与 Agents SDK 设计，减少胶水脚本。
- **一键上手**：安装与启动命令非常短，适合快速试用。

## 注意事项
- 运行容器需要足够的本地资源（CPU/内存/磁盘）。
- 任务输出建议先审查再合入主分支。
- 若需访问外部网络，确保容器网络策略符合团队要求。

## 参考链接
- [官方网站与安装说明](https://nanoclaw.bot)
- [GitHub 仓库](https://github.com/qwibitai/nanoclaw)
- [Agents SDK（Anthropic）](https://github.com/anthropics/anthropic-agents)
