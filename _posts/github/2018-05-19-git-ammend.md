---
layout: post
title:  "git 重命名commit message"
date:   2018-05-19 10:14:00 +0800
categories: git
tags: 
---


## 修改最后一次提交

`git commit` 提供了`amend`参数来修改`commit messaeg`：

```bash
git commit --amend
```

## 修改历史提交

不过上面那种方法只能修改最后一次提交信息。如果需要更改历史提交，则需要先rebase：


```bash
# 输入rebase命令，3代表要修改当前版本倒数第三次的状态
git rebase -i HEAD~3
```

然后控制台会出现类似于下面的内容

```bash
pick:*******
pick:*******
pick:*******
```

其中每行代表一次提交，将需要修改的那次提交的`pick`改成`edit`，wq保存。

这时通过`git log`可以发现刚才改成pick的那次提交已经被提到了第一个。
所以直接使用`git commit --amend`命令即可修改。

当修改完成后，使用`git rebase --continue`退出rebase，commit就会恢复之前的顺序
