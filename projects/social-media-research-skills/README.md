<!-- markdownlint-disable MD013 -->

# Social Media Research Skills（ScrapeCreators/social-media-research-skills）中文解读

> 上游仓库：<https://github.com/ScrapeCreators/social-media-research-skills> · 归类：办公、商业与行业应用 · 证据快照：2026-10-18（Asia/Shanghai）。认证 API：4,031 stars / 82 forks / 5 open issues；无 GitHub Release / tag；MIT。本页为上游材料及所列源码的静态整理，未安装运行、复测 benchmark 或完成全面安全审计。

## 定位

这是依赖 ScrapeCreators 公共社媒数据 API 的技能集合，覆盖异常表现帖子、评论挖掘、转录分析、竞品比较、广告库、受众和需求研究。它把原始 JSON 组织成可引用报告，适合市场研究 / 内容分析；仓库开放不代表数据服务免费、私有数据可取或全平台覆盖完整。

## 用法

上游安装入口为 `npx skills add ScrapeCreators/social-media-research-skills`，随后为实际宿主配置 `SCRAPECREATORS_API_KEY`。先选一个公共账号、一个平台与明确日期窗口，限制页数、调用数和产物范围。需要原始抓取时用 `scrapecreators-api`，需要分析时用相应 workflow；本轮只读材料，没有申请密钥或调用计费 API。

## 原理

README 列出 13 项技能：底层 API 路由 + 12 类研究工作流。`outlier-post-finder` 要求尽量获取至少 20 条帖子，分别按账号、平台和内容形式建立中位数基线，再计算 views / engagement lift；不足 10 条需标低置信度。`social-listening-brief` 组织主题与情绪，并保留来源和日期，明确不把互动量当真实性。

## 价值

比单纯按播放数排序更适合比较不同账号内的相对表现，也能把分析产物固定为来源表、评论主题和 CSV。工程上可借鉴其窗口、分组基线和证据字段设计；这些规范由技能指令表达，实际 Agent 是否遵守仍需校验。

## 风险边界

- 公共帖子、评论、账号与查询会经过第三方 API 和宿主模型；API key、返回数据、日志与导出需分别管理。公开可见也不等于可以无限再传播用户内容。
- 各平台可见指标、更新时延、分页覆盖和删除状态不同；不能合成一个无偏的跨平台热度排行，也不能把样本情绪当总体民意。
- lift 在分母为零、帖子年龄差异、付费推广和极小样本下不稳。技能中的 1.5x / 2x / 5x 是启发式阈值，并非统计显著性。
- MIT 覆盖仓库技能；API 使用、额度与数据获取另受服务规则约束。没有 Release / tag，安装默认分支会漂移。

## 补充建议

用自有公共账号做小样本：保存原始指标、采样时间、帖子年龄、失败 / 缺失字段、分页上限与费用；按平台和格式分别比较中位数。让分析明确区分观测、推断和建议，对引用做回链核对；这套技能的存在不能填补本日报尚未取得的社媒证据。

## 参考资料

- 上游仓库：<https://github.com/ScrapeCreators/social-media-research-skills>
- GitHub REST API：<https://api.github.com/repos/ScrapeCreators/social-media-research-skills>
- README / 技能表：<https://github.com/ScrapeCreators/social-media-research-skills/blob/main/README.md>
- API 路由技能：<https://github.com/ScrapeCreators/social-media-research-skills/blob/main/skills/scrapecreators-api/SKILL.md>
- Outlier 计算规范：<https://github.com/ScrapeCreators/social-media-research-skills/blob/main/skills/outlier-post-finder/SKILL.md>
- 社媒监听边界：<https://github.com/ScrapeCreators/social-media-research-skills/blob/main/skills/social-listening-brief/SKILL.md>
- 服务文档：<https://docs.scrapecreators.com>
- 许可：<https://github.com/ScrapeCreators/social-media-research-skills/blob/main/LICENSE>
