
---
layout: post
author: eature
published: true
categories: git
tags:
- Git
- 文件上传
---

例如我的提交历史如下
```
commit 58211e7a5da5e74171e90d8b90b2f00881a48d3a
Author: test <test@36nu.com>
Date:   Fri Sep 22 20:55:38 2017 +0800
 
    add d.txt
 
commit 0fb295fe0e0276f0c81df61c4fd853b7a000bb5c
Author: test <test@36nu.com>
Date:   Fri Sep 22 20:32:45 2017 +0800
 
    add c.txt
 
commit 7753f40d892a8e0d14176a42f6e12ae0179a3210
Author: test <test@36nu.com>
Date:   Fri Sep 22 20:31:39 2017 +0800
 
    init
```
假如要删除备注为add c.txt commit为0fb295fe0e0276f0c81df61c4fd853b7a000bb5c的这次提交

首先找到此次提交之前的一次提交的commit7753f40d892a8e0d14176a42f6e12ae0179a3210
执行如下命令
```
git rebase -i  7753f40
```
弹出如下界面(原图丢失，下图类似)
![图片](https://img-blog.csdn.net/20180729151540618?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhaXRobXk1MDk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
将需要删除的提交前面的pick改为drop，然后按照提示保存退出
至此已经删除了指定的commit，可以使用git log查看下