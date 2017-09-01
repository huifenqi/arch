# 22. 防 DDOS 攻击

Date: 28/04/2017

## Status

Accepted

## Context

1. DDOS 导致业务全线中断，购买高防 IP ，仍然需要重启机器进行 IP 更换（nginx 和业务系统在同一台机器上）；
2. 入口过多，针对 DDOS，需要多线解决；
3. 机器出问题，业务中断，单点；
4. 新功能部署，业务中断，没有对多实例进行管理，每次都是杀掉所有，然后重新启动。

## Decision

* 入口收敛，保证对外只有一个域名；
* 做业务服务的高可用；
* 使用 slb + nginx 做高可用，并且在遭遇 DDOS 攻击时，可以通过切换 slb 低成本的解决 DDOS；
* 使用 supervisor 进行任务管理，可逐步进行服务实例的重启。

## Consequences

需要保证所有业务机器都是无状态的，即无数据库（mysql, redis, mongodb 等服务在此机器运行），没有用这台机器存储业务用的文件等。

Refs:

* 防 DDOS 攻击 [http://baike.baidu.com/item/防DDOS攻击][1]
* 负载均衡（SLB）使用最佳实践 [https://yq.aliyun.com/articles/80055][2]
* Denial of Service Attack Mitigation on AWS [https://aws.amazon.com/cn/answers/networking/aws-ddos-attack-mitigation/][3]
* How to Help Prepare for DDoS Attacks by Reducing Your Attack Surface [https://aws.amazon.com/cn/blogs/security/how-to-help-prepare-for-ddos-attacks-by-reducing-your-attack-surface/][4]
* Comparing Load Balancing Options: Nginx vs. HAProxy vs. AWS ELB [http://www.mervine.net/comparing-load-balancing][5]

[1]:	http://baike.baidu.com/item/%E9%98%B2DDOS%E6%94%BB%E5%87%BB
[2]:	https://yq.aliyun.com/articles/80055
[3]:	https://aws.amazon.com/cn/answers/networking/aws-ddos-attack-mitigation/
[4]:	https://aws.amazon.com/cn/blogs/security/how-to-help-prepare-for-ddos-attacks-by-reducing-your-attack-surface/
[5]:	http://www.mervine.net/comparing-load-balancing