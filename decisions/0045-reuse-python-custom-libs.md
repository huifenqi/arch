# 45. Python 自建库的复用

Date: 2017-12-06

## Status

Accepted

## Context

我们有多个项目使用 Python 开发，随着项目的发展，大家也写了许多的库，比如，price、sms、mail 等。而其他项目也有这样的需求，当前项目之间是通过拷贝的方式进行复用，不是库还存在项目内独自自行更新。这就导致项目之间所使用的库产生不一致，并重复造了很多的轮子。

## Decision

1. 构建自己的 pypi 服务器；
	* 不只可以解决自建库的复用问题；
	* 也可以将我们的常用库缓存，加速 pip 的安装；
	* 有维护成本。
2. 使用 git 作为 pip 安装包
	* 单 repo 单 package：所有 libs 聚合在一个 package 里，对于大量简单 lib 可行；
	* 单 repo 多 package：分目录构建 package，适合稍微大些的 libs 之间做隔离；
	* 多 repo 多 package：每个 repo 是一个 package，适合大的 lib 库，lib 粒度过细会有库管理问题。
3. 使用 Artifactory，Pro+ 版本才提供 pypi 服务。

鉴于当前 lib 并不多，而且每个 lib 很简单，故选择单 repo 单 package 方案。

## Consequences

* 重构各个 lib，使其兼容每个项目；
* 移出项目自己的 libs，统一安装并使用公共 python-libs

Refs:

* [https://github.com/huifenqi/python-libs/][1]

[1]:	https://github.com/huifenqi/python-libs/