---
title: centos下压缩解压.zip文件
url: 20.html
id: 20
categories:
  - 技术
  - 服务器
date: 2017-08-31 14:25:53
tags:
  - centos
---

以下命令均在 /home 目录下操作
```bash
cd /home #进入/home目录
```


1、把 /home 目录下面的 mydata 目录压缩为 mydata.zip
```bash
zip -r mydata.zip mydata #压缩mydata目录
```

2、把 /home 目录下面的 mydata.zip 解压到 mydatabak 目录里面
```bash
unzip mydata.zip -d mydatabak
```

3、把 /home 目录下面的 abc 文件夹和 123.txt 压缩成为 abc123.zip
```bash
zip -r abc123.zip abc 123.txt
```

4、把 /home 目录下面的 wwwroot.zip 直接解压到 /home 目录里面
```bash 
unzip wwwroot.zip
```

5、把 /home 目录下面的 abc12.zip、abc23.zip、abc34.zip 同时解压到 /home 目录里面
```bash
unzip abc\*.zip
```

6、查看把 /home 目录下面的 wwwroot.zip 里面的内容
```bash
unzip -v wwwroot.zip
```

7、验证 /home 目录下面的 wwwroot.zip 是否完整
```bash
unzip -t wwwroot.zip
```

8、把 /home 目录下面 wwwroot.zip 里面的所有文件解压到第一级目录
```bash
unzip -j wwwroot.zip
```
=====================================================
主要参数
-c：将解压缩的结果
-l：显示压缩文件内所包含的文件
-p：与-c参数类似，会将解压缩的结果显示到屏幕上，但不会执行任何的转换
-t：检查压缩文件是否正确
-u：与-f参数类似，但是除了更新现有的文件外，也会将压缩文件中的其它文件解压缩到目录中
-v：执行是时显示详细的信息
-z：仅显示压缩文件的备注文字
-a：对文本文件进行必要的字符转换
-b：不要对文本文件进行字符转换
-C：压缩文件中的文件名称区分大小写
-j：不处理压缩文件中原有的目录路径
-L：将压缩文件中的全部文件名改为小写
-M：将输出结果送到more程序处理
-n：解压缩时不要覆盖原有的文件
-o：不必先询问用户，unzip执行后覆盖原有文件
-P<密码>：使用zip的密码选项
-q：执行时不显示任何信息
-s：将文件名中的空白字符转换为底线字符
-V：保留VMS的文件版本信息
-X：解压缩时同时回存文件原来的UID/GID


原文链接
https://www.cnblogs.com/inzens/articles/4968898.html