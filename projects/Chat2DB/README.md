# Chat2DB

## 项目简介
Chat2DB 是一个面向开发者/数据分析的多数据库客户端，主打“AI+数据库管理”。它把常见的数据库管理能力（连接、SQL 编辑、可视化查询、数据导入导出、结果可视化）与 AI 能力结合在一起：比如用自然语言生成 SQL、自动补全/修正 SQL、SQL 解释与优化建议、基于元数据的智能推荐等。

## 为什么值得关注
- GitHub 日榜出现频率高，最近增长快，是典型的“通用型 AI 工具 + 工程效率”项目。
- 数据库场景与企业日常工作强相关，可复制性高（开发、数据、运营都能用）。

## 主要功能
- 多数据库连接：MySQL、PostgreSQL、Oracle、SQL Server、SQLite、ClickHouse、MongoDB 等。
- SQL 编辑体验：语法高亮、格式化、历史记录、模板管理、可视化结果。
- AI 辅助：自然语言生成 SQL、SQL 解释、错误修复、建议优化。
- 协作与资产管理：连接、脚本、SQL 模板统一管理。

## 基本原理（工作流视角）
1. **元数据采集**：读取数据库表结构、字段、索引等元数据，为 AI 理解上下文。
2. **自然语言到 SQL**：把用户问题与元数据拼接成提示词，交给模型生成 SQL。
3. **校验与执行**：对 SQL 做格式/语法校验，执行后返回结果。
4. **解释与优化**：把 SQL 与执行结果交给模型，生成可读解释与优化建议。

## 快速上手
### 方式一：下载安装包（推荐）
- 访问项目的 Releases 页面，下载对应平台的安装包。

### 方式二：Docker 运行
```bash
docker run -d --name chat2db -p 10824:10824 -p 10825:10825 chat2db/chat2db
```

### 方式三：本地构建
```bash
# 克隆项目
git clone https://github.com/chat2db/Chat2DB.git
cd Chat2DB

# 前端
cd chat2db-client
pnpm install
pnpm dev

# 后端
cd ../chat2db-server
mvn clean install
mvn spring-boot:run
```

## 适用场景
- 快速写 SQL：用自然语言描述需求，生成 SQL 后微调即可。
- 排查问题：让 AI 解释 SQL、提示潜在性能风险。
- 数据分析：小团队/个人快速搭建数据查询台。

## 参考链接
- GitHub: https://github.com/chat2db/Chat2DB
