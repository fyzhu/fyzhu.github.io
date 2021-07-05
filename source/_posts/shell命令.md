---
title: shell命令
date: 2019-09-02 09:26:19
categories:
  - technology
  - Server
tags: shell
---
Bash(Bourne Again Shell)

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
#### 查找文件内容
grep 'test' package.json

#### ln

创建软链接

#### which
