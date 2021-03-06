---
title: Git分支管理
date: 2018-03-01 14:02:02
tags:
categories: Git
---

几乎每一种版本控制系统都以某种形式支持分支。使用分支意味着你可以从开发主线上分离开来，然后在不影响主线的同时继续工作。

有人把 Git 的分支模型称为"必杀技特性"，而正是因为它，将 Git 从版本控制系统家族里区分出来。

创建分支命令：

```
$ git branch <分支名称>
```

切换分支命令：

```
$ git checkout <分支名称>
```

当你切换分支的时候，Git 会用该分支的最后提交的快照替换你的工作目录的内容， 所以多个分支不需要多个目录。

合并分支命令:

```
$ git merge
```

你可以多次合并到统一分支， 也可以选择在合并之后直接删除被并入的分支。

