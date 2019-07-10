---
title: php 线程安全和非线程安全的区别
date: 2019-02-18 16:30:18
categories:
  - technology
  - back-end
tags: php
---
如何选择PHP版本（选择线程安全还是非线程安全）：
在Windows下安装PHP，在选择PHP版本上很有讲究。

Windows下的PHP版本分两种：线程安全版本与非线程安全版本。

如果你打算使用IIS，则你可以以ISAPI或FastCGI这两种方式来安装PHP。CGI的方式因为效率低下，故不予考虑。

如果你要在IIS中以FastCGI方式使用PHP，则你应该使用PHP的非线程安全的版本（Non-Thread Safe，NTS）。原因是以FastCGI方式安装PHP时，PHP拥有独立的进程，并且FastCGI是单一线程的，不存在多个线程之间可能引发的相互干扰（这种干扰通常都是由于全局变量和静态变量导致的）。由于省去了线程安全的检查，因此使用FastCGI方式比ISAPI方式的效率更高一些。

如果你要在IIS中以ISAPI的方式使用PHP，则你应该使用PHP的线程安全版本（Thread Safe，TS）。原因是PHP以ISAPI方式安装时，PHP没有独立的进程，而是作为DLL被IIS加载运行的，即是依附于Web服务器进程的。当Web服务器运行在多线程模式下（IIS正是这种情况），PHP自然也就运行在多线程模式下。只要是在多线程模式下运行，就可能存在线程安全问题，因此应选择PHP的线程安全版本。

但在这里还有必要说明一下，尽管Apache本身是线程安全的，同时你也选择了PHP的线程安全版本，但由于一些Apache和PHP下的第三方扩展最初是基于Unix的多进程思想开发出来的，在设计开发时没有考虑线程安全的问题，因此，不排除在这种情况下仍然存在IIS被某些第三方扩展搞崩溃的可能。

如果你打算使用Apache，则你可以以模块、ISAPI、FastCGI这三种方式来安装PHP。CGI的方式因为效率低下，故不予考虑。

如果你要在Apache中以模块方式安装PHP，则你应该使用PHP的线程安全的版本。原因是当PHP作为Apache的模块安装时，PHP没有独立的进程，而是作为模块以DLL的形式被加载到Apache中的，是随Apache的启动而启动的，而Windows下的Apache为多线程工作模式，因此PHP自然也就运行在多线程模式下。因此，这种情况下应使用PHP的线程安全版本。

再来看ISAPI的情况。通常认为ISAPI是配合IIS使用的，因为ISAPI最初就是微软为IIS开发的。但Apache现在也可以通过加载mod_isapi.so模块来实现ISAPI的功能，以允许PHP以ISAPI的方式安装。.so文件是Apache自1.3版本后制定的用于Windows下的模块命名规则，对于Windows下的Apache而言，.so与.dll文件一样，都是动态链接库文件。

当要以ISAPI方式来安装PHP时，通常是加载一个名如phpXisapi.dll的DLL文件，其中的X为阿拉伯数字4、5等等这样子。

但一般不建议在Apache中以ISAPI方式来安装PHP，原因是到目前为止，Apache通过mod_isapi.so模块来实现的ISAPI功能并不完整，并未完整实现微软对ISAPI所制定的全部规范。

同样的，由于以ISAPI方式来安装PHP时，PHP也没有独立的进程，也是作为模块被加载到Apache中的，因此，同样也需要使用PHP的线程安全版本。

如果你要在Apache中以FastCGI方式使用PHP，则同在IIS中使用FastCGI的PHP的情况一样，你应该使用PHP的非线程安全的版本。原因是在Apache中以FastCGI方式安装PHP时，PHP拥有独立的进程，并且FastCGI是单一线程的，故应使用PHP的非线程安全版本以提高性能。


转载自：https://blog.csdn.net/FAST_13469ND/article/details/82048649