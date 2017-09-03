# 16. 故障记录报告

Date: 20/04/2017

## Status

Accepted

## Context

事故频发，处理速度慢，流程不清晰，并且一直未做记录，导致同样的问题会再次复现。

## Decision

定义故障报告模板：

1. 对故障进行描述，以便查询并对我们的系统稳定性做评估；
2. 对故障做分析，便于未来可快速处理同样问题；
3. 加监控，以便问题出现前就做处理；
4. 解决并升级方案，完全避免此类问题。

## Consequences

### 故障报告模板

#### 问题描述

* 简单的故障描述（三句话即可）
* 故障出现及恢复时间
* 影响范围
* 根本原因

#### 时间线

 * 故障通知时间
* 各种为了恢复服务的操作时间（注意顺序）

#### 原因分析

* 详细的故障描述
* 客观，不要添加粉饰性的内容

#### 做错的事情

#### 做对的事情

#### 将来如何避免此类事情再次发生

* 监控
* 规范
* 预估

Refs:
Outage Post-Mortem – June 14 [https://www.pagerduty.com/blog/outage-post-mortem-june-14/][1]
How to write an Incident Report / Postmortem [https://sysadmincasts.com/episodes/20-how-to-write-an-incident-report-postmortem][2]

[1]:	https://www.pagerduty.com/blog/outage-post-mortem-june-14/
[2]:	https://sysadmincasts.com/episodes/20-how-to-write-an-incident-report-postmortem
