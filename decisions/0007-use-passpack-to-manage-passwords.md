# 7. 使用 PassPack 进行密码管理

Date: 07/04/2017

## Status

Accepted

## Context

1. 管理员以 company-name 注册付费管理员账号
2. 公司成员在 https://www.passpack.com/ 使用公司邮箱注册免费账号，用户名统一：company-name-username
3. 点击 `People` tab 激活自己的账号，使用相同的用户名
4. 邀请管理员账号
5. 创建或导入自己管理的所有用户名密码，批量 transfer 给 company-name(个人密码也可以用它管理，就无需 transfer 给管理员了)

PassPack 使用介绍：[https://www.passpack.com/getting-started/PasspackGettingStarted_Admin_EN.pdf][1]

## Decision

鉴于管理员一人处理非常琐碎，下放权限至 group owner 可编辑相应密码

用户名命名规范：公司名简称-姓名

Name 命名规范：简单描述所用的服务，用于搜索，层级间使用冒号`:`隔开，例如，`aliyun:oss:contract-doc:ak`

## Consequences

1. 推动各个 team leader 使用并管理；
2. 向 team member 分发密码走这个渠道；
3. 列入新人入职注册项。

[1]:	https://www.passpack.com/getting-started/PasspackGettingStarted_Admin_EN.pdf