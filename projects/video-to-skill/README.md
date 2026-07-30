# video-to-skill

## 定位

`video-to-skill` 试图把公开视频、播放列表、课程或本地媒体转为可安装的、带来源时间戳的 Agent Skill，面向 Claude Code 与 Codex 的教学、练习、检索和项目应用。

截至 2026-07-31，GitHub API 快照显示其创建于 2026-07-30，约 11 stars、0 forks，MIT 许可证。项目仍属早期开发者信号，尚无独立覆盖率或教学质量基准。

## 用法

可通过 Agent Skills 安装，随后以视频、课程或播放列表 URL 调用。首次使用会创建私有 Python runtime，并要求 Python 3.11--3.13、Node.js、网络和 FFmpeg。

```bash
npx skills add Lum1104/video-to-skill --skill video-to-skill \
  --global --agent claude-code --agent codex --yes
```

在 Codex 中例如输入：`$video-to-skill <课程或视频 URL>`。先确认访问权限与输出目录，再检查最终 coverage report 中的失败或不可访问条目。

## 原理

流水线依次盘点可访问媒体、获取字幕/音频/分析用视频、对齐语音/章节/镜头变化/OCR，再让宿主 agent 将证据合成为概念、练习、工作流与带时间戳出处的技能。运行时与项目环境隔离，并缓存证据和依赖。

## 价值

- 相比单纯转录，更强调演示画面、练习和来源定位，适合把许可课程转成可执行学习材料。
- 将私有 runtime、失败可见性和依赖指纹作为可恢复处理过程的一部分。

## 风险边界

- 不会绕过 DRM、付费墙、删除内容或平台权限；只处理有权访问的材料。
- 课程、字幕、截图和生成笔记仍可能受版权、合同与隐私约束，不能因“生成 skill”自动再分发。
- LLM 综合会遗漏或误读画面；时间戳不是事实正确性的保证，关键技术结论要回看原材料。

## 补充建议

先用一节公开、可许可的短课程测量概念覆盖、引用可回跳率和练习正确率。生产使用时保存 URL、授权依据、处理日期和 coverage report，并把课程 skill 限定为参考材料而非权威规范。

## 参考资料

- GitHub：<https://github.com/Lum1104/video-to-skill>
- GitHub API 快照：<https://api.github.com/repos/Lum1104/video-to-skill>
- 架构说明：<https://github.com/Lum1104/video-to-skill/blob/main/docs/architecture.md>
