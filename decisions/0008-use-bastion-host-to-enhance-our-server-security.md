# 8. Use bastion host to enhance our server security

Date: 08/04/2017

## Status

Accepted

## Context

1. 上次为了禁止外网暴力破解，我们将用户名、密码方式改为了 ssh key 登录；
2. 为了管理方便，当时只区分了生产 key 和测试 key，内部大家共用 key, 并且有 sudo 权限，导致存在内部风险，而针对每个人手动生成 ssh key 又会有管理上的问题。

未使用堡垒机：

![][image-1]

使用堡垒机后：

![][image-2]

## Decision

目标：简化并统一管理线上服务器的登录并添加操作日志

结构图：

![][image-3]

Refs:

* [https://skyportblog.com/2015/08/27/the-jump-boxjump-server-is-not-dead-it-is-more-necessary-than-ever/][1]
* [https://www.quora.com/What-is-the-difference-between-a-bastion-host-and-a-VPN-host][2]

## Consequences
pass

[1]:	https://skyportblog.com/2015/08/27/the-jump-boxjump-server-is-not-dead-it-is-more-necessary-than-ever/
[2]:	https://www.quora.com/What-is-the-difference-between-a-bastion-host-and-a-VPN-host

[image-1]:	files/without-bastion.png
[image-2]:	files/with-bastion.png
[image-3]:	files/bastion.png