# 20. 日志管理

Date: 24/04/2017

## Status

Accepted

## Context

1. 记录位置混乱，有系统默认路径，有自定义路径；
2. 日志未切割，日志一直记录在一个文件中，导致文件巨大；
3. 记录方式有问题，一个请求量不大的服务，每日存在 1G 的日志数据，发现存在将整个 html 写入日志的问题；
4. 日志记录格式不统一，涉及日志规范有 nginx, python 和 java；
5. 不容易访问，需要给开发者提供对应机器的登录与日志查看权限；
6. 使用 grep 等查询方式，上下文使用不方便，查询效率低；
7. 临时的统计需要写一次性的脚本；
8. 无法对异常日志做监控与报警；
9. 归档日志太多，需要定时清理。

附加需求：

1. 日志根据项目区分查看权限；
2. 可报警；
3. 可产生图表。

## Decision

1. 日志记录统一至 /data/logs 目录下，针对每个服务创建日志目录(包括系统服务)，如 nginx;
2. 所有需要文件切割的地方，我们使用系统的 `/etc/logrotate.d`, copy `/etc/logrotate.d/nginx` 的设置进行改动即可。(系统的默认切割时间各个系统不一致，所以我们删除 `/etc/cron.daily/logrotate`，改为在 `/etc/crontab` 加入 `59 23 * * * root /usr/sbin/logrotate /etc/logrotate.conf`(使用日志服务后无需此步));
3. 针对大日志文件进行调研，查看日志内容的必要性；
4. 规范化日志记录格式及内容，格式可以参考 Aliyun 采集方式及常见配置示例 [https://help.aliyun.com/document\_detail/28981.html][1]
5.  使用日志管理服务可用解决如上 5 - 9 的问题。

可选的日志服务：

1. Aliyun 日志服务 (功能强大(复杂)，价格计算复杂，阿里云体系内速度应该快些，服务提供没多久，可用性待验证，展示效果很一般，价格适中)；
2. sumologic (查询功能强大，上下文展示方便，费用高)；
3. logentries (使用很方便，展示效果很棒，上下文展示一般，费用高)；

综合考虑后，选用 Aliyun 日志服务

整体功能强大

![][image-1]

查询功能够用，虽然界面一般

![][image-2]

## Consequences

创建一个项目，然后创建各自服务的日志库，如下

* nginx: nginx-access, nginx-error
* service1: service1-access, service1-log

未来需处理好 Aliyun 子账号与日志的权限关系

Refs:

* How To Configure Logging and Log Rotation in Nginx on an Ubuntu VPS [https://www.digitalocean.com/community/tutorials/how-to-configure-logging-and-log-rotation-in-nginx-on-an-ubuntu-vps][2]

[1]:	https://help.aliyun.com/document_detail/28981.html
[2]:	https://www.digitalocean.com/community/tutorials/how-to-configure-logging-and-log-rotation-in-nginx-on-an-ubuntu-vps

[image-1]:	files/aliyun-log-service.png
[image-2]:	files/aliyun-log-search.png