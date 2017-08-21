# 43. 支持过滤的消息队列

Date: 2017-08-18

## Status

Accepted

## Context

最近需要优化这样的场景，我们的合同状态有多种（待完善，待审核，审核通过，审核不通过等），每种状态的改变来自多个地方（中介后台，运营后台，风控系统等），每种状态的处理也来自多个地方（SAAS系统，中介后台，运营系统等），且处理者需要处理的状态不相同；

当前实现方案是：

1. 定时任务，各个系统定时处理状态为 X 的合同(处理不及时)；
2. 使用回调，状态更新时回调至处理者处(扩展不方便)；

## Decision

1. 消息服务(MNS) 主题模型

	![][image-1]

	* 可订阅，并且可以通过 Tag 进行消息过滤；
	* 只支持推送模式，每个消费者需要创建回调接口；
	* 只支持外网地址推送，对内部服务来说，网络耗时太高。
2. 消息服务(MNS) 队列模型

	![][image-2]

	* 根据消费者创建队列，几个消费者就创建几个队列；
	* 生产者根据消费者所需向其队列发送消息，即生产者需要发送相同消息至多个队列；
	* 每增加一个消费者，都需更新所有对应生产者的代码，维护性太低。
3. 消息服务(MNS) 主题+队列模型

	![][image-3]

	* 根据消费者创建队列，几个消费者就创建几个队列；
	* 生产着只需向主题队列发送消息，<del>消费者队列订阅所有主题队列的消息</del>；
	* <del>消费者需要接收所有消息，并在业务逻辑中过滤出自己需要处理的消息</del>；
	* 消费者队列可以按 tag 进行过滤；
	* 消费者完整消费自己的队列即可。
4. 消息队列(ONS) MQ

	![][image-4]

	* 总共只需一个 topic 队列，各个消费者通过 Tag 进行过滤；
	* 完美支持我们的使用场景；
	* 不提供 Python SDK。

## Consequences

* 方案 1，2 不用考虑；
* 使用方案 3，所有消费者需要处理所有的消息；
* 使用方案 4，需先实现其 SDK。

![][image-5]

官方不建议用方案 4，我们尝试调试也不顺畅，所以决定使用方案 3。

Refs:

* 消息服务 [https://help.aliyun.com/document\_detail/27414.html][1]
* 广播拉取消息模型 [https://help.aliyun.com/document\_detail/34483.html][2]

[1]:	https://help.aliyun.com/document_detail/27414.html
[2]:	https://help.aliyun.com/document_detail/34483.html

[image-1]:	files/mns-topic.gif
[image-2]:	files/mns-queue.jpg
[image-3]:	files/pub-sub-with-mns.png
[image-4]:	files/message-filter.png
[image-5]:	files/ons-mq-from-ali-workorder.png