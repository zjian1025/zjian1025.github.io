---
title: git常用命令
date: 2021-11-16 19:46:03
tags: git
categories: 常用
---
## 前言  
因为最近工作时，总是会需要到git命令操作，但是本人又不熟悉命令行，每次都要问下度娘，所以还是辛苦点 自己总结一下
***
## 安装git
* Windows:  
官方网站下载https://git-scm.com/download/win安装，下一步下一步就行
* Macos:  
最简单的方法是安装 Xcode Command Line Tools
也可以从官网下载安装 https://git-scm.com/download/mac
**安装完后输入**  

        git --version
出现了如下的版本号就ok
<img src="/images/git-01.png">

***
## Git配置
Git 自带一个 git config 的工具来帮助设置控制 Git 外观和行为的配置变量。
你可以通过以下命令查看所有的配置以及它们所在的文件：
    
    git config --list --show-origin
###### 配置用户信息
    设置你的用户名和邮件地址
    git config --global user.name "John Doe"
    git config --global user.email johndoe@example.com
    检查你的配置
    git config –-list
    检查某一项配置
    git config user.name
    
***
## 使用命令
1. 获取git仓
    **将尚未进行版本控制的本地目录转换为 Git 仓库**

        git init
        git add *.c
        git add LICENSE
        git commit -m 'initial project version'
    **从其它服务器 克隆 一个已存在的 Git 仓库。**

        git clone https://github.com/libgit2/libgit2
    
    **检查当前文件状态**

        git status
    **追踪新文件或者将需要提交的文件放入缓存区，待下一次的提交**

        git add xxx
    **查看未添加到暂存区的文件修改的内容**

        git diff
    **查看暂存区文件的修改**
    
        git diff –staged
    **提交更新**
        
        git commit
    **所有已经跟踪过的文件暂存起来一并提交，跳过git add步骤**

        git commit -a -m 'added new benchmarks'
    **移除文件**

        git rm
    **查看提交历史**

        git log
        git log -p -2
    -p 显示每次提交文件的差异 -2 显示最近两次的提交
    **撤销操作，重新提交（提交完了才发现漏掉了几个文件没有添加，或者提交信息写错了）**

        git commit --amend
    **取消暂存某文件**

        git reset HEAD xxx
    **撤消对文件的修改**

        git checkout – xxx
    **查看远程仓库**

        git remote -v
    **添加远程仓库**

        git remote add pb https://github.com/paulboone/ticgit
    **从远程仓库中抓取与拉取**

        git fetch <remote>
    **推送到远程仓库**

        git push origin master
    **查看某个远程仓库**

        git remote show origin
    **远程仓库的重命名与移除**

        git remote rename pb paul
    **Git 别名**
        
        //输入 git checkout时，只需要输入 git co
        git config --global alias.co checkout
        
    **创建分支**
    
        git branch testing
    **切换分支**

        git checkout testing
    
***

**参考资料**
https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%91%BD%E4%BB%A4%E8%A1%8C

***
