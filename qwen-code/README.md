# Qwen Code

## 为什么是今天的热门
GitHub 的 AI 趋势榜单中，`QwenLM/qwen-code` 位列今日靠前位置，显示出近期关注度显著上升。citeturn3search1

## 这是什么
Qwen Code 是一个开源的终端 AI 代理，定位为“住在终端里的 agentic coding 工具”，并针对 Qwen3-Coder 进行优化，主打理解代码库、自动化工作流与加速交付。citeturn3view0turn3view7

## 能做什么（关键能力）
- 从需求描述生成或扩展功能实现。citeturn3view3
- 调试并修复 bug，给出可执行的修改。citeturn3view3
- 快速理解并导航复杂代码库。citeturn3view3
- 自动化重复性任务，提高开发效率。citeturn3view3

## 工作原理（简述）
Qwen Code 以终端为核心交互界面，使用 agentic workflow 执行任务，能够直接编辑文件、运行命令、甚至创建提交；当需要外部上下文时，还可以通过 MCP 接入额外数据源与工具。citeturn3view3

它支持多协议接入，既可以使用 OpenAI/Anthropic/Gemini 兼容的 API，也可以用 Qwen OAuth 登录获取免费额度；同时内置 Skills 与 SubAgents，并支持 VSCode 与 JetBrains 等 IDE 的可选集成。citeturn4view0

## 快速上手
**安装**（二选一）：

```bash
npm install -g @qwen-code/qwen-code
# 或
brew install qwen-code
```
citeturn3view1

**启动**：

```bash
qwen
# 首次运行建议查看帮助并完成鉴权
/help
/auth
```
citeturn3view1

**环境要求**：Node.js 20+。citeturn3view1

## 认证与调用方式
- **Qwen OAuth**：可直接登录并获得免费请求额度。citeturn4view0
- **OpenAI/Anthropic/Gemini 兼容 API**：使用 API Key 方式接入。citeturn4view0

## 参考链接

```text
https://github.com/QwenLM/qwen-code
https://qwenlm.github.io/qwen-code-docs/en/users/overview/
https://github-trending-api-wonderfulapi.vercel.app/github-trending-ai
```
