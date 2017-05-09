# 24. Exception and realtime error tracking

Date: 28/04/2017

## Status

Accepted

## Context

1. 用户 A 申请分期业务，咦，出错了，怎么办呢，再试，还是不行，算了，不用了；又或者我报告一下吧，写邮件？；
2. 项目 A 昨晚上线后出现了很多问题，怎么办呢，回滚还是赶快去解决呢？
3. 用户发邮件说使用我们应用时出现错误了，错误描述不清晰，我们和用户沟通下吧，1小时过去了，还是重现不了，那我们去看看日志吧，翻出很久之前的日志，使用二分法慢慢查询，3 个小时过去了，终于定位出错误行啦，但是没有上下文及当时的环境变量等信息。

## Decision

使用 Sentry 对我们线上主要业务做异常监控。

![][image-1]

* 实时通知（sms, email, chat）；
* 可定位具体的代码，包括错误栈信息；
* 包含异常的环境变量信息。
* 可主动上报信息；
* 异常信息会聚合，了解当前异常优先级，避免被异常信息淹没；
* 支持所有主流语言及对应的框架。

	![][image-2]

## Consequences

Refs:

* [使用异常的优势][1];
* [如何正确使用Java异常处理机制][2];
* [Java编码中异常的使用建议][3];

[1]:	http://leaforbook.com/blog/jexception/translate/advantages.html
[2]:	http://leaforbook.com/blog/jexception/original/practical.html
[3]:	http://www.jianshu.com/p/69cd9b7427bf

[image-1]:	files/sentry-console.jpg
[image-2]:	files/sentry-supports.png