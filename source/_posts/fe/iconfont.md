---
title: iconfont 乱码
categories:
  - 未分类
date: 2023-11-08 19:25:13
tags:
---
# 前置知识
[Character encodings: Essential concepts](https://www.w3.org/International/articles/definitions-characters/#charsets)  

UTF-8 uses 1 byte to represent characters in the ASCII set, two bytes for characters in several more alphabetic blocks, and three bytes for the rest of the BMP. Supplementary characters use 4 bytes.

UTF-16 uses 2 bytes for any character in the BMP, and 4 bytes for supplementary characters.

UTF-32 uses 4 bytes for all characters.

In the following chart, the first line of numbers represents the position of a character in the Unicode coded character set. The other lines show the byte values used to represent that character in a particular character encoding.

| |Latin A.	|Hebrew alef.	|Han ideograph AN.	|Chinese ideograph meaning 'stump of tree'.|
|-|-|-|-|-|
|Code point|	U+0041|	U+05D0|	U+597D|	U+233B4|
|UTF-8|	41	|D7 90|	E5 A5 BD|	F0 A3 8E B4|
|UTF-16|	00 41|	05 D0|	59 7D|	D8 4C DF B4|
|UTF-32|	00 00 00 41|	00 00 05 D0|	00 00 59 7D	|00 02 33 B4|

# 乱码原因
以下 css 进行 sass 压缩 
```css
a::before {
  content: '\4e2d' // codepoint
}
b::after {
  content: "\e6df"; // codepoint
}
```
压缩后（为了方便查看，对压缩后的代码进行了格式化）
```css
a::before {
  content '中'
}
b::after {
  content: "";
}
```
源代码 `\4e2d` 占用 5 个字节，压缩后代码 `中` 占用 3 个字节 `E4 B8 AD`

浏览器对压缩后的代码解析可能会出错，把 `中` 按 3 个 codepoint 解析，然后页面中就出现了三个 ascii 码

# 解决方案

css-unicode-loader

# 备注
```js
encodeURI('中') // '%E4%B8%AD' 三位 16 进制
const encoder = new TextEncoder();
const view = encoder.encode("中"); // [228, 184, 173] 三位十进制
'中'.charCodeAt(0).toString(16) // 4e2d codepoint
```



