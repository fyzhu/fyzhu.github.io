---
title: windows terminal
categories:
  - 未分类
date: 2020-08-19 10:35:43
tags:
---
### 安装 windows Terminal
1. windows 应用商店安装
2. github 下载安装

### 安装 powershell 7
github 下载安装

### 安装字体
安装字体，否则乱码
这里仅推荐一款字体：Fira Code。该字体支持 ligature 连字功能，而且是一款专门为代码显示准备的字体。该字体开源，广受海内外程序员好评！  
下载地址：
https://github.com/tonsky/FiraCode/releases/download/3.1/FiraCode_3.1.zip  
解压  
进入 ttf 文件夹  
双击字体文件安装
#### 配置 windows Terminal
guid 需要生成，文章末尾有生成 guid 的网站
```
// 默认的配置就是我们的新 powershell（重要！！！）
"defaultProfile": "{574e775e-4f2a-5b96-ac1e-a2962a402336}",

{
    // Powershell 7.1.0-preview.6 配置
    "guid": "{574e775e-4f2a-5b96-ac1e-a2962a402336}",
    "hidden": false,
    "name": "pwsh",
    // -nologo 去掉启动时的logo等信息输出
    "commandline": "D:/Program Files/PowerShell/7-preview/pwsh.exe -nologo",
    "icon": "D:/Program Files/PowerShell/7-preview/assets/Powershell_avatar.ico",
    //"source": "Windows.Terminal.PowershellCore",
    // 启动菜单一定要设置为 <.>，否则后面重要的一步将会无效！
    "startingDirectory": ".",
    // 字体
    "fontFace": "Fira Code",
    "fontSize": 11,
    "historySize": 9001,
    "padding": "5, 5, 20, 25",
    "snapOnInput": true,
    "useAcrylic": false,
    // 颜色方案
    // "colorScheme": "Homebrew"
},
```
### 安装 powershell 插件
```
# 1. 安装 PSReadline 包，该插件可以让命令行很好用，类似 zsh
Install-Module -Name PSReadLine -AllowPrerelease -Force

# 2. 安装 posh-git 包，让你的 git 更好用
Install-Module posh-git -Scope CurrentUser

# 3. 安装 oh-my-posh 包，让你的命令行更酷炫、优雅
Install-Module oh-my-posh -Scope CurrentUser
```
### 添加 Powershell 启动参数
```
notepad $PROFILE
```
```

#------------------------------- Import Modules BEGIN -------------------------------
# 引入 posh-git
Import-Module posh-git

# 引入 oh-my-posh
Import-Module oh-my-posh

# 设置 PowerShell 主题
Set-Theme Paradox
#------------------------------- Import Modules END   -------------------------------





#-------------------------------  Set Hot-keys BEGIN  -------------------------------
# 设置 Tab 键补全
# Set-PSReadlineKeyHandler -Key Tab -Function Complete

# 设置 Ctrl+d 为菜单补全和 Intellisense
Set-PSReadLineKeyHandler -Key "Tab" -Function MenuComplete

# 设置 Ctrl+d 为退出 PowerShell
Set-PSReadlineKeyHandler -Key "Ctrl+d" -Function ViExit

# 设置 Ctrl+z 为撤销
Set-PSReadLineKeyHandler -Key "Ctrl+z" -Function Undo

# 设置向上键为后向搜索历史记录
Set-PSReadLineKeyHandler -Key UpArrow -Function HistorySearchBackward

# 设置向下键为前向搜索历史纪录
Set-PSReadLineKeyHandler -Key DownArrow -Function HistorySearchForward
#-------------------------------  Set Hot-keys END    -------------------------------


```

参考：
https://www.cnblogs.com/Rohn/p/12940312.html
https://zhuanlan.zhihu.com/p/137595941
https://blog.csdn.net/WPwalter/article/details/100159481
字体：
https://sspai.com/post/52907
powershell 乱码，vscode 乱码 :
https://zhuanlan.zhihu.com/p/51901035
其他：
guid 生成工具
https://www.qvdv.com/tools/qvdv-guid.html