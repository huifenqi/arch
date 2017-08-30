# 2. 团队中的密码管理

Date: 30/03/2017

## Status

Accepted

## Context

![][image-1]

视频链接：[http://v.youku.com/v\_show/id\_XMjk5ODQ3NzA3Mg==.html][1]

我们工作中使用的密码有 100 + 左右，其中包括
服务器，数据库，测试账号，第三方服务（阿里云，Dnspod，邮箱，等）

我们所有的密码都是分散的管理着，每个人都自行对这 20 到 100 个密码进行管理，并且方式各种各样。

当前存在以下问题：

1. 使用容易记但很不安全的密码，例如，`123456`；
2. 在每一个服务上使用相同的非安全密码；
3. 当团队成员有变动时，密码没有改变；
4. 无加密的将密码存在本地文件或是云笔记中；
5. 通过邮箱或是微信进行密码分享。

我们需要一个工具管理我们的密码，包括如下功能：

1. 生成复杂密码；
2. 密码被加密后保存；
3. 分发方式安全；
4. 使用起来简单方便；
5. 支持团队分组管理。

Refs:

How to Manage Passwords in a Team: [https://medium.com/altcademy/how-to-manage-passwords-in-a-team-3ed010bc3ccf][2]

## Decision

LastPass(功能繁杂，使用人数最多，费用 1450 USD / 50 users)
PassPack(功能简单，小众，不支持附件，费用 144 USD / 80 users)
1Password(功能简单，使用方式友好，费用 7200 USD / 50 users)

## Consequences

1. 需要考虑兼容性，Win/Mac/Linux;
2. 费用需要考虑；
3. 需要可存储附件（比如，ssh 公私钥）。

[1]:	http://v.youku.com/v_show/id_XMjk5ODQ3NzA3Mg==.html
[2]:	https://medium.com/altcademy/how-to-manage-passwords-in-a-team-3ed010bc3ccf

[image-1]:	files/password-manage.png