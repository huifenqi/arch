# 37. 通过代理解决白名单问题

Date: 2017-06-07

## Status

Accepted

## Context

1. 我们的支付及财务业务，需要向第三方金融机构发起请求，第三方机构出于安全性考虑，需要将我们的服务器 IP 地址进行报备；
2. 第三方机构较多，针对服务器扩容，更换，报备一次比较麻烦；
3. 第三方机构审核时间不定，1 天到多天不定，关键时刻影响业务。

## Decision

正向代理是一个位于客户端和目标服务器之间的代理服务器(中间服务器)。为了从原始服务器取得内容，客户端向代理服务器发送一个请求，并且指定目标服务器，之后代理向目标服务器转交并且将获得的内容返回给客户端。正向代理的情况下客户端必须要进行一些特别的设置才能使用。

常见场景：

![][image-1]

反向代理正好相反。对于客户端来说，反向代理就好像目标服务器。并且客户端不需要进行任何设置。客户端向反向代理发送请求，接着反向代理判断请求走向何处，并将请求转交给客户端，使得这些内容就好似他自己一样，一次客户端并不会感知到反向代理后面的服务，也因此不需要客户端做任何设置，只需要把反向代理服务器当成真正的服务器就好了。

常见场景：

![][image-2]

方案：

1. 使用正向代理；
	* 这个场景最容易想到的方案，使用起来直观，易懂；
	* 需要每个客户端进行配置，或是在应用中对单个请求做代理配置；
	* 需要维护一个高可用的代理服务，并备案此代理服务器。
2. 使用反向代理。
	* 在我们的服务器上做对方服务的反向代理（听起来有点绕，不直观）
	* 维护简单，就像是我们用 nginx/slb 为对方做了个负载均衡，但配置稍有不同；
```json
server {

     server_name {{ proxy_info.server_name }};
     listen {{ proxy_info.ssl_listen }};

     location / {
         proxy_pass_header Server;
         proxy_pass {{ proxy_info.proxy_url }};
         proxy_redirect off;
         proxy_set_header X-Real-IP $remote_addr;
         proxy_set_header X-Scheme $scheme;
         proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
     }
}
```
* 使用简单，使用方配置本机 hosts 即可，为对方域名和代理 IP 映射。 
3. iptables
	* 类似局域网共享上网；
	* 对 iptables 配置有要求；
	* 目标域名对应的 ip 地址改变，需要更新配置。

最终我们通过 aliyun slb 的4层负载接两台部署了 ss5 的机器提供高可用的代理服务

* 4层（TCP协议）服务中，当前不支持添加进后端云服务器池的ECS既作为Real Server，又作为客户端向所在的负载均衡实例发送请求。
* ss5 启动于内网地址即可
* ss5 配置需关注 AUTHENTICATION 和 AUTHORIZATION

## Consequences

Refs:

1. 云服务器 ECS Linux 系统通过 Squid 配置实现代理上网 [https://help.aliyun.com/knowledge\_detail/41342.html][1]
2. 正向代理与反向代理的区别 [http://www.jianshu.com/p/208c02c9dd1d][2]
3. 设置 iptables 使用linux做代理服务器 [https://www.l68.net/493.html][3]
4. SS5 [http://ss5.sourceforge.net/project.htm][4]

[1]:	https://help.aliyun.com/knowledge_detail/41342.html
[2]:	http://www.jianshu.com/p/208c02c9dd1d
[3]:	https://www.l68.net/493.html
[4]:	http://ss5.sourceforge.net/project.htm

[image-1]:	files/proxy.jpg
[image-2]:	files/reverse-proxy.jpg