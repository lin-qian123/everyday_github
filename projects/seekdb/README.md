<!-- markdownlint-disable MD013 -->

# seekdb

## 定位

seekdb 是 OceanBase 体系中的 AI 检索 / Agent 状态数据库，将向量、全文、结构化和半结构化数据放在同一引擎中。当前 README 强调持续写入后的检索、混合 SQL 和数据库分叉，也提供嵌入式 SDK 与独立服务入口。

2026-10-29 快照：C++ daily +6 stars；API 3,200 stars / 1,040 forks / 502 open issues（含 PR），Apache-2.0。核读主线 `ab7bc71f5da2`；发行首项 v1.4.0（2026-08-27 UTC）。本页能力依据主线文档，不能据此认定该旧发行包含全部功能；未启动数据库、运行 SQL 或复现性能。

## 用法

Python 入门可按 README 选择低层 SQL binding；要求 Python 3.11 及以上。先在独立环境审阅并固定实际包版本：

```bash
python -m pip install pylibseekdb pymysql
```

```python
from contextlib import closing
import pylibseekdb
import pymysql

with closing(pylibseekdb.open("./seekdb.db")) as db:
    with pymysql.connect(database="test", autocommit=True,
                         **db.connection_options()) as connection:
        with connection.cursor() as cursor:
            cursor.execute("SELECT 1 AS value")
            print(cursor.fetchall())
```

路径为数据库目录；先关闭 SQL 连接再释放 runtime。高层 Collection / embedding API 是另一个 pyseekdb 入口，不要混用包名与 API。Node binding 的文档说明会管理独立本地进程，Go 例子还要求 CGO / C 编译器；嵌入式不一定意味着所有工作都在调用进程内。

## 原理

按作者说明，Change Stream 从 redo log 异步更新索引，增量与快照两层 HNSW 共同支持检索；SQL 可把向量距离、全文匹配和标量过滤放入同一计划。`FORK DATABASE` 通过写时复制建立数据分支，再选择合并或丢弃。这里的“sandbox”属于数据库状态分支，不限制 Agent 的操作系统、网络或其他凭据权限。

## 价值

- 为持续写入的 Agent 记忆和检索状态减少多个存储系统间的同步负担。
- 让关系过滤与文本 / 向量检索结合，并沿用 MySQL 驱动生态。
- 数据分叉适合试验分支和回滚研究，但应先明确冲突与保留策略。

## 风险边界

- README 的 QPS、P99 及对其他系统倍数是作者给定工作负载的结果；本轮未核完整配置或复现，不能作通用选型排名。
- 当前主线新能力、v1.4.0、Python / JS / Go 原生 runtime 可能版本不同，兼容性须逐项验证。
- 数据库分支不能撤销已发送邮件、已调用 API 或其他库外副作用；合并策略也要审查覆盖与冲突。
- 本地数据库不自动保证 embedding 在本地完成；选择高层 API / 外部模型后应重新梳理数据出口和费用。
- README 的 Docker 示例发布 2881 / 2886 端口，云端 quickstart 会创建远端实例；本轮没有执行。试用应收窄监听和权限，避免用正式资料直接测试。
- ACID、MySQL 兼容与立即可搜等文档表述，仍需对实际版本、事务隔离、索引时延和异常恢复进行测试。

## 补充建议

用可重放合成集合验证写后可见时延、召回率、P50 / P99、内存与磁盘增长；固定并发、向量维度、索引和对照系统条件。另测 fork / merge 冲突、崩溃恢复及最小数据库账户，分别报告数据隔离与进程权限。

## 参考资料

- [上游仓库](https://github.com/oceanbase/seekdb)、[GitHub API](https://api.github.com/repos/oceanbase/seekdb)。
- [固定 README：SDK、索引、分叉与作者性能声明](https://github.com/oceanbase/seekdb/blob/ab7bc71f5da2e09ad23e86a158201e055b8bd37e/README.md)。
- [Apache-2.0 许可](https://github.com/oceanbase/seekdb/blob/ab7bc71f5da2e09ad23e86a158201e055b8bd37e/LICENSE)、[v1.4.0 发行](https://github.com/oceanbase/seekdb/releases/tag/v1.4.0)。
