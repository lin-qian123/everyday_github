# qiaomu-anything-to-notebooklm

## 项目定位

- GitHub：<https://github.com/joeseesun/qiaomu-anything-to-notebooklm>
- 定位：将多源内容（网页/YouTube/PDF/Markdown/搜索等）转换为 NotebookLM 可消费素材，并生成播客/PPT/脑图/问答等产物。
- 当前信号（2026-05-16 抓取）：约 2.6k stars。

## 用法

### 安装（仓库推荐流程）

```bash
cd ~/.claude/skills/
git clone https://github.com/joeseesun/qiaomu-anything-to-notebooklm
cd qiaomu-anything-to-notebooklm
./install.sh
```

### 初始化

```bash
notebooklm login
notebooklm list
```

## 原理

- **输入归一化层**：识别多种输入源并做统一抽取。
- **转换层**：调用文件转换和抓取能力，把内容整理为 NotebookLM 友好格式。
- **生成层**：交给 NotebookLM 生成目标输出（如播客、演示稿、测验）。

## 价值

- 把“资料收集-结构化-再创作”从多工具切换压缩为单流程。
- 对学习型和内容型工作流（课程、研究、知识库）效率提升明显。

## 风险边界

- 部分来源抓取涉及平台规则与版权边界，需合规使用。
- 自动生成内容存在幻觉与事实偏差，不能直接当最终稿。
- 长链路处理失败点较多，需要重试与监控策略。

## 补充建议

- 默认先处理公开授权内容，减少版权风险。
- 对生成结果做事实核查清单（数据、引用、结论）。
- 为关键流程保留中间产物，便于回滚和审计。

## 参考资料

- GitHub 仓库：<https://github.com/joeseesun/qiaomu-anything-to-notebooklm>
- NotebookLM：<https://notebooklm.google.com>
