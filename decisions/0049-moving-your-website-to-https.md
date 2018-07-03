# 49. 全站 https

Date: 2018-06-27

## Status

Proposed

## Context

0. 客户网络环境不佳，存在流量劫持；使用的第三方服务要求 https；
1. 10+ 主域名，50+ 二级域名；
2. 190+ 项目；
3. 10+ 数据库表；
4. 大量自行托管及第三方资源文件。

## Decision

### why

1. 防止流量劫持，插入广告；
2. 防止账号密码等隐私数据被盗取；
3. 支持 HTML5 API，如用户地理位置，音视频等隐私数据获取；
4. 支持 HTTP/2；
5. Apple，微信等有要求。

### How

1. 了解整个系统，统计使用到的域名及购买什么类型的域名证书；
2. 相关资源支持 https，解决 Mixed Content 问题
	1. 针对此问题，浏览器会提示警告，Android 的 webview 直接无法打开；
	2. 前端页面的外链资源（CSS、JS、图片、音频、字体文件、异步接口、表单 action 地址等等）固定了协议引用(http://, https://)，需更新为(//)；
	3. 后端代码中协议是否为动态的；
		1. 返回接口协议应和请求协议保持一致；
	4. 数据库；
		1. 针对自有资源，应只保存路径信息，协议和域名建议动态补充；
		2. 针对第三方资源，默认保留原地址，跟进需要再做转换，实在不行需要做代理。
	5. 资源文件：确保支持 https。
3. 支持 https；
	1. 移动端适配 https
		1. 针对运营商 DNS 劫持(降低 https 请求成功率)，需支持两种协议，并有动态降级方案；
	 2. nginx proxy + backend server
		1. 需关注 scheme 获取是否正确，注意 log 记录。
	3. 跳转
		1. 先 302 测试 https 全站正常，再 301 跳转；
		2. POST 请求会丢失 body 信息。
	4. 测试
		1. [https://www.ssllabs.com/ssltest/][1]
4. 强制 https；
5. 所有环境均要升级 https；
	1. 除生产外，需要将开发、测试、预发布均进行升级，保持环境的一致性，减少不可预估的问题发生
6. 优化。

## Consequences

1. 性能(访问速度)有降低；
2. 增加系统复杂性；
3. 证书及资源(CDN 等)成本；

Refs:

1. [为什么我们应该尽快升级到 HTTPS？][2]
2. [浅谈推进有赞全站 HTTPS 项目-工程篇][3]
3. [启用全站HTTPS后不仅更安全而且更快 看淘宝是如何做到的][4]
4. [更快更安全的HTTPS 优化总结][5]

[1]:	https://www.ssllabs.com/ssltest/
[2]:	https://imququ.com/post/moving-to-https-asap.html
[3]:	https://juejin.im/post/5aa22db7518825558804fbac
[4]:	https://mp.weixin.qq.com/s?__biz=MzAxNDEwNjk5OQ==&mid=402402866&idx=1&sn=f3fde8ece13d51397c12f1a08713ebeb
[5]:	https://zhuanlan.zhihu.com/p/35233649