---
title: '使用GitHub来管理博客源文件 '
date: 2016-01-22 20:30:00
tags:
---

使用hexo写博客的一个问题就是源文件都是在本地的，如果换了电脑需要更新博客时就会比较麻烦。正好快要放假回家了，这个问题急需解决。

以前的解决办法是将博客拷到U盘里，但是同步又比较麻烦。使用云盘时每次又提示.git文件不能上传。目前，觉得比较靠谱的办法就是用github来管理了。
<!--more-->
##### 1.建立新的Repository，与hexo博客文件夹同名
##### 2.进入本地博客文件夹，执行 git init
##### 3.设置远程仓库地址 git remote add origin git@github.com:xxx/xxx.git
##### 4.修改.gitignore文件，加入：public/ 和 .deploy/
##### 5.提交到缓存区：git add .
##### 6.提交到本地仓库：git commit -m "xxxxxxxx"
##### 7.推送到远程仓库：git push origin master

现在在任何一台电脑，只需要`git clone <address>`，就可以将hexo的源文件复制到本地了。之后，当写博客后，只需要`git add` .再`git commit -m`再`git push`即可提交到远程仓库。当远程仓库有更新时，使用`git pull`或者`git fetch`就可以同步代码到本地了。
