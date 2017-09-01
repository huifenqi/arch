# 29. 本地 hosts 管理

Date: 18/05/2017

## Status

Accepted

## Context

1. 我们有多个测试环境（开发、测试、预发布及线上）；
2. 我们的客户端为了避免针对不同环境做多次打包，使用了和线上一致的域名，所以当我们的 QA 需要测试不同环境时，需要手动更新每个 QA 的本地 hosts 文件；
3. 由于服务器及对应服务的调整，无法实时做到 hosts 的及时更新，也没法保证每个测试人员都做了更新（当前无通知，出问题后主要依靠问其他 QA 成员或咨询 Dev）；
4. 部分线上服务未配置外网域名，比如 Boss 系统、Wiki 等，需要包括运营人员在内的所有人各自去配置本地 hosts。

## Decision

1. 方案一：使用 SwitchHosts（Chosen）
	* 可快速切换 hosts；
	* 支持集中式的 hosts 管理（在线）；
	* 支持多 hosts 合并；
	* 支持多客户端。

主界面如下，默认会将旧的 hosts 文件保存为 backup

![][image-1]

可以新建 hosts，比如测试环境一

![][image-2]

可以使用远程集中式管理的 hosts

![][image-3]

最重要的是这些 hosts 可以通过同时打开各自开关将其合并使用。

2. 方案二：使用路由器
	* 只需切换不同的路由器即可进行不同环境的测试；
	* 配置办公网络路由器，需要 IT 人员来维护(暂无)；
	* 只能办公室内进行访问。

## Consequences

软件基于 Electron 开发，跨平台，Windows/Mac/Linus 客户端下载地址: [https://pan.baidu.com/share/link?shareid=150951&uk=3607385901#list/path=%2Fshare%2FSwitchHosts!&parentPath=%2Fshare][1]

Refs:

SwitchHosts Github: [https://github.com/oldj/SwitchHosts][2]

[1]:	https://pan.baidu.com/share/link?shareid=150951&uk=3607385901#list/path=/share/SwitchHosts!&parentPath=/share
[2]:	https://github.com/oldj/SwitchHosts

[image-1]:	files/switchhosts.png
[image-2]:	files/switchhosts2.png
[image-3]:	files/remote-hosts.png