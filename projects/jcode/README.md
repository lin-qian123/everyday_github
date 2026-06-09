# jcode（记录日期：2026-05-01）

- GitHub：<https://github.com/1jehuang/jcode>
- 趋势信号：GitHub Trending（今日榜单出现）

## 1. 项目定位
`jcode` 把自己定义为“下一代 coding agent harness（智能体执行底座）”。
它关注的不是某个模型本身，而是：
- 多会话并行
- 更低资源占用
- 持久化记忆
- 浏览器工具内置

也就是把“模型能力”转化为“工程可执行能力”。

## 2. 基础用法
1. 安装：
   - macOS/Linux：`curl -fsSL https://raw.githubusercontent.com/1jehuang/jcode/master/scripts/install.sh | bash`
2. 启动与连接：
   - `jcode serve`
   - `jcode connect`
3. 浏览器工具：
   - `jcode browser status`
   - `jcode browser setup`
4. 按任务组织多会话（调研、编码、验证分离），最后统一审阅输出。

## 3. 原理理解
- Harness 层：统一代理会话生命周期、工具调用、输出结构。
- 记忆层：将对话转为向量记忆并做相似检索，减少“反复喂上下文”的成本。
- 工具层：内建 browser 等动作，覆盖从代码到页面操作的闭环。
- 性能层：强调低内存占用与快启动，适合多会话常驻。

它解决的是“如何稳定地跑 agent 任务”，而不只是“让模型回答更聪明”。

## 4. 适用场景
- 需要长期运行 agent（不是一次性问答）的个人/团队。
- 希望把网页操作纳入同一条自动化链路（抓取、测试、录证据）。
- 需要把历史任务沉淀为可检索记忆资产。

## 5. 潜在争议与注意点
- 内存系统会带来额外隐私/数据治理要求。
- 多工具自动化越强，越需要严格权限边界与人工复核点。
- 作为新项目，生态稳定性和最佳实践仍在快速演进。

## 6. 补充材料
- 仓库 README 的性能与内存章节：<https://github.com/1jehuang/jcode>
- 安装脚本与后端工具说明：同仓库文档
