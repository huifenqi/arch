# 23. 应用性能监控

Date: 28/04/2017

## Status

Accepted

## Context

1. 服务 A，用户访问搜索页面时，请求了 10 分钟，还没返回内容；
2. 服务 B，这个页面请求怎么有 1000 次数据库查询；
3. 服务 C，这条数据库查询怎么耗时 5 分钟。
4. 我们的这个项目做了半年，使用效果如何呀，哦，页面平均响应时间是 5 秒，啊！；
5. 用户反馈平均需要需要 1 天以上的时间；
6. 测试很难将所有边界场景测试到。

## Decision

使用 Newrelic 对我们线上主要业务做性能监控，包括响应时长、吞吐量、错误率，慢查询，查询分析等，他可以做到实时定位和通知，并指出具体的代码行及 SQL 语句。

## Consequences

Refs:

* New Relic [https://newrelic.com/application-monitoring/features][1]
* 应用性能监控方法一览 [http://www.infoq.com/cn/news/2015/08/monitoring-applications-category][2]

[1]:	https://newrelic.com/application-monitoring/features
[2]:	http://www.infoq.com/cn/news/2015/08/monitoring-applications-category