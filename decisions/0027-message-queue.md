# 27. 消息队列

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
6. ONS 使用起来有些复杂，监控方面的功能确实强大许多，但多数在开发与公测中；
7. 不好的点是各自都加了一些私活，MNS 加了自家的短信服务，ONS 加入了 MQTT 物联网套件，让 Q 看起来不单纯。

## Consequences

使用 MNS 时需要确认以下几点：
* 确认队列模型（支持一对一发送和接收消息）还是主题模型（支持一对多发布和订阅消息，并且支持多种消息推送方式）

	![][image-1]

	![][image-2]

* 队列模型，需关注
	1. 消息接收长轮询等待时间(0-30s)；
	2. 消息最大长度(1K-64K);
	3. 消息存活时间(1min-15day);
	4. 消息延时(0-7day);
	5. 取出消息隐藏时长(1s-12hour);

* 主题模型，需关注
	1. 消息最大长度(1K-64K);
	2. 消息可以加过滤标签；

Refs:

* MNS 产品概述 [https://help.aliyun.com/document\_detail/27414.html?spm=5176.doc51077.6.539.XIqAPd][1]
* 消息服务MNS和消息队列ONS产品对比 [https://help.aliyun.com/document\_detail/27437.html?spm=5176.doc27475.6.655.piX01s][2]
* SDK 下载地址：[https://help.aliyun.com/document\_detail/32305.html][3]
* Python 队列使用手册 [https://help.aliyun.com/document\_detail/32295.html?spm=5176.doc32305.6.667.mnHdf4][4]
* Java 队列使用手册 [https://help.aliyun.com/document\_detail/32449.html?spm=5176.doc32295.6.659.vWCLgJ][5]

[1]:	https://help.aliyun.com/document_detail/27414.html?spm=5176.doc51077.6.539.XIqAPd
[2]:	https://help.aliyun.com/document_detail/27437.html?spm=5176.doc27475.6.655.piX01s
[3]:	https://help.aliyun.com/document_detail/32305.html
[4]:	https://help.aliyun.com/document_detail/32295.html?spm=5176.doc32305.6.667.mnHdf4
[5]:	https://help.aliyun.com/document_detail/32449.html?spm=5176.doc32295.6.659.vWCLgJ

[image-1]:	files/mns-queue.jpg
[image-2]:	files/mns-topic.gif