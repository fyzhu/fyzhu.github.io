---
title: zsh 自动补全、语法高亮插件
categories:
  - 未分类
date: 2021-11-25 17:53:38
tags:
---
在日常使用 zsh 的过程中，如果需要打很多命令，会很麻烦，除了可以使用ctrl+r 的方式来查询历史命令，还可以通过插件的方式来自动匹配命令，提高效率。

语法高亮也是帮助我们不要打错命令的好帮手。

第一步，进入 zsh 插件目录，并 clone 项目到此目录中：
cd "$ZSH_CUSTOM/plugins"
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git
git clone https://github.com/zsh-users/zsh-autosuggestions.git
第二步，配置 .zshrc 文件
... 上面省略
plugins = (git zsh-autosuggestions zsh-syntax-highlighting)
... 下面省略
最后一步，让配置生效
zsh
完成！👍

作者：万有引力万有
链接：https://www.jianshu.com/p/d70f9c4cb47c
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。