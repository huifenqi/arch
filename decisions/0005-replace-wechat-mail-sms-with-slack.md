# 5. Replace wechat mail sms with slack

Date: 31/03/2017

## Status

Accepted

## Context

1. 当前使用 Wechat 作为工作中的沟通工具，工作与生活混合；
2. 各种告警信息需查看邮件，短信或是监控平台；
3. 随着任务管理平台，Bug 管理平台，wiki，文档分享网站，聊天工具的流行，邮件的使用场景越来越小。

## Decision

### Slack 支持的功能

1. **公开与私有的聊天组，聊天组可随时加入或退出**；
2. **消息支持表情回复**；
3. 消息支持收藏；
4. 支持各种文件的分享；
5. **分享的链接支持预览**；
6. 搜索功能强大，可通过快捷方式，搜索同事，消息记录，文件等；
7. 多种程序代码支持高亮；
8. **强大的第三方集成，将所有消息、通知汇聚在一处**，例如，Trello，Github，NewRelic, Sentry，Jenkins 等

### 研发部聊天组设计

1. CI - 用于接收测试结果，测试覆盖率，PR 等信息，也用于发起测试等；
2. Newrelic - 用于接收报警等信息；
3. Sentry - 线上实时错误信息，可根据项目单独拆出来；
4. Team-X - 用于组内沟通，一个 Scrum 组，包括研发，产品及测试；
5. Backend - 用于所有后端人员进行问题咨询及分享；
6. Product - 用于跨 Team 的产品进行沟通与分享；
7. Knowledge - 用于所有研发人员进行沟通与分享；
8. Leads - 私密，用于所有研发 leader 进行沟通；
9. Frontend, UI, Mobile, Devops, QA etc

我们用了如下软件：

* Sentry
* Newrelic
* Redmine
* Teambition
* Confluence
* Github
* Bugly
* FIR.im
* Jenkins
* etc

Slack vs BearyChat:

* Slack 优缺点：
	* 鼻祖
	* 几乎所有常用软件(国外)都有集成
	* 功能完善健壮，公司可信
	* 网络不稳定
	* 国内应用集成一般（Teambiton, 监控宝等）
* BearChat 优缺点：
	* 基本完成了 Slack 的功能
	* 数据的隐私无法保证
	* 服务的可用性无法保证

最终，我们给国产软件(服务)一个机会。

## Consequences

* 大家已习惯使用 Wechat，引入一个新的沟通平台有学习成本。
