# 21. Redis 使用按业务分离并上云

Date: 26/04/2017

## Status

Accepted

## Context

1. redis server 部署在业务机上，业务与数据存储耦合；
2. 所有业务的数据存在一个 db 0 中，业务之间很容易产生 key 冲突，业务扩展时需顾虑其他业务数据；
3. 单点，业务中存有流程数据，风险比较大；
4. 如果切到独立的机器，资源利用率不高。

## Decision

1. 将自建 redis server 迁移至 aliyun redis 中；
2. 理清业务对 redis 的使用情况，按业务划分指定 redis db index 或 独立 redis 实例；
3. aliyun redis 做了高可用；
4. aliyun 目前可选的范围很多，最小实例是 256M，价格也合理。

使用 aliyun redis 后，额外得到一个数据管理与监控功能功能，如图

![][image-1]

## Consequences

1. 针对缓存数据：

	我们无需做数据迁移，直接指定预分配的 aliyun redis db index 即可；

2. 对于存在需要迁移的数据：

	测试 -\> 更新连接配置 -\> 暂停业务服务 -\> 导入数据(AOF) -\> 启动业务服务

	`redis-cli -h xxx.redis.rds.aliyuncs.com -p 6379 -a xx--pipe < appendonly.aof`

	1. 确保 AOF 已打开（未打开的话，需更新配置及使用 bgrewriteaof 手动触发）；
	2. 当前使用的版本（3.0.4）不支持单 db 导入及 db swap，所以只能将整个 instance 数据导入（对于按 db index 区分的业务，需要注意数据不被搞乱）。

Refs:

* 持久化（persistence）[http://redisdoc.com/topic/persistence.html][1]
* How To Back Up and Restore Your Redis Data on Ubuntu 14.04 [https://www.digitalocean.com/community/tutorials/how-to-back-up-and-restore-your-redis-data-on-ubuntu-14-04][2]
* SWAPDB Redis command [https://news.ycombinator.com/item?id=12707973][3]
* Storing Data with Redis [http://www.mikeperham.com/2015/09/24/storing-data-with-redis/][4]

[1]:	http://redisdoc.com/topic/persistence.html
[2]:	https://www.digitalocean.com/community/tutorials/how-to-back-up-and-restore-your-redis-data-on-ubuntu-14-04
[3]:	https://news.ycombinator.com/item?id=12707973
[4]:	http://www.mikeperham.com/2015/09/24/storing-data-with-redis/

[image-1]:	files/dms-redis-overview.png