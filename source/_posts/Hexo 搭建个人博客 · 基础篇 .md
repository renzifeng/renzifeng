---
title: Hexo 搭建个人博客 
date: 2014-05-16 15:30:16 #文章生成时间，一般不改，当然也可以任意修改
categories: #文章分类目录，可以为空，注意:后面有个空格
tags: [blog] #文章标签，可空，多标签请用格[tag1,tag2,tag3],注意:后面有个空格
photos: 
- http://bruce.u.qiniudn.com/2013/11/27/reading/photos-1.jpg
---

# 搭建属于自己的博客

Hexo 是一个轻量的静态博客框架。通过Hexo可以快速生成一个静态博客框架,仅需要几条命令就可以完成,相当方便。

<!--more-->

### 使用hexo生成博客文件

在使用 Hexo 之前，请先安装 Node.js 以及 Git，Node.js 和 Git 都有安装包，可以到官网去下载：

> [Node.js](http://www.nodejs.org/)

> [Git](http://git-scm.com)

另外说明下：因为手头只有一台 Mac，所以下面使用的命令都是在 Mac 终端的，如果使用 Windows 的话，Git 有个 Git Bash 的程序，是一个模拟的终端，可以执行一些命令。
#### 安装 Hexo
前提：必须先安装 Node.js！ 打开终端，执行命令：

``` bash
$ npm install -g hexo-cli
```

Hexo 安装成功之后，在任意目录新建一个子目录并切换到这个目录，这就是本地的博客目录：

``` bash 
$ hexo init <folder>
$ cd <folder>
$ npm install
```

接着安装下依赖

``` bash
$ npm install
$ npm install hexo-renderer-ejs --save
$ npm install hexo-renderer-stylus --save
$ npm install hexo-renderer-marked --save
```
新建完成后，指定文件夹的目录如下：

``` bash
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```

接着修改hexo根目录下_config.yml文件（xxx为你的github账户名称）

``` bash
deploy:
    type: git
    repo: git@github.com:xxx/xxx.github.io.git
    branch: master
    message: 博客迁移测试        #提交的注释内容
```

至此，本地的博客就搭建好了，是不是超简单 ^_^！
然后直接输入以下命令，在本地预览博文

``` bash
$ hexo g   
$ hexo s   // 启动本地服务器
```

然后打开浏览器，在地址栏输入：`localhost:4000`，你就可以喉嗨尚的看到你的博客了～～～

### 托管博客到 Github
尽管在本来浏览器中可已访问自己的博客了，但这仅仅只是一个单机版。如果要在整个互联网上发布直接的博客，需要有服务器托管，下面介绍如果托管直接的 Hexo 博客到 Github 上。

前提：需在 [Github](https://github.com) 上注册！

#### Github的ssh设置
输入以下命令生成ssh的key，引号内是你的github邮箱，如果已经配置完成，同样跳过。

``` bash
$ ssh-keygen -t rsa -C "xxx@xxx.com”
```

如果出现以下提示，直接回车就好

``` bash
$ Generating public/private rsa key pair.
Enter file in which to save the key (/your_home_path/.ssh/id_rsa):
```

接着会显示一下信息，提示你输入两次密码，这个是在提交项目时输入的密码，不想设置的话可以直接回车跳过

``` bash
$ Enter passphrase (empty for no passphrase): [Type a passphrase]
$ Enter same passphrase again: [Type passphrase again]
```

最后如果出现一下信息就表示设置成功

``` bash
$ Your identification has been saved in /your_home_path/.ssh/id_rsa.
$ Your public key has been saved in /your_home_path/.ssh/id_rsa.pub.
$ The key fingerprint is: 01:0f:f4:3b:ca:85:d6:17:a1:7d:f0:68:9d:f0:a2:db your_email@example.com
```

#### 添加SSH key到自己的Github上
1.在完成上一步后，会生成一个.ssh的隐藏文件，这里直接输入以下命令打开后全选复制里面的内容

``` bash
$ cd ~/.ssh
$ open -e id_rsa.pub
```

2.接着登陆github，按照以下步骤

> 1,点击右上角的头像图标 Settings—->SSH keys —-> add SSH keys
> 2,把刚刚复制的内容粘贴到key里，title随便填
> 3,点击add SSH，这就完成了

3.本地测试，直接复制以下命令到命令行回车，不用修改下面的邮箱

```  bash
ssh -T git@github.com
```

如果看到下面的提示，则是提醒你网站证书未验证而已，直接输入yes后回车就行

``` bash
$ The authenticity of host 'github.com (207.97.227.239)' can't be established.
$ RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
$ Are you sure you want to continue connecting (yes/no)?
```

最后看到以下提示，标明ssh的key设置成功

``` bash
$ Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

最后设置一下自己的个人信息，用于push提交内容时记录提交者信息，就完成了，引号内的内容自行修改

```	 bash
$ git config --global user.name "your user_name"
$ git config --global user.email "your_email@example.com"
```


如果查看没问题，直接输入以下命令提交

``` bash
$ hexo d -g
```

注：因为目前用npm下载的hexo是最新的3.x版本，所以在配置完yml文件，执行 hexo deploy后,可能出现 error deployer not found:github 的错误，这时候直接 cd进入生成hexo的博文目录，输入以下命令即可


``` bash
$ npm install hexo-deployer-git --save
```
