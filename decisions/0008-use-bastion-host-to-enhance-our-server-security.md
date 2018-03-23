# 8. 使用堡垒机加强服务器安全

Date: 08/04/2017

## Status

Accepted

## Context

1. 旧文写了为了禁止外网暴力破解，我们将用户名、密码登录方式改为了 ssh key 登录；
2. 为了管理方便，当时只区分了生产 key 和测试 key，内部大家共用 key, 并且有 sudo 权限，导致存在内部风险，而针对每个人手动生成 ssh key 又会有管理上的问题；
3. 每个人需要对所有机器配置 ssh config，使用不方便；
4. 当前成员行为无法区分，有成员在系统上执行了 vim 大文件操作导致系统负载急剧升高，也有成员将系统配置改动导致其他项目运行出现问题，当然也存在数据安全上的问题。

未使用堡垒机时：

![][image-1]

## Decision

目标：简化并统一管理线上服务器的登录并审计操作日志

结构图：

![][image-2]

经过多个堡垒机项目的调研，我们最终选择了 [https://github.com/jumpserver/jumpserver][1]，源于使用人数多，并且项目活跃度高。

Jumpserver v0.4.0 新版本预览 [https://github.com/jumpserver/jumpserver/issues/350][2]

## Consequences

* 0.3 版本的一些弊端导致我们激进的选择了 0.4 版本，此版本处于开发中，存在很多未知问题，并且我们已在之上做二次开发
* 文件下载不方便
* 内网之间文件同步不方便

Refs:

* [https://github.com/huifenqi/arch/blob/master/decisions/0003-use-ssh-key-instead-of-password.md][3]
* [https://skyportblog.com/2015/08/27/the-jump-boxjump-server-is-not-dead-it-is-more-necessary-than-ever/][4]
* [https://www.quora.com/What-is-the-difference-between-a-bastion-host-and-a-VPN-host][5]

[1]:	https://github.com/jumpserver/jumpserver
[2]:	https://github.com/jumpserver/jumpserver/issues/350
[3]:	https://github.com/huifenqi/arch/blob/master/decisions/0003-use-ssh-key-instead-of-password.md
[4]:	https://skyportblog.com/2015/08/27/the-jump-boxjump-server-is-not-dead-it-is-more-necessary-than-ever/
[5]:	https://www.quora.com/What-is-the-difference-between-a-bastion-host-and-a-VPN-host

[image-1]:	files/without-bastion.png
[image-2]:	files/bastion.png