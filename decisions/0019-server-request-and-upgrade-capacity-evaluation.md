# 19. 服务器申请与升级 - 容量评估

Date: 21/04/2017

## Status

Accepted

## Context

1. 部分机器的 CPU，内存，硬盘，使用率均在 90% 左右，另一些机器各项指标使用率在 1% 左右；
2. 部分机器的 CPU，内存，硬盘搭配不合理，CPU 使用率 1%，但内存使用率在 90% 左右；
3. 一些对磁盘读写要求高的服务，使用的是普通云盘，比如，数据库，SVN等；
4. 申请机器时，无法提出配置要求，基本靠拍脑门决定；
5. 对服务的发展没有思考，配置要了 12 个月后才能使用到的配置。

## Decision

1. 压力测试；
2. 分析业务各个指标的使用情况，CPU 密集型，内存密集型还是有其他的特点；
3. 鉴于 Aliyun ECS 随时可以扩展，可以先用低配机器，根据使用情况，进行单指标垂直升级；
4. 水平扩展，即提升了服务的处理能力又做了高可用；
5. 对于不合理的内存使用，要分析自己程序中是否有内存泄漏或大数据加载。

## Consequences

Refs:

* 互联网性能与容量评估的方法论和典型案例 [http://www.jianshu.com/p/fbf56ccb4ebe][1]
* 携程网基于应用的自动化容量管理与评估 [https://zhuanlan.zhihu.com/p/25341948][2]
* 大促活动前团购系统流量预算和容量评估 [http://tech.meituan.com/stress-test-before-promotion.html][3]
* 10个互联网团队应对高压的容量评估与高可用体系:私董会1期 [http://weibo.com/ttarticle/p/show?id=2309403998916147312333][4]
* mysql 性能容量评估 [http://www.cnblogs.com/Aiapple/p/5697912.html][5]

[1]:	http://www.jianshu.com/p/fbf56ccb4ebe
[2]:	https://zhuanlan.zhihu.com/p/25341948
[3]:	http://tech.meituan.com/stress-test-before-promotion.html
[4]:	http://weibo.com/ttarticle/p/show?id=2309403998916147312333
[5]:	http://www.cnblogs.com/Aiapple/p/5697912.html