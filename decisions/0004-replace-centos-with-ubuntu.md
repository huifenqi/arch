# 4. Ubuntu vs CentOS

Date: 30/03/2017

## Status

Accepted

## Context

 我们的服务器用的都是阿里云的 ECS，历史原因多数操作系统是 centos(6.5)，内部得到的信息是稳定，当然目前阿里云已不提供此版本镜像。

从个人使用经历看，自 10 年那会起，我所经历的公司选用的都是 ubuntu，当然我们应该知其所以然，而不是盲目的接受。

1. centos 系统初始化，软件安装基本都走的是手动编译，效率低，但这点往往被大家作为稳定性的佐证；
2. centos 系统之上的所有软件都过于老旧，想装第三方软件的最新稳定版，很困难（难道一定要手动编译才好）；
3. 从开始使用 ubuntu，就看重他的简单易用，当然当时业界的看法是，不专业，不稳定；
4. ubuntu 的社区比 centos 更活跃，网上的资料也比 centos 多；
5. ubuntu 相关的问题很容易在网上找到解决方案，但 centos 不是。

这些都是自己的使用体验

从主机市场分析数据（[https://www.digitalocean.com/community/questions/whats-is-better-and-why-linux-centos-or-ubuntu?answer=30514][1]）看，Simple Hosting, VPS, Dedicated & Clouds 这三个领域，centos 占有率均低于 ubuntu。尤其在云市场，centos 只有 ubuntu 的 1/20（[http://thecloudmarket.com/stats#/by\_platform\_definition][2]）。

![][image-1]

更多的对比信息请查看：

* CentOS vs Ubuntu: Which one is better for a server [https://thishosting.rocks/centos-vs-ubuntu-server/][3]
* What Linux server should I go for: Ubuntu or CentOS? [https://www.quora.com/What-Linux-server-should-I-go-for-Ubuntu-or-CentOS][4]

## Decision

逐步将系统从 centos 切换至 ubuntu，保证系统的一致，为后期的运维自动化做准备。

## Consequences

* 手动的编译软件改为 apt-get 安装；
* 如果没有对旧系统，旧软件的某些特性有依赖，最好升级为各个软件的最新稳定版，这对性能和安全都大有好处。

[1]:	https://www.digitalocean.com/community/questions/whats-is-better-and-why-linux-centos-or-ubuntu?answer=30514
[2]:	http://thecloudmarket.com/stats#/by_platform_definition
[3]:	https://thishosting.rocks/centos-vs-ubuntu-server/
[4]:	https://www.quora.com/What-Linux-server-should-I-go-for-Ubuntu-or-CentOS

[image-1]:	files/centos-vs-ubuntu-in-clouds.png