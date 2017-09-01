# 32. TCP 长连接高可用

Date: 2017-05-25

## Status

Accepted

## Context

1. 我们的一些智能设备，通过 TCP 和后端进行通信，上报数据及接收指令；
2. 智能设备由第三方提供，我们实现后端服务，当前支持域名和 IP 请求；
3. 随着未来设备数量的增长，我们的单台服务预计将无法满足；
4. 原方案是针对不同批次的智能设备，我们绑定不同的域名，已做客户的负载；
5. 存在设备使用的不可控引起服务端的使用率会存在问题；
6. 服务器出问题后服务的恢复时间受限于 DNS 更新的时间（切换新机器）。

## Decision

![][image-1]

## Consequences

Refs:

* Aliyun 负载均衡 产品概述：[https://help.aliyun.com/document\_detail/27539.html][1]
* Aliyun 负载均衡 基础架构：[https://help.aliyun.com/document\_detail/27544.html][2]
* Aliyun 负载均衡 技术原理浅析：[https://help.aliyun.com/knowledge\_detail/39444.html][3]
* 负载均衡服务TCP端口健康检查成功后返回RST包导致出现大量业务错误日志：[https://help.aliyun.com/knowledge\_detail/39464.html][4]
* 为什么不均衡：[https://help.aliyun.com/document\_detail/27656.html][5]
* [TCP接入层的负载均衡、高可用、扩展性架构][6]

[1]:	https://help.aliyun.com/document_detail/27539.html
[2]:	https://help.aliyun.com/document_detail/27544.html
[3]:	https://help.aliyun.com/knowledge_detail/39444.html
[4]:	https://help.aliyun.com/knowledge_detail/39464.html
[5]:	https://help.aliyun.com/document_detail/27656.html
[6]:	https://mp.weixin.qq.com/s?__biz=MjM5ODYxMDA5OQ==&mid=2651960086&idx=1&sn=70bbe7165ecddc7896767f4503a927fe&chksm=bd2d06ca8a5a8fdc67fcacb169583f53a968fdf623a20395926059d44e6abae6b2e56ff1f9f9&mpshare=1&scene=1&srcid=0525oOPDmXhWJAGYDGCM7ods#rd "TCP接入层的负载均衡、高可用、扩展性架构"

[image-1]:	files/HA-for-TCP-long-connection.png