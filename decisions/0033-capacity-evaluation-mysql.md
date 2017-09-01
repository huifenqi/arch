# 33. 容量评估 - MySQL

Date: 2017-05-25

## Status

Accepted

## Context

QPS: 每秒钟查询量。如果每秒钟能处理 100 条查询 SQL 语句，那么 QPS 就约等于 100
TPS: 每秒钟事务处理的数量

## Decision

### 和 MySQL 性能相关的几个指标

* CPU
	* 对于 CPU 密集型的应用，我们需要加快 SQL 语句的处理速度。由于MySQL 的 SQL 语句处理是单线程的，因此我们需要更好的 CPU，而不是更多的cpu
	* 一个 CPU 同时只能处理一条 SQL 语句。所以高并发量的情况下，就需要更多的 CPU 而不是更快的 CPU。
* 内存
	* 把数据缓存到内存中读取，可以大大提高性能。常用的 MySQL 引擎中，MyISAM 把索引缓存到内存，数据不缓存。而InnoDB 同时缓存数据和索引
* 磁盘
	* MySQL 对磁盘 IO 的要求比较高，推荐高性能磁盘设备，比如，Aliyun 就推荐使用其 SSD，而不是普通云盘和高效云盘，当然 SSD 这个介质的可靠性，我们也需要考虑
	* MySQL 实例应该独享，尤其不能和其他磁盘 IO 密集型任务放在一起
* 网络
	* 一般数据库服务都部署在内网，带宽影响不大，避免使用外网连接数据库
	* 外网查询，尤其避免使用 `select *` 进行查询
	* 从库如果跨地域，走外网，则尽量减少从库数量。

### 影响数据库性能的因素及应对方式

* 高并发
	* 数据库连接数被占满
	* 对于数据库而言，所能建立的连接数是有限的，MySQL 中`max_connections` 参数默认值是 100
* 大表
	* 记录行数巨大，单表超过千万行
	* 表数据文件巨大，表数据文件超过10G
	* 影响
		* 慢查询：很难在一定的时间内过滤出所需要的数据
		* DDL 操作、建立索引需要很长的时间：MySQL 版本 \<5.5 建立索引会锁表，\>=5.5 虽然不会锁表但会引起主从延迟
		* 修改表结构需要很长时间锁表：会造成长时间的主从延迟；影响正常的数据操作
	* 处理
		* 分库分表
		* 历史数据归档
* 大事务
	* 运行时间比较长，操作数据比较多的事务
	* 影响
		* 锁定太多数据，造成大量的阻塞和锁超时
		* 回滚时需要的时间比较长
		* 执行时间长，容易造成主从延迟
	* 处理
		* 避免一次处理太多的数据
		* 移出不必要在事务中的select操作

## Consequences

鉴于我们使用了 Aliyun MySQL，他有完善的监控项，CPU、内存、磁盘、连接数及网络流量，关注各个指标并针对其做好报警策略即可

Refs:

* 什么影响了MySQL性能 [http://blog.csdn.net/u011118321/article/details/54694262][1]
* 哪些因素影响了数据库性能 [http://blog.csdn.net/u011118321/article/details/54692454][2]
* Aliyun RDS 产品概述 [https://help.aliyun.com/document\_detail/26092.html][3]
* 使用RDS不得不知的注意事项 [https://help.aliyun.com/knowledge\_detail/41872.html][4]
* 阿里云RDS上的一些概念性记录 [http://www.cnblogs.com/olinux/p/5563584.html][5]

[1]:	http://blog.csdn.net/u011118321/article/details/54694262
[2]:	http://blog.csdn.net/u011118321/article/details/54692454
[3]:	https://help.aliyun.com/document_detail/26092.html
[4]:	https://help.aliyun.com/knowledge_detail/41872.html
[5]:	http://www.cnblogs.com/olinux/p/5563584.html