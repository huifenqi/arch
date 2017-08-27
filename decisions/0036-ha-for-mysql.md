# 36. 关于 MySQL 高可用

Date: 2017-06-06

## Status

Proposed

## Context

1. 数据库版本 5.1，太旧，性能，安全，主从复制都存在问题；
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

ECS self built MySQL 5.1 to RDS 5.5 with DTS 迁移流程：

1. 在 RDS 中创建原 MySQL 数据库对应的账号(各个项目账号独立)；
2. 更新白名单：添加项目所部署的服务器；
3. 明确数据规模，对同步时间做个预期；
4. 同步（全量 or 增量），明确无延迟状态；
5. 更新数据库连接配置文件；
6. 明确无延迟状态，停服；
7. 确定数据量一致（由预先写好的脚本判断）(1min)；
8. 关闭迁移服务(10s)；
9. 重启服务器（10s）。

6 至 9 步决定我们的停服时间。

鉴于我们使用从库作为迁移的数据源，需更新如下配置：

* log-slave-updates=1
* binlog-format=row

## Consequences

同步过程中出现如下问题，请周知：

1. 判断脚本出问题，未准备好脚本命令；
2. 终端出问题，更改命令麻烦；
3. 配置信息直接在生产环境更改，应走 github 提交；
4. 停服那步影响其他业务；
5. 从库使用者是否受影响，如数据组。

Refs:

* MySQL upgrade from MySQL 5.1 to MySQL 5.5 [http://www.ineedwebhosting.co.uk/blog/mysql-upgrade-from-mysql-5-1-to-mysql-5-5/][1]
* Mysql时间字段格式如何选择，TIMESTAMP，DATETIME，INT？[https://segmentfault.com/q/1010000000121702][2]
* Changes Affecting Upgrades to MySQL 5.5 [https://dev.mysql.com/doc/refman/5.5/en/upgrading-from-previous-series.html][3]
* Aliyun RDS 访问控制 [https://help.aliyun.com/document\_detail/53617.html][4]
* Mysql log\_slave\_updates 参数 [http://www.cnblogs.com/zejin2008/p/4656251.html][5]
* Mysql数据库主从心得整理 [http://blog.sae.sina.com.cn/archives/4666][6]
* 即使删了全库，保证半小时恢复: [http://mp.weixin.qq.com/s?\_\_biz=MjM5ODYxMDA5OQ==&mid=2651959694&idx=1&sn=4ac53b797fca64229901373e793f860a][7]

[1]:	http://www.ineedwebhosting.co.uk/blog/mysql-upgrade-from-mysql-5-1-to-mysql-5-5/
[2]:	https://segmentfault.com/q/1010000000121702
[3]:	https://dev.mysql.com/doc/refman/5.5/en/upgrading-from-previous-series.html
[4]:	https://help.aliyun.com/document_detail/53617.html
[5]:	http://www.cnblogs.com/zejin2008/p/4656251.html
[6]:	http://blog.sae.sina.com.cn/archives/4666
[7]:	http://mp.weixin.qq.com/s?__biz=MjM5ODYxMDA5OQ==&mid=2651959694&idx=1&sn=4ac53b797fca64229901373e793f860a