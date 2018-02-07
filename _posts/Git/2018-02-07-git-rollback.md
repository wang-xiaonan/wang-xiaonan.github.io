---
layout: post
title: Git 版本回滚
categories: Git
description: 版本回滚
keywords: 回滚, git
---

> Git 回滚提交代码

这只是 Git 回滚的其中一种，还有其他的方式以后在补充

1. 将本地master定位到要回滚的版本

   - **注意在回滚前记得先备份一下回滚前的分支**

   1. 备份回滚前的分支，可以说是本地和远程同步之后的本地分支
      `git branch master-backup`（备份前确保在要备份的master分支）
   2. 找到要回滚的commit_id
      `git log --oneline `
   3. 本地回滚
      `git reset --hard/--soft commit_id`
      --hard 之前的修改会被git直接删除
      --soft 之前的修改会被存在stage缓冲区
      还有一种是`git revert `，是用一种提交来回滚之前的提交


2. 在git命令行执行（强制将本地版本提交到远程分支）

   `git push -u -f origin master` 