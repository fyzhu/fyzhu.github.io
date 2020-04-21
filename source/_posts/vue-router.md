---
title: vue-router的基本使用
categories:
  - 未分类
date: 2020-04-21 14:16:37
tags: vue
---
## 路由跳转
```
// 字符串
this.$router.push('/home/first')

// 对象
this.$router.push({ path: '/home/first' })

// 命名的路由
this.$router.push({ name: 'home', params: { userId: wise }})
```
## 传参
### query
```
http://192.168.1.12:8080/#/detail/?id=123

let id = this.$route.query.id
```
### params
```
{
    path: '/detail/:id/',
    name: 'detail',
    component: detail,
    meta: {
        title: '详情'
    }
}

let id = this.$route.params.id
```

## 监听路由变化

```
watch:{
  $route(to,from){
    console.log(to.path);
  }
}
```