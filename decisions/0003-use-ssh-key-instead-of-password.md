# 3. use ssh key instead of password

Date: 30/03/2017

## Status

Accepted

## Context

当前我们使用的是用户名、密码方式进行服务器登录，存在以下问题

1. 安全性问题，密码面临被破解的风险；
2. 易用性问题，可以使用第三方软件如，SecureCRT，ZOC7；
3. 无法充分使用 local terminal，如 iTerm2；

### Refs:
* SSH: passwords or keys? [https://lwn.net/Articles/369703/][1]
* Why is SSH key authentication better than password authentication? [https://superuser.com/questions/303358/why-is-ssh-key-authentication-better-than-password-authentication][2]
* Why is using an SSH key more secure than using passwords? [https://security.stackexchange.com/questions/69407/why-is-using-an-ssh-key-more-secure-than-using-passwords][3]

## Decision

禁用用户名、密码登录，使用 ssh key 进行登录

![][image-1]

## Consequences

1. 团队成员使用新方式需要适应；
2. key 的管理需要统一（可能需要引入堡垒机）。

[1]:	https://lwn.net/Articles/369703/
[2]:	https://superuser.com/questions/303358/why-is-ssh-key-authentication-better-than-password-authentication
[3]:	https://security.stackexchange.com/questions/69407/why-is-using-an-ssh-key-more-secure-than-using-passwords

[image-1]:	hack-ssh-key.png