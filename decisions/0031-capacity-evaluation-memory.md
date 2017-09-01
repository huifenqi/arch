# 31. 容量评估 - 内存

Date: 2017-05-25

## Status

Accepted

## Context

1. 机器内存太小了，需要升级一下；
2. 我们之前公司服务需要用多少多少；
3. Java 程序最大最小堆的指定无标准。

## Decision

* 分析业务场景，明确我们到底需要多少内存，合理的预留1-2倍内存都没有问题；
* 我们的业务目前分别由两种语言实现 Python 及 Java，Java 程序对内存的使用量非常大且监控不直观，为了合理分配内存，我们采取了以下分析方法。
	* 分配的最大内存用完后，GC 频率高且特定时间内无法做到垃圾回收，将会导致 `java.lang.OutOfMemoryError`；
	* OOF，GC 频率及 GC 时间是确定 heap 参数的一个指标；
	* 线上不可能等到 OOF 时，才做升级，这样直接影响了系统的可用性，所以针对 Java 程序，一定要做好压力测试或对 JVM 做好监控（通过 Java VisualVM or JConsole），鉴于我们已用 Newrelic 栈，将有其通知我们服务的状况，Memory Analyzer 可以做更详细的变量级别内存使用查看；
* 内存的不合理使用有：将大文件完整加载至内存，将整个表的数据读取至内存；
* 内存泄漏：微观的有对象的引用问题，宏观的有连接未释放等；
* Xmx 设置后，对系统来说是已使用的，所以我们需要同时关注系统级别和 JVM 级别的内存使用情况。

![][image-1]

## Consequences

这篇文章的缘起是因为我们的一个同事发现自己使用的测试环境内存不够用，导致其他服务无法启动，并要求升级机器配置。当时的测试环境配置是：2核4G。出现问题前的操作是将 Xmx 由 1G 调整为 2G，通过分析发现是程序中加载了一个 7万条数据的大表导致，调整批量加载数据将以原先一半的内存解决此问题。

Refs:

* [Server request and upgrade: capacity evaluation][1]
* Spring Boot Memory Performance: [https://spring.io/blog/2015/12/10/spring-boot-memory-performance][2]
* How to control Java heap size (memory) allocation (xmx, xms)：[http://alvinalexander.com/blog/post/java/java-xmx-xms-memory-heap-size-control][3]
* What are the Xms and Xmx parameters when starting JVMs?：[https://stackoverflow.com/questions/14763079/what-are-the-xms-and-xmx-parameters-when-starting-jvms][4]
* JVM Tuning: Heapsize, Stacksize and Garbage Collection Fundamental：[https://crunchify.com/jvm-tuning-heapsize-stacksize-garbage-collection-fundamental/][5]
* 云监控内存使用率与Linux系统内存占用差异的原因：[https://help.aliyun.com/knowledge\_detail/38849.html][6]

[1]:	0019-server-request-and-upgrade-capacity-evaluation.md
[2]:	https://spring.io/blog/2015/12/10/spring-boot-memory-performance
[3]:	http://alvinalexander.com/blog/post/java/java-xmx-xms-memory-heap-size-control
[4]:	https://stackoverflow.com/questions/14763079/what-are-the-xms-and-xmx-parameters-when-starting-jvms
[5]:	https://crunchify.com/jvm-tuning-heapsize-stacksize-garbage-collection-fundamental/
[6]:	https://help.aliyun.com/knowledge_detail/38849.html

[image-1]:	files/java-memory-investigate.png