---
title: windows terminal
categories:
  - 未分类
date: 2020-08-19 10:35:43
tags:
---
### 注意
terminal 中使用 powershell 可以选择 nerd-fonts 和 powerline fonts 字体  
单独使用 powershell 只能选择 powerline fonts 字体，部分图标可能无法显示   
vscode 中是单独使用 powershell , 但 vscode 可以配置 nerd-fonts 字体  
综上，可以选择一个使用图标比较少的主题 paradox  

### 安装 windows Terminal
1. windows 应用商店安装
2. github 下载安装

### 安装 powershell 7
github 下载安装  
如果继续使用 powershell 5.1  
1. 可能需要 Change the execution policy
```bash
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned
```
2. 升级 PowerShellGet (否则接下来无法安装 PSReadline)
Windows PowerShell 5.1 comes with version 1.0.0.1 of PowerShellGet preinstalled.  
This version of PowerShellGet has a limited features and doesn't support the updated capabilities of the PowerShell Gallery. To be supported, you must update to the latest version.
```
Install-Module -Name PowerShellGet -Force
Exit
```

### 安装 powershell 插件
```
# 1. 安装 PSReadline 包，该插件可以让命令行很好用，类似 zsh
Install-Module -Name PSReadLine -AllowPrerelease -Force

# 2. 安装 posh-git 包，让你的 git 更好用
Install-Module posh-git -Scope CurrentUser

# 3. 安装 oh-my-posh 包，让你的命令行更酷炫、优雅
winget install JanDeDobbeleer.OhMyPosh -s winget
```
### 安装字体
安装字体，否则乱码   

#### nerd-fonts(推荐)
1. 下载安装(推荐)
[nerd fonts 官网](https://www.nerdfonts.com/)
[Meslo下载地址](https://github.com/ryanoasis/nerd-fonts/releases/download/v2.1.0/Meslo.zip) (推荐) 
解压  
进入 ttf 文件夹  
双击字体文件依次安装 或 全选-》右键-》安装
2. 命令安装（beta，需要管理员身份)  
oh-my-posh font install

#### powerline fonts
```bash
git clone https://github.com/powerline/fonts.git
cd .\fonts\
.\install.ps1
cd ..
del .\fonts\ -Recurse -Force
```

### 配置 windows Terminal
1. 可视化界面配置
2. json 文件配置  
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

### 添加 Powershell 启动参数
```bash
notepad $PROFILE # 打开配置文件
```
如果上面代码报错找不到文件，新建一个
```bash
New-Item -Path $PROFILE -Type File -Force
```
```

#------------------------------- Import Modules BEGIN -------------------------------
# 引入 posh-git
Import-Module posh-git

# 初始化 oh-my-posh 并设置 PowerShell 主题
oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\paradox.omp.json" | Invoke-Expression
# oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\jandedobbeleer.omp.json" | Invoke-Expression
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

#-------------------------------  Set Hot-keys END    -------------------------------


```

参考：  
[on-my-posh 官网](https://ohmyposh.dev/)  
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