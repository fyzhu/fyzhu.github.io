---
title: Mac禁止向日葵开机启动
categories:
  - 未分类
date: 2021-06-16 10:15:37
tags:
---
```bash
cd /Library/LaunchAgents
sudo vim com.oray.sunlogin.agent.plist
sudo vim com.oray.sunlogin.startup.plist

cd /Library/LaunchDaemons
sudo vim com.oray.sunlogin.helper.plist
sudo vim com.oray.sunlogin.plist
```
这里，是进入到系统的启动项文件存放目录，然后用vim直接修改向日葵的启动配置。

每次运行vim后，按i进入编辑模式，然后把<key>Disabled</key>从<false/>改为<true/>，这样就禁用了该启动项，然后按Esc退出编辑模式，继续按:wq保存并退出。

编辑好了这四个文件后，再重新启动机器，烦人的向日葵控制端终于消失了！


作者：smartshallot

链接：https://www.jianshu.com/p/a20efbcc61dd

来源：简书

著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
