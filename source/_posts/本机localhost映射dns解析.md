---
title: 本机localhost映射dns解析
date: 2021-11-03 08:42:03
tags: 技术
categories: 常用
---
## 本机localhost映射dns解析

#### 方法
    C:\Windows\System32\drivers\etc目录下找到hosts文件 ， 进入修改
1. 最后一行添加127.0.0.1 空格 写自己的域名映射  
2. 增加后进入cmd命令行窗口输入ipconfig /flushdns刷新dns解析  
3. 此后就可以通过自己写的域名访问自己本机上的域名了

如下：  
    <img src="/images/localhost.png" />

之后你的访问路径就可以是：
    http://mytest.com:8080 相当于 localhost:8080

