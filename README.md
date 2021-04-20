# hexo

#### 介绍
使用hexo搭建的个人博客
![图解](https://upload-images.jianshu.io/upload_images/1052511-eaa9a57afa53e37a.jpg)
#### 命令
```
hexo s server
hexo clean
hexo g generate
hexo d deploy
```

### 部署
```
hexo d 直接部署 deploy
yarn d 增量部署 generate + deploy
yarn deploy 全新部署 clean + generate + deploy
```
### 备注
1. 收集所有需要登录的用户的公钥（id_rsa.pub）文件，把所有公钥导入到 /home/git/.ssh/authorized_keys 文件内，一行一个。
2. 网站部署在 /www/wwwroot/www.zhuyunfeng.com 下给与文件夹 777 权限 chmod -R 777 * ，更换为 www 用户 chown www:www -R www.zhuyunfeng.com ，给与.git 目录 777 权限，不然报错 error: cannot open .git/FETCH_HEAD: Permission denied
3. git 仓库 git@dreamlist.cn:/home/git/hexo.git

### 最新方法
```
git --work-tree=/www/wwwroot/zhuyunfeng.com --git-dir=/home/git/hexo.git checkout -f
```
使用此方法不会有 git 权限问题，确保 /www/wwwroot/zhuyunfeng.com 文件夹目录为 777 就可以
