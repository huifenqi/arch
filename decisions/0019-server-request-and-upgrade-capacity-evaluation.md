# 19. Server request and upgrade: capacity evaluation

Date: 21/04/2017

## Status

Accepted

## Context

1. 有部分机器， CPU，内存，硬盘，使用率在 90% 左右，还有一些各项配置使用率在 1%左右；
2. 还有一部分机器，他的 CPU，内存，硬盘搭配不合理，CPU 使用率 1%，但内存使用率在 80% 左右；
3. 一些对磁盘读写要求高的服务，使用的是普通云盘；
4. 开发的同学申请机器时，无法提出配置要求，基本靠拍脑门决定。

## Decision

1. 可以开始做些手动的压力测试；
2. 计划由运维人员协助开发人员分析业务各个指标的使用情况，CPU 密集型，内存密集型还是有其他的点。
3. 鉴于 Aliyun ECS 随时可以扩展，可以有低配机器，根据使用情况，进行单指标升级。

## Consequences

Refs

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