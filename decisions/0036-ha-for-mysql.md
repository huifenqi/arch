# 36. HA for MySQL

Date: 2017-06-06

## Status

Proposed

## Context

1. 数据库版本 5.1；
2. 数据库部署在 ECS 上，但磁盘使用的是普通云盘，IOPS 已到阈值（优先级最高）；
3. 数据库一主两从，但无高可用；
4. 业务端使用 IP 连接主数据库。

## Decision

1. 提交 Aliyun 工单，尝试是否能申请下 5.1 版本的 MySQL，迁移数据至 RDS，解决 2，3，4 问题（沟通后，5.1 版本已不再提供，PASS）；
2. 将部分数据库迁移出，缓解当前 MySQL 服务器压力，维护多个数据库实例（并未解决实际问题，PASS，当前压力最终确认是慢查询原因）；
3. ECS 上自建 HA，并启用新的实例磁盘为 SSD，切换新实例为 Master，停掉旧实例（根本问题未解决，技术债一直存在，自行维护仍然存在风险点）；
4. 调研 5.5 和 5.1 的差异，直接迁移自建数据库至 Aliyun RDS MySQL 5.5。

鉴于查看文档后， 5.1 到 5.5 的差异性影响不大，Aliyun 官方也支持直接 5.1 到 5.5 的迁移，所以计划直接迁移至 RDS 的 5.5 版本。

为了杜绝风险：

1. 按业务分数据库分别迁移；
2. 所有迁移先走测试数据库，由 QA 做完整的测试。

## Consequences

Refs:

* MySQL upgrade from MySQL 5.1 to MySQL 5.5 [http://www.ineedwebhosting.co.uk/blog/mysql-upgrade-from-mysql-5-1-to-mysql-5-5/][1]
* Mysql时间字段格式如何选择，TIMESTAMP，DATETIME，INT？[https://segmentfault.com/q/1010000000121702][2]

[1]:	http://www.ineedwebhosting.co.uk/blog/mysql-upgrade-from-mysql-5-1-to-mysql-5-5/
[2]:	https://segmentfault.com/q/1010000000121702