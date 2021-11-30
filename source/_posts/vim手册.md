---
title: vim手册
categories:
  - 未分类
date: 2021-06-16 10:23:24
tags:
---
### 模式

1. normal
   
2. insert
   1. i insert 前插
   2. a append 后插
   3. o open a line below
   4. I 开头
   5. A 末尾
   6. O open a line up
3. command
   1. 替换 :% s/java/python/g
   2. set nu 设置行号
   3. sp 横分屏 vs 竖分屏
4. visual
   1. v
   2. V 整行
   3. ctrl + v 块状

### vim 手册
vimtutor

### 插入模式下

ctrl+h 删除上一个字符

ctrl+w 删除上一个单词

​ctrl+u 删除当前行光标之前的内容

### motions
1. hjkl
2. wb move word by word
3. WB move WORD by WORD
4. e/ge
5. E/gE
6. f(character) find in line
7. F(character)
8. t(character) until
9. T(character)
10. ; / , 继续搜索
11. 0 first character of a line
12. ^ first non-blank character of a line
13. $ end character of a line
14. g_ end non-blank character of a line
15. { / } move entire paragraphs
16. ctrl + d / ctrl + u
17. /{pattern} search forward
18. ?{pattern} search backward
19. n / N 搜索上一个/下一个
20. ? without a pattern change the direction
21. gg top of a file
22. {line}gg
23. G end of a file

### operators
1. u to undo
2. ctrl + r to redo
