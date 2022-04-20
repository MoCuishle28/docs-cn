---
title: TiDB 5.2.4 Release Notes
category: Releases
---

# TiDB 5.2.4 Release Notes

发版日期：2022 年 4 月 xx 日

TiDB 版本：5.2.4

## 兼容性更改

+ TiDB

    - (dup: release-5.1.4.md > 兼容性更改> TiDB)- 将系统变量 [`tidb_analyze_version`](/system-variables.md#tidb_analyze_version-从-v510-版本开始引入) 的默认值从 `2` 修改为 `1` [#31748](https://github.com/pingcap/tidb/issues/31748)
    - (dup: release-5.3.1.md > 兼容性更改> Tools> TiDB Lightning)- 将 `regionMaxKeyCount` 的默认值从 1_440_000 调整为 1_280_000，以避免数据导入后出现过多空 Region [#30018](https://github.com/pingcap/tidb/issues/30018)

+ Tools

    + Backup & Restore (BR)

        -
        -

## 提升改进

+ TiDB

    -

+ TiKV

    - (dup: release-6.0.0-dmr.md > 提升改进> TiKV)- 通过将 leader 转让给 CDC observer 减少延迟抖动 [#12111](https://github.com/tikv/tikv/issues/12111)
    - (dup: release-6.0.0-dmr.md > 提升改进> TiKV)- 通过减少需要进行清理锁 (Resolve Locks) 步骤的 Region 数量来减少 TiCDC 恢复时间 [#11993](https://github.com/tikv/tikv/issues/11993)

+ PD

    -

+ TiDB Dashboard

    -

+ TiFlash

    -

+ Tools

    + Backup & Restore (BR)

        -

    + Data Migration (DM)

        -

    + TiCDC

        - (dup: release-5.3.1.md > 提升改进> Tools> TiCDC)- 将 Kafka Sink `partition-num` 的默认值改为 3，使 TiCDC 更加平均地分发消息到各个 Kafka partition [#3337](https://github.com/pingcap/tiflow/issues/3337)
        - (dup: release-5.4.0.md > 提升改进> Tools> TiCDC)- 减少 TiKV 节点宕机后 KV client 恢复的时间 [#3191](https://github.com/pingcap/tiflow/issues/3191)
        - (dup: release-6.0.0-dmr.md > 提升改进> Tools> TiCDC)- 在 Grafana 中添加 `Lag analyze` 监控面板 [#4891](https://github.com/pingcap/tiflow/issues/4891)
        - (dup: release-6.0.0-dmr.md > 提升改进> Tools> TiCDC)- 暴露 Kafka producer 配置参数，使之在 TiCDC 中可配置 [#4385](https://github.com/pingcap/tiflow/issues/4385)
        - (dup: release-6.0.0-dmr.md > 提升改进> Tools> TiCDC)- 为 changefeed 重启操作添加指数退避机制 [#3329](https://github.com/pingcap/tiflow/issues/3329)
        - (dup: release-5.4.0.md > 提升改进> Tools> TiCDC)- 减少 "EventFeed retry rate limited" 日志的数量 [#4006](https://github.com/pingcap/tiflow/issues/4006)
        - (dup: release-5.3.1.md > 提升改进> Tools> TiCDC)- 将 `max-message-bytes` 默认值设置为 10M [#4041](https://github.com/pingcap/tiflow/issues/4041)
        - (dup: release-5.3.1.md > 提升改进> Tools> TiCDC)- 增加更多 Promethous 和 Grafana 监控告警参数，包括 `no owner alert`、`mounter row`、`table sink total row` 和 `buffer sink total row` [#4054](https://github.com/pingcap/tiflow/issues/4054) [#1606](https://github.com/pingcap/tiflow/issues/1606)

    + Dumpling

        -

    + TiDB Lightning

        - note 1

    + TiDB Binlog

        - note 1

## Bug 修复

+ TiDB

    - (dup: release-6.0.0-dmr.md > Bug 修复> TiDB)- 修复 Nulleq 函数作用在 Enum 类型上可能出现结果错误的问题 [#32428](https://github.com/pingcap/tidb/issues/32428)
    - (dup: release-5.4.0.md > Bug 修复> TiDB)- 修复 INDEX HASH JOIN 报 `send on closed channel` 的问题 [#31129](https://github.com/pingcap/tidb/issues/31129)
    - (dup: release-5.4.0.md > Bug 修复> TiDB)- 修复并发的列类型变更导致 schema 与数据不一致的问题 [#31048](https://github.com/pingcap/tidb/issues/31048)
    - (dup: release-5.4.0.md > Bug 修复> TiDB)- 修复乐观事务下数据索引可能不一致的问题 [#30410](https://github.com/pingcap/tidb/issues/30410)
    - (dup: release-5.0.6.md > Bug 修复> TiDB)- 修复当 SQL 语句中存在 JSON 类型列与 `CHAR` 类型列连接时，SQL 出错的问题 [#29401](https://github.com/pingcap/tidb/issues/29401)
    - executor: fix pipelined window invalid memory address [#30326](https://github.com/pingcap/tidb/issues/30326)
    - (dup: release-5.0.6.md > Bug 修复> TiDB)- 修复窗口函数在使用事务时，计算结果与不使用事务时的计算结果不一致的问题 [#29947](https://github.com/pingcap/tidb/issues/29947)
    - (dup: release-5.0.6.md > Bug 修复> TiDB)- 修复 SQL 语句中带有 NATURAL JOIN 时，意外报错 `Column 'col_name' in field list is ambiguous` 的问题 [#25041](https://github.com/pingcap/tidb/issues/25041)
    - (dup: release-5.0.6.md > Bug 修复> TiDB)- 修复将 `Decimal` 转为 `String` 时长度信息错误的问题 [#29417](https://github.com/pingcap/tidb/issues/29417)
    - (dup: release-5.0.6.md > Bug 修复> TiDB)- 修复由于 `tidb_enable_vectorized_expression` 设置的值不同（`on` 或 `off`）导致 `GREATEST` 函数返回结果不一致的问题 [#29434](https://github.com/pingcap/tidb/issues/29434)
    - (dup: release-6.0.0-dmr.md > Bug 修复> TiDB)- 修复使用 left join 同时删除多张表数据时可能出现错误结果的问题 [#31321](https://github.com/pingcap/tidb/issues/31321)
    - (dup: release-6.0.0-dmr.md > Bug 修复> TiDB)- 修复 TiDB 可能向 TiFlash 发送重复任务的问题 [#32814](https://github.com/pingcap/tidb/issues/32814)
    - (dup: release-5.3.1.md > Bug 修复> TiDB)- 修复执行查询时报 MPP task list 为空错误的问题 [#31636](https://github.com/pingcap/tidb/issues/31636)
    - (dup: release-5.3.1.md > Bug 修复> TiDB)- 修复 innerWorker panic 导致的 index join 结果错误的问题 [#31494](https://github.com/pingcap/tidb/issues/31494)
    - (dup: release-5.4.0.md > Bug 修复> TiDB)- 修复 `INSERT ... SELECT ... ON DUPLICATE KEY UPDATE` 语句 panic 的问题 [#28078](https://github.com/pingcap/tidb/issues/28078)
    - (dup: release-5.3.1.md > Bug 修复> TiDB)- 修复针对 `Order By` 的优化导致查询结果有误的问题 [#30271](https://github.com/pingcap/tidb/issues/30271)
    - (dup: release-5.1.4.md > Bug 修复> TiDB)- 修复使用 `ENUM` 类型的列进行 Join 时结果可能不正确的问题 [#27831](https://github.com/pingcap/tidb/issues/27831)
    - (dup: release-5.0.6.md > Bug 修复> TiDB)- 修复当 `CASE WHEN` 函数和 `ENUM` 类型一起使用时的崩溃问题 [#29357](https://github.com/pingcap/tidb/issues/29357)
    - (dup: release-5.0.6.md > Bug 修复> TiDB)- 修复 `microsecond` 函数的向量化表达式版本结果不正确的问题 [#29244](https://github.com/pingcap/tidb/issues/29244)

+ TiKV

    -
    - (dup: release-6.0.0-dmr.md > Bug 修复> TiKV)- 修复旧信息造成 TiKV panic 的问题 [#12023](https://github.com/tikv/tikv/issues/12023)
    - (dup: release-6.0.0-dmr.md > Bug 修复> TiKV)- 修复因内存统计指标溢出而造成的间歇性丢包和内存不足 (OOM) 的问题 [#12160](https://github.com/tikv/tikv/issues/12160)
    - (dup: release-6.0.0-dmr.md > Bug 修复> TiKV)- 修复在 Ubuntu 18.04 下进行性能分析会造成 TiKV panic的问题 [#9765](https://github.com/tikv/tikv/issues/9765)
    - (dup: release-6.0.0-dmr.md > Bug 修复> TiKV)- 修复 tikv-ctl 对 `bad-ssts` 结果字符串进行错误匹配的问题 [#12329](https://github.com/tikv/tikv/issues/12329)
    - (dup: release-6.0.0-dmr.md > Bug 修复> TiKV)- 修复 Replica Read 可能违反线性一致性的问题 [#12109](https://github.com/tikv/tikv/issues/12109)
    - (dup: release-6.0.0-dmr.md > Bug 修复> TiKV)- 修复 TiKV 运行 2 年以上可能 panic 的问题 [#11940](https://github.com/tikv/tikv/issues/11940)
    - (dup: release-6.0.0-dmr.md > Bug 修复> TiKV)- 修复开启流量控制且显式设置 `level0_slowdown_trigger` 时出现 QPS 下降的问题 [#11424](https://github.com/tikv/tikv/issues/11424)
    - (dup: release-5.3.1.md > Bug 修复> TiKV)- 修复 cgroup controller 没有被挂载会造成 Panic 的问题 [#11569](https://github.com/tikv/tikv/issues/11569)
    - (dup: release-5.3.1.md > Bug 修复> TiKV)- 修复在已完成重新选举但没有通知被隔离的 Peer 的情况下执行 `Prepare Merge` 会导致元数据损坏的问题 [#11526](https://github.com/tikv/tikv/issues/11526)
    - (dup: release-5.3.1.md > Bug 修复> TiKV)- 修复 TiKV 停止后 Resolved TS 延迟会增加的问题 [#11351](https://github.com/tikv/tikv/issues/11351)
    - (dup: release-5.3.1.md > Bug 修复> TiKV)- 修复在极端情况下同时进行 Region Merge、ConfChange 和 Snapshot 时，TiKV 会出现 Panic 的问题 [#11475](https://github.com/tikv/tikv/issues/11475)
    - (dup: release-5.3.1.md > Bug 修复> TiKV)- 修复 tikv-ctl 无法正确输出 Region 相关信息的问题 [#11393](https://github.com/tikv/tikv/issues/11393)
    - (dup: release-5.0.6.md > Bug 修复> TiKV)- 修复 Decimal 除法计算的结果为 0 时符号为负的问题 [#29586](https://github.com/pingcap/tidb/issues/29586)
    - (dup: release-5.4.0.md > Bug 修复> TiKV)- 修复悲观事务中 prewrite 请求重试在极少数情况下影响数据一致性的风险 [#11187](https://github.com/tikv/tikv/issues/11187)
    - (dup: release-5.3.0.md > Bug 修复> TiKV)- 修复因统计线程监控数据导致的内存泄漏 [#11195](https://github.com/tikv/tikv/issues/11195)

+ PD

    - (dup: release-6.0.0-dmr.md > Bug 修复> PD)- 修复 Region Scatterer 生成的调度缺失部分 Peer 的问题 [#4565](https://github.com/tikv/pd/issues/4565)
    - (dup: release-5.4.0.md > Bug 修复> PD)- 修复热点统计中无法剔除冷热点数据的问题 [#4390](https://github.com/tikv/pd/issues/4390)

+ TiDB Dashboard

    -

+ TiFlash

    - (dup: release-6.0.0-dmr.md > Bug 修复> TiFlash)- 修复 MPP 任务可能永远泄漏线程的问题 [#4238](https://github.com/pingcap/tiflash/issues/4238)
    - (dup: release-6.0.0-dmr.md > Bug 修复> TiFlash)- 修复 `IN` 函数的结果在多值表达式中不正确的问题 [#4016](https://github.com/pingcap/tiflash/issues/4016)
    - (dup: release-6.0.0-dmr.md > Bug 修复> TiFlash)- 修复将 `INT` 类型转换为 `DECIMAL` 类型可能造成溢出的问题 [#3920](https://github.com/pingcap/tiflash/issues/3920)
    - (dup: release-6.0.0-dmr.md > Bug 修复> TiFlash)- 修复日期格式将 `'
'` 处理为非法分隔符的问题 [#4036](https://github.com/pingcap/tiflash/issues/4036)
    - (dup: release-6.0.0-dmr.md > Bug 修复> TiFlash)- 修复在读取工作量大时添加列后可能出现的查询错误 [#3967](https://github.com/pingcap/tiflash/issues/3967)
    - (dup: release-6.0.0-dmr.md > Bug 修复> TiFlash)- 修复将 `DATETIME` 转换为 `DECIMAL` 时结果错误的问题 [#4151](https://github.com/pingcap/tiflash/issues/4151)

+ Tools

    + Backup & Restore (BR)

        -

    + Data Migration (DM)

        -

    + TiCDC

        -
        - (dup: release-5.4.0.md > Bug 修复> Tools> TiCDC)- 修复不支持同步默认值的问题 [#3793](https://github.com/pingcap/tiflow/issues/3793)
        - (dup: release-6.0.0-dmr.md > Bug 修复> Tools> TiCDC)- 修复某些情况下序列对象被错误同步的问题 [#4552](https://github.com/pingcap/tiflow/issues/4552)
        - (dup: release-6.0.0-dmr.md > Bug 修复> Tools> TiCDC)- 修复了 TiCDC 进程在 PD leader 被杀死时的异常退出问题 [#4248](https://github.com/pingcap/tiflow/issues/4248)
        - (dup: release-6.0.0-dmr.md > Bug 修复> Tools> TiCDC)- 修复 MySQL sink 在禁用 `batch-replace-enable` 参数时生成重复 `replace` SQL 语句的错误 [#4501](https://github.com/pingcap/tiflow/issues/4501)
        - (dup: release-5.4.0.md > Bug 修复> Tools> TiCDC)- 修复输出默认列值时的 panic 问题和数据不一致的问题 [#3929](https://github.com/pingcap/tiflow/issues/3929)
        - (dup: release-5.4.0.md > Bug 修复> Tools> TiCDC)- 修复 `mq sink write row` 没有监控数据的问题 [#3431](https://github.com/pingcap/tiflow/issues/3431)
        - (dup: release-5.4.0.md > Bug 修复> Tools> TiCDC)- 修复当 `min.insync.replicas` 小于 `replication-factor` 时不能同步的问题 [#3994](https://github.com/pingcap/tiflow/issues/3994)
        - (dup: release-5.4.0.md > Bug 修复> Tools> TiCDC)- 修复 `mq sink write row` 没有监控数据的问题 [#3431](https://github.com/pingcap/tiflow/issues/3431)
        - (dup: release-5.4.0.md > Bug 修复> Tools> TiCDC)- 修复在移除同步任务后潜在的 panic 问题 [#3128](https://github.com/pingcap/tiflow/issues/3128)
        - (dup: release-5.3.1.md > Bug 修复> Tools> TiCDC)- 修复了 HTTP API 在查询的组件不存在时导致 CDC 挂掉的问题 [#3840](https://github.com/pingcap/tiflow/issues/3840)
        - (dup: release-5.4.0.md > Bug 修复> Tools> TiCDC)- 修复因 checkpoint 不准确导致的潜在的数据丢失问题 [#3545](https://github.com/pingcap/tiflow/issues/3545)

        - (dup: release-5.4.0.md > Bug 修复> Tools> TiCDC)- 修复潜在的同步流控死锁问题 [#4055](https://github.com/pingcap/tiflow/issues/4055)

        - (dup: release-5.3.1.md > Bug 修复> Tools> TiCDC)- 修复人为删除 etcd 任务的状态时导致 TiCDC panic 的问题 [#2980](https://github.com/pingcap/tiflow/issues/2980)
        - (dup: release-5.4.0.md > Bug 修复> Tools> TiCDC)- 修复 DDL 特殊注释导致的同步停止的问题 [#3755](https://github.com/pingcap/tiflow/issues/3755)
        - (dup: release-5.4.0.md > Bug 修复> Tools> TiCDC)- 修复 `config.Metadata.Timeout` 没有正确配置而导致的同步停止问题 [#3352](https://github.com/pingcap/tiflow/issues/3352)
        - (dup: release-5.4.0.md > Bug 修复> Tools> TiCDC)- 修复在某些 RHEL 发行版上因时区问题导致服务无法启动的问题 [#3584](https://github.com/pingcap/tiflow/issues/3584)
        - (dup: release-5.3.1.md > Bug 修复> Tools> TiCDC)- 修复集群升级后 `stopped` 状态的 changefeed 自动恢复的问题 [#3473](https://github.com/pingcap/tiflow/issues/3473)
        - (dup: release-5.4.0.md > Bug 修复> Tools> TiCDC)- 修复不支持同步默认值的问题 [#3793](https://github.com/pingcap/tiflow/issues/3793)
        - (dup: release-5.3.1.md > Bug 修复> Tools> TiCDC)- 修复 MySQL sink 模块出现死锁时告警过于频繁的问题 [#2706](https://github.com/pingcap/tiflow/issues/2706)
        - (dup: release-5.3.1.md > Bug 修复> Tools> TiCDC)- 修复 Canal 和 Maxwell 协议下 TiCDC 没有自动开启 `enable-old-value` 选项的问题 [#3676](https://github.com/pingcap/tiflow/issues/3676)
        - (dup: release-5.3.1.md > Bug 修复> Tools> TiCDC)- 修复 Avro sink 模块不支持解析 JSON 类型列的问题 [#3624](https://github.com/pingcap/tiflow/issues/3624)
        - (dup: release-5.3.1.md > Bug 修复> Tools> TiCDC)- 修复监控 checkpoint lag 出现负值的问题 [#3010](https://github.com/pingcap/tiflow/issues/3010)
        - (dup: release-5.4.0.md > Bug 修复> Tools> TiCDC)- 修复在容器环境中 OOM 的问题 [#1798](https://github.com/pingcap/tiflow/issues/1798)
        - (dup: release-5.0.6.md > Bug 修复> Tools> TiCDC)- 修复执行 DDL 后的内存泄漏的问题 [#3174](https://github.com/pingcap/tiflow/issues/3174)

    + Dumpling

        -

    + TiDB Lightning

        - (dup: release-5.4.0.md > Bug 修复> Tools> TiDB Lightning)- 修复当 TiDB Lightning 没有权限访问 `mysql.tidb` 表时，导入的结果不正确的问题 [#31088](https://github.com/pingcap/tidb/issues/31088)
        - (dup: release-6.0.0-dmr.md > Bug 修复> Tools> TiDB Lightning)- 修复了 checksum 报错 “GC life time is shorter than transaction duration” [#32733](https://github.com/pingcap/tidb/issues/32733)
        - (dup: release-6.0.0-dmr.md > Bug 修复> Tools> TiDB Lightning)- 修复在某些导入操作没有包含源文件时，TiDB Lightning 不会删除 metadata schema 的问题 [#28144](https://github.com/pingcap/tidb/issues/28144)
        - (dup: release-5.1.4.md > Bug 修复> Tools> TiDB Lightning)+ 修复 S3 存储路径不存在时 TiDB Lightning 不报错的问题 [#28031](https://github.com/pingcap/tidb/issues/28031) [#30709](https://github.com/pingcap/tidb/issues/30709)

    + TiDB Binlog

        -