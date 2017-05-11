# 27. Apply message queue in our system

Date: 10/05/2017

## Status

Accepted

## Context

1. 我们的很多业务都有这个需要，当前的一些定时任务已导致机器的产生瓶颈，很多业务之间的耦合性也很高；
2. 当前只有少量的业务在使用消息队列服务（activeMQ）；
3. activeMQ 对非 java 语言的支持并不友好；
4. 自己需要维护队列服务，做监控，高可用等。

## Decision

我们急需一个多语言支持且可靠的服务可以解决如上问题，即

* 异步解耦
* 削峰填谷

Aliyun 的 MNS 和 ONS 功能的重合导致选择起来很困难，最终选择 MNS 源于以下几点。

1. 支持消息优先级；
2. 可靠性更高；
3. 文档更完善；
4. 服务更成熟；
5. 使用起来简单方便，定时消息不支持这点比较遗憾；
6. ONS 使用起来有些复杂，但监控方面的功能确实强大许多。 

## Consequences

Refs:

* 消息服务MNS和消息队列ONS产品对比 [https://help.aliyun.com/document\_detail/27437.html?spm=5176.doc27475.6.655.piX01s][1]
* SDK 下载地址：[https://help.aliyun.com/document\_detail/32305.html][2]

[1]:	https://help.aliyun.com/document_detail/27437.html?spm=5176.doc27475.6.655.piX01s
[2]:	https://help.aliyun.com/document_detail/32305.html