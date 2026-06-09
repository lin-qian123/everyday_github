# Project N.O.M.A.D（Crosstalk-Solutions/project-nomad）项目速览与上手指南

- GitHub: https://github.com/Crosstalk-Solutions/project-nomad
- 更新日期: 2026-03-31（Asia/Shanghai）

## 1. 为什么今天值得跟踪

`project-nomad` 是一个把“离线知识库 + 本地 AI + 教育/地图/数据工具”整合到一台机器上的开源项目，近期在 GitHub 日榜热度很高。

- 热度信号（2026-03-31 抓取）:
  - GitHub 仓库页：`20.2k stars`、`1.9k forks`
  - GitHub Trending 镜像（zdoc）：`4,138 stars today`

## 2. 项目在做什么（核心定位）

官方定位是 `Node for Offline Media, Archives, and Data`：

1. 离线优先知识底座
- 通过 Kiwix 提供离线 Wikipedia/医疗资料/电子书等内容。

2. 本地 AI 问答与检索
- 通过 Ollama + Qdrant 提供本地聊天、文档上传与语义检索（RAG）。

3. 统一管理界面（Command Center）
- 项目本质是一个管理 UI + API，负责安装、编排和更新一组容器化工具。

4. 教育与工具扩展
- 集成 Kolibri（课程）、ProtoMaps（离线地图）、CyberChef（数据处理）、FlatNotes（笔记）等模块。

## 3. 怎么用（可直接执行）

### 3.1 一键安装（Debian/Ubuntu）

```bash
sudo apt-get update && sudo apt-get install -y curl && \
curl -fsSL https://raw.githubusercontent.com/Crosstalk-Solutions/project-nomad/refs/heads/main/install/install_nomad.sh -o install_nomad.sh && \
sudo bash install_nomad.sh
```

安装后浏览器打开：

- `http://localhost:8080`
- 或 `http://<你的设备IP>:8080`

### 3.2 Docker Compose 方式（高级用户）

- 使用官方 Docker Compose 模板进行定制后启动：

```bash
docker compose up -d
```

### 3.3 部署建议

1. 先跑最小化部署验证链路（管理台、检索、文档上传）。
2. 再按硬件能力增配模型与知识内容（避免一次性导入导致资源打满）。
3. 若用于断网/应急场景，建议提前完成镜像与知识库预拉取。

## 4. 原理是什么（工程视角）

1. 控制面与数据面分离
- N.O.M.A.D 的 Command Center 负责“安装、编排、升级”；
- 真正能力由各容器服务承担（例如检索、地图、课程、笔记）。

2. 本地化 RAG 闭环
- 文档进入向量索引（Qdrant）后，由本地模型（Ollama）完成检索增强问答；
- 结果不依赖外部云服务即可完成基本知识问答。

3. 离线内容分层
- 基础层：系统与容器编排；
- 资源层：离线百科/课程/地图；
- AI 层：问答、语义搜索、知识增强。

4. 适配“断网可用”场景
- 安装阶段需要网络，但运行阶段可在离线条件下保持核心能力。

## 5. 适用场景

- 远程/野外/应急环境下的知识与 AI 支持。
- 家庭实验室或组织内网的本地 AI 知识节点。
- 需要“可迁移、低外网依赖”的教育与资料系统。

## 6. 风险与边界

1. 硬件门槛
- 最小可运行配置较低，但要获得可用 AI 体验，通常需要更高内存/显卡资源。

2. 内容与合规
- 离线镜像内容需要注意版权与数据更新周期。

3. 安全治理
- 若开放局域网/公网访问，需补齐认证、端口暴露最小化与备份策略。

## 来源

- GitHub 仓库: https://github.com/Crosstalk-Solutions/project-nomad
- GitHub Trending 镜像（today stars）: https://www.zdoc.app/en/trending
