---
title: PHP URL参数获取方式的四种例子
url: 65.html
id: 65
categories:
  - 技术
  - 后端
date: 2017-09-18 13:32:54
tags:
---

这篇文章主要介绍了PHP URL参数获取方式的四种例子,php url参数解析的4种方法,需要的朋友可以参考下

在已知URL参数的情况下，我们可以根据自身情况采用$\_GET来获取相应的参数信息（$\_GET\['name'\]）;那，在未知情况下如何获取到URL上的参数信息呢？ **第一种、利用$_SERVER内置数组变量** 相对较为原始的$\_SERVER\['QUERY\_STRING'\]来获取，URL的参数，通常使用这个变量返回的会是类似这样的数据：name=tank&sex=1 如果需要包含文件名的话可以使用$\_SERVER\["REQUEST\_URI"\](返回类似：/index.php?name=tank&sex=1) **第二种、利用pathinfo内置函数**

复制代码代码如下:

<?php $test = pathinfo("http://localhost/index.php"); print_r($test); /* 结果如下 Array ( \[dirname\] => http://localhost //url的路径 \[basename\] => index.php  //完整文件名 \[extension\] => php  //文件名后缀 \[filename\] => index //文件名 ) */ ?>

**第三种、利用parse_url内置函数**

复制代码代码如下:

<?php $test = parse\_url("http://localhost/index.php?name=tank&sex=1#top"); print\_r($test); /* 结果如下 Array ( \[scheme\] => http //使用什么协议 \[host\] => localhost //主机名 \[path\] => /index.php //路径 \[query\] => name=tank&sex=1 // 所传的参数 \[fragment\] => top //后面根的锚点 ) */ ?>

**第四种、利用basename内置函数**

复制代码代码如下:

<?php $test = basename("http://localhost/index.php?name=tank&sex=1#top"); echo $test; /* 结果如下 index.php?name=tank&sex=1#top */ ?>

另外，还有就是自己通过正则匹配的处理方式来获取需要的值了。这种方式较为精确，效率暂不考虑。。。 下面拓展实践下正则处理方式：

复制代码代码如下:

<?php preg\_match\_all("/(\\w+=\\w+)(#\\w+)?/i","http://localhost/index.php?name=tank&sex=1#top",$match); print_r($match); /* 结果如下 Array ( \[0\] => Array ( \[0\] => name=tank \[1\] => sex=1#top ) \[1\] => Array ( \[0\] => name=tank \[1\] => sex=1 ) \[2\] => Array ( \[0\] => \[1\] => #top ) ) */ ?>

补充 函数dirname() 路途漫漫...还有待继续挖掘... 转载至http://www.jb51.net/article/47396.htm