---
title: shell命令
date: 2019-09-02 09:26:19
tags: shell
---
Bash(Bourne Again Shell)

#### cp -f 不起作用
默认cp命令是有别名(alias cp='cp -i')的,无法强制覆盖,即使你用 -f 参数也无法强制覆盖文件。
##### 加个反斜杠，可以使用\cp 执行cp命令时不走alias
```
\cp -rf 
```
-r 文件夹
-f 强制覆盖，不提示
##### 临时取消cp的alias
```
#unalias cp
#cp a /test/a
```

#### scp
scp 是 secure copy的缩写, scp是linux系统下基于ssh登陆进行安全的远程文件拷贝命令。
scp [可选参数] file_source file_target 
```
scp -r ./dist/* root@ip:/www/wwwroot/jd.dreamlist.cn/
```

#### ssh
```
ssh root@ip
```
