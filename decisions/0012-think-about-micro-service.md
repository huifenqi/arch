# 12. Think about micro service

Date: 13/04/2017

## Status

Proposed

## Context

1. 已拆分为各种服务（1. 接口不统一、无监控、无统一日志管理）；
2. API 文档管理不够；
3. 服务的部署纯手动；

## Decision

Decision here...

## Consequences

1. 跨语言；
2. 提供 server 和 client 端；
3. 统一上线过程：独立部署、运行、升级；
4. 统一日志记录与审计：第三方日志服务；
5. 统一风格：REST API or RPC;
6. 统一认证和鉴权：权限管理、安全策略；
7. 统一服务测试：调度方式、访问入口；
8. 资源管理（虚拟机、物理机、网络）；
9. 负载均衡：客户端 or 服务端；
10. 注册发现：中心话注册 or hardcode；
11. 监控告警；

## Refs

### Why

* 先把平台做扎实，再来微服务吧 [http://www.infoq.com/cn/articles/how-to-understand-microservice-architecture][1]
* Microservices – Please, don’t [http://basho.com/posts/technical/microservices-please-dont/][2]
* SOA和微服务架构的区别？ [https://www.zhihu.com/question/37808426/answer/93335393][3]

### How

* 一个完整的微服务系统，应该包含哪些功能？[http://www.infoq.com/cn/articles/what-complete-micro-service-system-should-include][4]
* 构建高性能微服务架构 [http://www.infoq.com/cn/articles/building-a-high-performance-micro-service-architecture][5]
* 服务化框架技术选型与京东JSF解密 [http://zhuanlan.51cto.com/art/201612/525719.htm][6]
* 微服务实战：从架构到发布（一）[https://segmentfault.com/a/1190000004634172][7]
* 微服务架构的基础框架选择：Spring Cloud还是Dubbo？ [http://blog.didispace.com/microservice-framework/][8]
* 分布式服务框架之服务化最佳实践 [http://www.infoq.com/cn/articles/servitization-best-practice][9]
* You need to be this tall to use [micro]() services: [https://news.ycombinator.com/item?id=12508655][11]

### 服务注册

* 分布式服务治理的设计问题？ [https://www.zhihu.com/question/51436292/answer/126128311][12]

### REST API vs RPC

* Do you really know why you prefer REST over RPC? [https://apihandyman.io/do-you-really-know-why-you-prefer-rest-over-rpc/][13]
* REST vs JSON-RPC? [http://stackoverflow.com/questions/15056878/rest-vs-json-rpc][14]
* What differentiates a REST web service from a RPC-like one? [http://stackoverflow.com/questions/7410040/what-differentiates-a-rest-web-service-from-a-rpc-like-one][15]

[1]:	http://www.infoq.com/cn/articles/how-to-understand-microservice-architecture
[2]:	http://basho.com/posts/technical/microservices-please-dont/
[3]:	https://www.zhihu.com/question/37808426/answer/93335393
[4]:	http://www.infoq.com/cn/articles/what-complete-micro-service-system-should-include
[5]:	http://www.infoq.com/cn/articles/building-a-high-performance-micro-service-architecture
[6]:	http://zhuanlan.51cto.com/art/201612/525719.htm
[7]:	https://segmentfault.com/a/1190000004634172
[8]:	http://blog.didispace.com/microservice-framework/
[9]:	http://www.infoq.com/cn/articles/servitization-best-practice
[11]:	https://news.ycombinator.com/item?id=12508655
[12]:	https://www.zhihu.com/question/51436292/answer/126128311
[13]:	https://apihandyman.io/do-you-really-know-why-you-prefer-rest-over-rpc/
[14]:	http://stackoverflow.com/questions/15056878/rest-vs-json-rpc
[15]:	http://stackoverflow.com/questions/7410040/what-differentiates-a-rest-web-service-from-a-rpc-like-one