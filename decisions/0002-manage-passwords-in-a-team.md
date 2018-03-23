# 2. 团队中的密码管理

Date: 30/03/2017

## Status

Accepted

## Context

![][image-1]

视频链接：[http://v.youku.com/v\_show/id\_XMjk5ODQ3NzA3Mg==.html][1]

工作中我们会使用大量的密码，其中包括服务器，数据库，测试账号，第三方服务（阿里云，Dnspod，应用市场等）。

所有的密码都是分散的管理着，每个人都自行对这几十个密码进行管理与存储，方式各样，word, excel, 在线文档等。

当前存在以下问题：

1. 使用容易记但很不安全的密码，例如，`123456`；
2. 在每一个服务上使用相同的非安全密码；
3. 当团队成员有变动时，密码没有改变；
4. 无加密的将密码存在本地文件或是云笔记中；
5. 通过邮箱或是微信进行密码分享。

我们需要一个工具管理我们的密码，包括如下功能及考虑：

1. 生成复杂密码；
2. 密码被加密后保存；
3. 分发方式安全；
4. 使用起来简单方便；
5. 支持团队分组管理；
6. 需要可存储附件（比如，ssh 公私钥）；
7. 兼容 Win/Mac/Linux;
8. 费用合适。

账号密码作为公司的重要虚拟资产，使用传统的方式会带来极大的风险，我们需要一个有效的管理方法。

## Decision

* LastPass(功能繁杂，使用人数最多，费用 1450 USD / 50 users)
* PassPack(**Chosen**)(功能简单，小众，支持文本段，费用 144 USD / 80 users)
* 1Password(功能简单，使用方式友好，费用 7200 USD / 50 users)

## Consequences

1. PassPack 仅有英文版；
2. 对现有密码的整理与录入，推动大家使用密码管理软件。

Refs:

* How to Manage Passwords in a Team: [https://medium.com/altcademy/how-to-manage-passwords-in-a-team-3ed010bc3ccf][2]

[1]:	http://v.youku.com/v_show/id_XMjk5ODQ3NzA3Mg==.html
[2]:	https://medium.com/altcademy/how-to-manage-passwords-in-a-team-3ed010bc3ccf

[image-1]:	files/heres-why-you-should-stop-memorizing-your-passwords.png