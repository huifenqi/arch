# 8. Use bastion host to enhance our server security

Date: 08/04/2017

## Status

Accepted

## Context

1. 上篇文章写了为了禁止外网暴力破解，我们将用户名、密码登录方式改为了 ssh key 登录；
2. 为了管理方便，当时只区分了生产 key 和测试 key，内部大家共用 key, 并且有 sudo 权限，导致存在内部风险，而针对每个人手动生成 ssh key 又会有管理上的问题；
3. 当前成员行为无法区分，有成员在系统上执行了 vim 大文件操作导致系统负载急剧升高，也有成员将系统配置改动导致其他成员命令执行存在问题，当然也会存在数据安全上的问题；

未使用堡垒机：

![][image-1]

使用堡垒机后：

![][image-2]

## Decision

目标：简化并统一管理线上服务器的登录并审计操作日志

结构图：

![][image-3]

Refs:

* [https://skyportblog.com/2015/08/27/the-jump-boxjump-server-is-not-dead-it-is-more-necessary-than-ever/][1]
* [https://www.quora.com/What-is-the-difference-between-a-bastion-host-and-a-VPN-host][2]

经过多个堡垒机项目的调研，我们最终选择了 [https://github.com/jumpserver/jumpserver][3]，源于使用人数多，并且项目活跃度高。

Jumpserver v0.4.0 新版本预览 [https://github.com/jumpserver/jumpserver/issues/350][4]

## Consequences

* 0.3 版本的一些弊端导致我们激进的选择了 0.4 版本，此版本处于开发中，存在很多未知问题，并且我们已在之上做二次开发
* 文件下载不方便
* 内网之间文件同步不方便

[1]:	https://skyportblog.com/2015/08/27/the-jump-boxjump-server-is-not-dead-it-is-more-necessary-than-ever/
[2]:	https://www.quora.com/What-is-the-difference-between-a-bastion-host-and-a-VPN-host
[3]:	https://github.com/jumpserver/jumpserver
[4]:	https://github.com/jumpserver/jumpserver/issues/350

[image-1]:	files/without-bastion.png
[image-2]:	files/with-bastion.png
[image-3]:	files/bastion.png