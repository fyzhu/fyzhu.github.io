---
title: shell命令
date: 2019-09-02 09:26:19
categories:
  - technology
  - Server
tags: shell
---
Bash(Bourne Again Shell)

#### 查看文件夹大小
du -sh

#### 新建文件
touch xxx

#### cp -f 不起作用
默认cp命令是有别名(alias cp='cp -i')的,无法强制覆盖,即使你用 -f 参数也无法强制覆盖文件。
##### 加个反斜杠，可以使用 \cp 执行 cp 命令时不走 alias
```bash
\cp -rf 
```
-r 文件夹
-f 强制覆盖，不提示
##### 临时取消 cp 的alias
```bash
unalias cp
cp a /test/a
```

#### scp
scp 是 secure copy的缩写, scp是linux系统下基于ssh登陆进行安全的远程文件拷贝命令。
scp [可选参数] file_source file_target 
```bash
scp -r ./dist/* root@ip:/www/wwwroot/jd.dreamlist.cn/
```

#### ssh
```
ssh root@ip
```
#### ssh-copy-id
此功能是把当前主机的 id_rsa.pub copy 到目标主机的 authrized_keys 里，从而实现无密码登录目标主机
```
ssh-copy-id -i ~/.ssh/id_rsa.pub root@dreamlist.cn
```
#### tail & head
```
-n<行数> 显示文件的尾部 n 行内容
tail test.log -n 30

```
#### chown
#### chmod
给 sh 文件可执行权限
```
chmod ugo+x deploy.sh
```
#### 查看文件属性

```bash
lsattr .user.ini
```
#### 修改文件属性

```bash
chattr -i .user.ini
```
#### 查找文件内容
grep 'test' package.json

#### ln

创建链接

Linux链接分两种，一种被称为硬链接（Hard Link），另一种被称为符号链接（Symbolic Link）。默认情况下，ln命令产生硬链接。
##### hard link
ln f1 f2 
##### soft link (Symbolic Link)
ln -s f1 f3

##### list
ls -li   # -i参数显示文件的inode节点信息


#### which

#### 显示行号
set nu

#### 查看端口占用
sudo lsof -i :8080
#### 杀死进程
sudo kill -9 进程pid

#### nohup
英文全称 no hang up（不挂起），用于在系统后台不挂断地运行命令，退出终端不会影响程序的运行。
```
nohup Command [ Arg … ] [　& ]
```
Command：要执行的命令。

Arg：一些参数，可以指定输出文件。

&：让命令在后台执行，终端退出后命令仍旧执行。
#### 查看ip
ifconfig | grep "inet " | grep -v 127.0.0.1

#### 进程相关
##### ps
ps -ef & ps aux  
-ef是System V展示风格，而aux是BSD风格。 

##### top
按P – 以 CPU 占用率大小的顺序排列进程列表

按M – 以内存占用率大小的顺序排列进程列表
参考：
https://www.runoob.com/linux/linux-command-manual.html

top & ps

https://www.cnblogs.com/tudachui/p/9516009.html