# git使用说明

## 一.安装配置

### 1.安装

> [Git官网(安装全选next)](https://git-scm.com/)

### 2.全局配置

>```git
> git config --global user.name Nono
> git config --gloval user.email 1572307127@qq.com
> ```
> 

### 3.建立SSH协议

+ 打开C:\Users\Administrator\.ssh

> ```git
> ssh-keygen -t rsa -C "1572307127@qq.com"
> ssh -v git@github.com
> ssh-agent -s
> ssh-add ~/.ssh/id_rsa 
> ```
> 

+ 若第四行出错，则修改第四行代码：

> ```git
> eval `ssh-agent -s`
> ssh-add ~/.ssh/id_rsa
> ```
> 

+ 打开生成的id_rsa.pub,复制所有内容至github账号setting下的SSH.下的new key
+ 回到原文件夹

> ```git
> ssh -T git@github.com
> ```
>

## 二.建立远程仓库

### 1.github官网

+ 点击new Repositories



## 三.建立本地仓库并连接远程仓库

+ 打开需要建立本地仓库的文件夹

+ 按照上一步的界面中(or creat...下的)代码输入即可



## 四.git相关操作

+ 上传文件

> ```git
> git add .   //.代表所有文件,可以替换成具体文件
> git commit -m "intro"   //intro为此次上传说明，可替换
> git push -u origin main   //上传到github
>```



+ 还原文件(至上次提交状态)

> ```git
> git checkout HEAD filename   //filename为需要还原的文件名
> ```