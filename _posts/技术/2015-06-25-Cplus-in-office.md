---
layout: post
title: 初用github
category: 技术
tags: github
keywords: 
description: 
---
话说现在学东西比年轻的时候慢了很多，折腾了两天才把博客搭建起来。

github也是初次接触，还需要多多使用早日熟悉。

##初次上传文件到github

###1.建立仓库什么的就不说了。

###2.clone仓库：
`git clone https://github.com/liuweigg/liuweigg.github.io.git`  
  
clone成功如下：  
Cloning into 'liuweigg.github.io'...  
Warning: Permanently added 'github.com,207.97.227.239' (RSA) to the list of known hosts.  
remote: Counting objects: 3, done.  
remote: Total 3 (delta 0), reused 0 (delta 0)  
Receiving objects: 100% (3/3), done.  
  
这一段我没截上，网上随便找了这么一段，大概是个意思。  

###3.push文件：  
`git add .`  
`git commit -m 'first_commit'`  
`git remote add origin https://github.com/liuweigg/liuweigg.github.io.git`  
`git push origin master`  

如果执行git remote add origin https://github.com/liuweigg/liuweigg.github.io.git，出现错误：  
fatal: remote origin already exists  
则执行以下语句：  
`git remote rm origin`  
再往后执行git remote add origin https://github.com/liuweigg/liuweigg.github.io.git 即可。  
  
在执行git push origin master时，报错：  
error:failed to push som refs to.......  
则执行以下语句：  
`git pull origin master`  
  
先把远程服务器github上面的文件拉先来，再push 上去。   

###有用的资料
【1】[关于初学者上传文件到github的方法](http://blog.csdn.net/steven6977/article/details/10567719)
