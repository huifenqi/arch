# 34. DNS 笔记

Date: 2017-06-03

## Status

Accepted

## Context

1. 网站被 DDOS 需要考虑切换 DNS 解析；
2. 负载均衡服务切换服务器，需要更新 DNS 解析；
3. 新加子域名，需要配置 DNS 解析。

## Decision

DNS 解析的同步需要时间，涉及以下几点：

1. DNSPod 生效时间，一般在 30s 以内；
2. 各个 ISP DNS 服务器刷新时间；
3. 域名 TTL (用户本地缓存时间）。

针对全球性业务，保险起见，我们等待一天以上。DNSPod 给出的说法是，域名解析通常需 24 小时至 72 小时才能全球完全同步。大多数业务正常情况以 TTL 为依据即可。

## Consequences

一种域名解析更新策略是，现将旧的域名解析 TTL 设为最小值，等待一天，确保解析都已完全同步，这个完全不影响现有业务。将 DNS 解析更新到新的记录，这个时候 DNS 服务器将以最快的速度进行同步更新；确认都更新完毕后，我们将 TTL 设为较长时间，确保 DNS 解析的稳定性。

Refs:

* 有关DNSPod常见问题汇总: [https://www.douban.com/group/topic/26842738/][1]
* DNS解析过程及DNS TTL值: [http://www.xiaoxiaozi.com/2013/04/23/2409/][2]

[1]:	https://www.douban.com/group/topic/26842738/
[2]:	http://www.xiaoxiaozi.com/2013/04/23/2409/