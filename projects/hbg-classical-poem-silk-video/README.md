# hbg-classical-poem-silk-video

- 仓库：[Mr-funny/hbg-classical-poem-silk-video](https://github.com/Mr-funny/hbg-classical-poem-silk-video)
- 快照：2026-08-04；创建于 2026-08-03，约 44 stars、5 forks，MIT。
- 分类：语音、视频与多模态

## 定位

将中国古诗词转换为 1080×1920 国风动态短视频的 Agent Skill：分镜、ImageGen 静帧、Docker 图生视频、书法字幕、环境声/BGM、转场和最终 MP4 质检被组织在同一管线。

## 用法

安装 skill 后提供诗词和镜头约束，例如逐句一景、固定镜头、仅让水纹/鸟/雾等局部物象运动。运行前按仓库的前置检查连接用户已授权的 Docker I2V 运行时；产出后按抽帧、黑帧、音轨、主体一致性和字幕安全区复查。

## 原理

先抽取意象、时空与情绪，按一句或两句分镜并选择水墨、工笔等风格通道。静帧中的建筑、树干和人物躯干被设为锚点，视频阶段限制主动作；最后以 ffmpeg 类流程叠加逐字书法和交叉淡化。

## 价值

相比只做推镜的模板，它将生成一致性和成片 QA 显式化，适合需要保留诗意叙事、可审阅制作过程和竖屏交付的内容实验。

## 风险边界

图生视频仍会重绘、复制主体或产生肢体错误；示例中涉及 ImageGen、Gemini I2V、字体、音乐与素材，各自的账户、地区和版权条款须核验。不要用安装脚本处理未审阅的密钥、Cookie 或私有素材。

## 补充建议

从无版权争议的公版诗词和自有素材开始；逐镜保存提示词、输入、运行时版本和 QA 帧。发布前审查配乐、生成画面、题字和人物肖像的权利链。

## 参考资料

- [项目 README](https://github.com/Mr-funny/hbg-classical-poem-silk-video)
- [GitHub API 元数据快照](https://api.github.com/repos/Mr-funny/hbg-classical-poem-silk-video)
