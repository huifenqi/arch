# 9. 结构化 Django 项目

Date: 10/04/2017

## Status

Accepted

## Context

We have 20+ projects which based on Django, but we don’t have the same structure which make our project hard to read.

We need handle those things:
1. store all apps in one place;
2. support different environments;
3. store project related configs.

## Decision

make a skeleton for django: [https://github.com/huifenqi/django-project-skeleton][1]

## Consequences

1. make all new projects with this skeleton;
2. apply this structure to the old projects when refactoring.

[1]:	https://github.com/huifenqi/django-project-skeleton