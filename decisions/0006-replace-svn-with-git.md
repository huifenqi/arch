# 6. SVN 迁移至 Git

Date: 06/04/2017

## Status

Accepted

## Context

当前我们用的是 SVN 做代码、产品文档、UI 设计图的管理，在此说说其中的代码管理

1. 代码仓库过大，新分支，新Tag 代码都是一份完整的拷贝;
2. 必须联网提交；
3. SVN 代码合并方式低效，目前使用 Beyond Compare 做代码合并，分支使用方式落后；
4. 无法很好的做 code review（只能 patch 或第三方工具）；
5. 面试者看到是这么落后，以此类别其他技术栈，综合理解就是，我能学到啥。

## Decision

使用全球最流行的分布式管理工具 Git 及平台 Github，其特点为分布式，目录结构简单，代码无冗余，可 review with PR。  

### 方式一：  

git svn clone `svn project url` -T trunk

将 SVN 项目的 trunk 转为 git 项目的 master，仅保留了 trunk 分支的提交记录，此方式适用于所有代码都规整到了一个分支，并且不需要其他分支的提交记录。

### 方式二：

使用命令 `https://github.com/nirvdrum/svn2git`，它可以保留所有branch, tags，以及所有分支的提交历史。

svn2git http://svn.example.com/path/to/repo --trunk trunk --tags tag --branches branch

git push --all origin

git push --tags

use `--revision number` to reduce the commit history.

目前生产环境使用的 centos 版本过低，导致 git 也无法升级的处理方法：

yum install http://opensource.wandisco.com/centos/6/git/x86\_64/wandisco-git-release-6-1.noarch.rpm

yum update git

## Consequences

* 工作流的调整

Refs:

* https://help.github.com/articles/what-are-the-differences-between-subversion-and-git/
* http://stackoverflow.com/questions/871/why-is-git-better-than-subversion
* [https://www.atlassian.com/git/tutorials/migrating-overview][1]
* [https://www.atlassian.com/git/tutorials/svn-to-git-prepping-your-team-migration][2]
* [https://www.git-tower.com/learn/git/ebook/cn/command-line/appendix/from-subversion-to-git][3]
* [https://tecadmin.net/how-to-upgrade-git-version-1-7-10-on-centos-6/][4]

[1]:	https://www.atlassian.com/git/tutorials/migrating-overview
[2]:	https://www.atlassian.com/git/tutorials/svn-to-git-prepping-your-team-migration
[3]:	https://www.git-tower.com/learn/git/ebook/cn/command-line/appendix/from-subversion-to-git
[4]:	https://tecadmin.net/how-to-upgrade-git-version-1-7-10-on-centos-6/