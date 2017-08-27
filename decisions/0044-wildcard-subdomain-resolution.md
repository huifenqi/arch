# 44. 泛域名解析

Date: 2017-08-25

## Status

Accepted

## Context

随着会找房平台第三方公寓的入驻，我们需要手动添加大量的公寓二级域名于 DNS 中，如，ayk.huizhaofang.com, jingyu.huizhaofang.com 等。

1. 整个流程依赖域名管理者；
2. DNS 管理控制台维护这些记录很麻烦，并将原有专用域名淹没在大量记录中；
3. 网站做了前后端分离，起始页永远返回状态为 200 的页面。

## Decision

1. DNS 记录添加泛解析；
2. Nginx server name 添加泛解析；
3. 不受约束的泛解析，会使所有子域名返回状态为 200 的页面，导致搜索引擎降权；
4. 使用 `include /path/to/server_names;` 可以通过独立的文件解决此问题，并可对新添加的子域名做 code review；
5. 上面的方案需要每次更改后做 nginx reload；有个想法是通过 lua 从 redis 中获取支持的子域名，进行判断并过滤；

## Consequences

1. `include` 方案：当前最简单，且有审核机制，但运维参与较重，需经常重启 nginx；
2. lua + redis 方案：
	* 每次请求需查询 redis；
	* 需做一个对应的管理系统进行子域名的管理。

Refs:

* How can I set up a catch-all (wildcard) subdomain? [https://www.namecheap.com/support/knowledgebase/article.aspx/597/2237/how-can-i-set-up-a-catchall-wildcard-subdomain][1]
* Server names [http://nginx.org/en/docs/http/server\_names.html][2]
* 谷歌重复内容处理 [https://support.google.com/webmasters/answer/66359][3]
* 百度网址降权 [https://baike.baidu.com/item/网站降权][4]
* nginx泛域名解析，实现多个二级域名 [https://yq.aliyun.com/articles/44682][5]
* SEO Friendly Wildcard DNS Set Up for Apache, IIS, Nginx [http://www.stepforth.com/resources/web-marketing-knowledgebase/set-seo-friendly-wildcard-dns/][6]
* Nginx : thousands of server\_name [https://serverfault.com/questions/405355/nginx-thousands-of-server-name][7]

[1]:	https://www.namecheap.com/support/knowledgebase/article.aspx/597/2237/how-can-i-set-up-a-catchall-wildcard-subdomain
[2]:	http://nginx.org/en/docs/http/server_names.html
[3]:	https://support.google.com/webmasters/answer/66359
[4]:	https://baike.baidu.com/item/%E7%BD%91%E7%AB%99%E9%99%8D%E6%9D%83
[5]:	https://yq.aliyun.com/articles/44682
[6]:	http://www.stepforth.com/resources/web-marketing-knowledgebase/set-seo-friendly-wildcard-dns/
[7]:	https://serverfault.com/questions/405355/nginx-thousands-of-server-name