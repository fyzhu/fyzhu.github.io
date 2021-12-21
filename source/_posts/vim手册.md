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
2. w/b move word by word
3. W/B move WORD by WORD
4. e/ge move to the end of a word
5. E/gE
6. f(character) find character in line
7. F(character)
8. t(character) until character in line
9. T(character)
10. ; / , 继续搜索
11. 0 first character of a line
12. ^ first non-blank character of a line
13. $ end character of a line
14. g_ end non-blank character of a line
15. { / } move entire paragraphs
16. ctrl + d / ctrl + u
17. ctrl + f / ctrl + b 
18. /{pattern} search forward
19. ?{pattern} search backward
20. n / N next/previous
21. ctrl + o go back
22. ? without a pattern change the direction
23. gg top of a file
24. {line}gg
25. G end of a file

### operators
1. u to undo
2. ctrl + r to redo
3. d delete
   1. d2w delete two words
   2. dt; delete until ;
   3. df; delete until ;(include ;)
   4. d/hello delete until hello
   5. diw
   6. di"/'/`
4. dd delete a complete line
5. D delete from the cursor until the end of the line
6. c change (combine d and i)
7. cc change a complete line
8. C change from the cursor until the end of the line
9. . repeat change
10. y
    1.  y1w copy one word
11. yy copy a complete line
12. Y copy from the cursor until the end of the line
13. p 在当前位置之后
14. P 在当前位置之前

### text-object
1. w word
2. s sentence
3. p paragraph
4. " quotes  special
5. ' single quote special 
6. ` backtick special
7. () b
8. {} B
9. []