# 26. 文件服务与业务服务隔离

Date: 06/05/2017

## Status

Accepted

## Context

1. 当前存储方案有 3 种（FastDFS, nginx static, OSS），各自分别维护，人力成本高，都是单点，资源有效性无法保障；
2. 文件存储和业务服务共享服务器资源（CPU, 内存，带宽，磁盘 IO），服务器资源使用不合理，文件服务会占用大量内存和磁盘 IO 及网络 IO，影响业务，并且业务服务无法做高可用，遇到 DDOS 只能傻眼；
3. 面向用户的资源无法做加速；
4. 所有文件都是公开可访问，存在严重的安全问题（用户身份证照片、合同及报表数据的泄露）。
5. 所有敏感信息可被任何人全网下载；

## Decision

1. 将所有文件存储和业务机器分离，将 FastDFS 配置单独机器提供服务；
2. 所有静态文件集中上云，录音，电子合同等静态文件上云；
3. 文件分权限访问，分配临时 token 去获取文件；
4. css/js/images 等上云并配置 CDN，加速用户端访问。

## Consequences

综合考虑了 Aliyun OSS 及七牛云，最终选择 OSS 是因为我们的服务都是基于 Aliyun ECS 的，使用 OSS 内网数据同步速度会快很多，并且内网通讯不收费。

1. 本地文件迁移至 Aliyun OSS （使用 ossimport2）注意事项：
	* 宿主机内存消耗量大，磁盘读 IO 很高；
	* 需要写脚本进行文件比对，确认所有文件都同步成功。
2. FastDFS 迁移注意事项：
	* 同过配置多节点来进行新机器得同步；
	* 新机器需要 IO 优化的磁盘，否则整个数据同步瓶颈将在写磁盘操作上。

Refs:

* ossimport2 Linux平台使用说明 [https://help.aliyun.com/document\_detail/32201.html?spm=5176.doc44075.2.11.I53UPo][1]

[1]:	https://help.aliyun.com/document_detail/32201.html?spm=5176.doc44075.2.11.I53UPo