---
title: Vue2源码
categories:
  - technology
  - front-end
date: 2021-04-20
tags: vue
---
### new Vue 都发生了什么
new vue => init => $mount => compile => render => vnode => patch => DOM

### 响应式原理

#### 依赖收集

#### 依赖触发

#### nextTick

#### 如何实现

```
Object.defineProperty()
```

### Virtural Dom

### 编译原理