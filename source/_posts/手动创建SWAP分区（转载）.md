---
title: 手动创建SWAP分区（转载）
url: 239.html
id: 239
categories:
  - technology
  - Server
date: 2018-05-10 14:47:17
tags:
---

大纲

1、swap分区是什么？

2、为什么需要swap分区？

3、关于swap分区大小

4、手动创建swap分区

1、swap分区是什么？

swap，即交换分区，除了安装Linux的时候，有多少人关心过它呢？其实，Swap的调整对Linux服务器，特别是Web服务器以及数据库服务器,如Oracle的性能至关重要。

众所周知，现代操作系统都实现了“虚拟内存”这一技术，不但在功能上突破了物理内存的限制，使程序可以操纵大于实际物理内存的空间，更重要的是，“虚拟内存”是隔离每个进程的安全保护网，使每个进程都不受其它程序的干扰。

Swap 空间的作用可简单描述为：当系统的物理内存不够用的时候，就需要将物理内存中的一部分空间释放出来，以供当前运行的程序使用。那些被释放的空间可能来自一些很长时间没有什么操作的程序，这些被释放的空间被临时保存到Swap空间中，等到那些程序要运行时，再从Swap中恢复保存的数据到内存中。这样，系统总是在物理内存不够时，才进行Swap交换，这就是所谓的“换页”。

2、为什么需要swap分区？

如果系统的物理内存用光了，系统就会跑得很慢，但仍能运行；如果Swap空间用光了，那么系统就会发生错误。例如，Web服务器能根据不同的请求数量衍生出多个服务进程（或线程），如果Swap空间用完，则服务进程无法启动，通常会出现“application is out of memory”的错误，严重时会造成服务进程的死锁。因此Swap空间的分配是很重要的。通常情况下，服务器应用场景中，为安全起见，都会使用swap，防止内存溢出。

3、关于swap分区大小

几乎所有Linux 系统管理的书上或者很多资料上都推荐设置swap交换分区大小为物理内存的2倍。这些建议到了现在就不是那么适用了，现在的服务器动不动就是 16GB/32GB 内存，难道相应的交换分区也要扩大到 32GB/64GB？根据 OpenBSD 的安装建议：

Many people follow an old rule of thumb that your swap partition should be twice the size of your main system RAM. This rule is nonsense. On a modern system, that’s a LOT of swap, most people prefer that their systems never swap. You don’t want your system to ever run out of RAM+swap, but you usually would rather have enough RAM in the system so it doesn’t need to swap. If you are using a flash device for disk, you probably want no swap partition at all. Use what is appropriate for your needs.

再看看 RHEL 5 推荐的 swap 分区大小：

Swap should equal 2x physical RAM for up to 2 GB of physical RAM, and then an additional 1x physical RAM for any amount above 2 GB, but never less than 32 MB. For systems with really large amounts of RAM (more than 32 GB) you can likely get away with a smaller swap partition (around 1x, or less, of physical RAM).

上面说的是一般情况，在安装系统的时候很难决定多大的交换空间，往往需要根据服务器实际负载、运行情况、以及未来可能应用来综合考虑 swap 分区的大小，所以这里参考推荐最小 swap 大小更实际一些：
<pre class="crayon-plain-tag">4GB&nbsp;或&nbsp;4GB&nbsp;以下内存的系统，最小需要&nbsp;2GB&nbsp;交换空间；
大于&nbsp;4GB&nbsp;而小于&nbsp;16GB&nbsp;内存的系统，最小需要&nbsp;4GB&nbsp;交换空间；
大于&nbsp;16GB&nbsp;而小于&nbsp;64GB&nbsp;内存的系统，最小需要&nbsp;8GB&nbsp;交换空间；
大于&nbsp;64GB&nbsp;而小于&nbsp;256GB&nbsp;内存的系统，最小需要&nbsp;16GB&nbsp;交换空间。</pre>

但是不建议超过32G，这样操作系统误认为有很多物理内存，反而导致性能下降。

4、手动创建swap分区

想想以下情况：

*   系统安装时，没有创建swap分区
*   服务器无法添加物理内存，而且swap分区不够用

此时，我们就需要手动的创建或者增大swap分区了。注意，虚拟内存必须是独立的文件系统，那么我们也必须为其提供单独的分区。

**1、创建一个单独的分区，并调整分区类型为Linux swap**
<pre class="crayon-plain-tag">[root@localhost&nbsp;~]#&nbsp;fdisk&nbsp;/dev/sdb&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
Command&nbsp;(m&nbsp;for&nbsp;help):&nbsp;p&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;#&nbsp;打印分区表

Disk&nbsp;/dev/sdb:&nbsp;5368&nbsp;MB,&nbsp;5368709120&nbsp;bytes
255&nbsp;heads,&nbsp;63&nbsp;sectors/track,&nbsp;652&nbsp;cylinders
Units&nbsp;=&nbsp;cylinders&nbsp;of&nbsp;16065&nbsp;*&nbsp;512&nbsp;=&nbsp;8225280&nbsp;bytes

&nbsp;&nbsp;&nbsp;Device&nbsp;Boot&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Start&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;End&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Blocks&nbsp;&nbsp;&nbsp;Id&nbsp;&nbsp;System
/dev/sdb1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;123&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;987966&nbsp;&nbsp;&nbsp;83&nbsp;&nbsp;Linux

Command&nbsp;(m&nbsp;for&nbsp;help):&nbsp;n&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;#&nbsp;创建新分区
Command&nbsp;action
&nbsp;&nbsp;&nbsp;e&nbsp;&nbsp;&nbsp;extended
&nbsp;&nbsp;&nbsp;p&nbsp;&nbsp;&nbsp;primary&nbsp;partition&nbsp;(1-4)
p
Partition&nbsp;number&nbsp;(1-4):&nbsp;2
First&nbsp;cylinder&nbsp;(124-652,&nbsp;default&nbsp;124):&nbsp;
Using&nbsp;default&nbsp;value&nbsp;124
Last&nbsp;cylinder&nbsp;or&nbsp;+size&nbsp;or&nbsp;+sizeM&nbsp;or&nbsp;+sizeK&nbsp;(124-652,&nbsp;default&nbsp;652):&nbsp;+512M

Command&nbsp;(m&nbsp;for&nbsp;help):&nbsp;p

Disk&nbsp;/dev/sdb:&nbsp;5368&nbsp;MB,&nbsp;5368709120&nbsp;bytes
255&nbsp;heads,&nbsp;63&nbsp;sectors/track,&nbsp;652&nbsp;cylinders
Units&nbsp;=&nbsp;cylinders&nbsp;of&nbsp;16065&nbsp;*&nbsp;512&nbsp;=&nbsp;8225280&nbsp;bytes

&nbsp;&nbsp;&nbsp;Device&nbsp;Boot&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Start&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;End&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Blocks&nbsp;&nbsp;&nbsp;Id&nbsp;&nbsp;System
/dev/sdb1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;123&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;987966&nbsp;&nbsp;&nbsp;83&nbsp;&nbsp;Linux
/dev/sdb2&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;124&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;186&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;506047+&nbsp;&nbsp;83&nbsp;&nbsp;Linux

Command&nbsp;(m&nbsp;for&nbsp;help):&nbsp;t&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;#&nbsp;调整分区类型
Partition&nbsp;number&nbsp;(1-4):&nbsp;2
Hex&nbsp;code&nbsp;(type&nbsp;L&nbsp;to&nbsp;list&nbsp;codes):&nbsp;82
Changed&nbsp;system&nbsp;type&nbsp;of&nbsp;partition&nbsp;2&nbsp;to&nbsp;82&nbsp;(Linux&nbsp;swap&nbsp;/&nbsp;Solaris)

Command&nbsp;(m&nbsp;for&nbsp;help):&nbsp;p

Disk&nbsp;/dev/sdb:&nbsp;5368&nbsp;MB,&nbsp;5368709120&nbsp;bytes
255&nbsp;heads,&nbsp;63&nbsp;sectors/track,&nbsp;652&nbsp;cylinders
Units&nbsp;=&nbsp;cylinders&nbsp;of&nbsp;16065&nbsp;*&nbsp;512&nbsp;=&nbsp;8225280&nbsp;bytes

&nbsp;&nbsp;&nbsp;Device&nbsp;Boot&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Start&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;End&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Blocks&nbsp;&nbsp;&nbsp;Id&nbsp;&nbsp;System
/dev/sdb1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;123&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;987966&nbsp;&nbsp;&nbsp;83&nbsp;&nbsp;Linux
/dev/sdb2&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;124&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;186&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;506047+&nbsp;&nbsp;82&nbsp;&nbsp;Linux&nbsp;swap&nbsp;/&nbsp;Solaris

Command&nbsp;(m&nbsp;for&nbsp;help):&nbsp;w&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;#&nbsp;写入到磁盘
The&nbsp;partition&nbsp;table&nbsp;has&nbsp;been&nbsp;altered!

Calling&nbsp;ioctl()&nbsp;to&nbsp;re-read&nbsp;partition&nbsp;table.
Syncing&nbsp;disks.
[root@localhost&nbsp;~]#&nbsp;partprobe&nbsp;/dev/sdb</pre>

OK，/dev/sdb2就是我们新创建的分区。

**2、使用mkswap命令创建swap文件系统**
<pre class="crayon-plain-tag">[root@localhost&nbsp;~]#&nbsp;mkswap&nbsp;/dev/sdb2
Setting&nbsp;up&nbsp;swapspace&nbsp;version&nbsp;1,&nbsp;size&nbsp;=&nbsp;518184&nbsp;kB</pre>

**3、使用swapon命令激活swap分区**

# swapon [device]

# swapon -a        # 开启所有标识为swap的分区
<pre class="crayon-plain-tag">[root@localhost&nbsp;~]#&nbsp;free&nbsp;-m
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;total&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;used&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;free&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;shared&nbsp;&nbsp;&nbsp;&nbsp;buffers&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cached
Mem:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;122&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;103&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;18&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;33
-/+&nbsp;buffers/cache:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;68&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;53
Swap:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1027&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;70&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;957
[root@localhost&nbsp;~]#&nbsp;swapon&nbsp;/dev/sdb2
[root@localhost&nbsp;~]#&nbsp;free&nbsp;-m
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;total&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;used&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;free&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;shared&nbsp;&nbsp;&nbsp;&nbsp;buffers&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cached
Mem:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;122&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;103&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;18&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;33
-/+&nbsp;buffers/cache:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;68&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;53
Swap:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1521&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;70&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1451</pre>

**4、使用swapoff命令关闭swap分区**

# swapoff [device]

# swapoff -a
<pre class="crayon-plain-tag">[root@localhost&nbsp;~]#&nbsp;swapoff&nbsp;/dev/sdb2</pre>

**5、设置开机自动挂载swap分区**

我们可以编辑/etc/fstab配置文件，在文件末尾增加：
<pre class="crayon-plain-tag">/dev/sda5&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;swap&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;swap&nbsp;&nbsp;&nbsp;&nbsp;defaults&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0&nbsp;0</pre>

* * *

当前系统上，没有任何磁盘空间可以创建分区了，但是又必须要扩展swap时，该如何是好呢？

在类Unix系统中，/dev/loop（或称vnd (vnode disk)、lofi（循环文件接口））是一种伪设备，这种设备使得文件可以如同块设备一般被访问。在使用之前，循环设备必须与现存文件系统上的文件相关联。这种关联将提供给用户一个应用程序接口，接口将允许文件视为块特殊文件（参见设备文件系统）使用。因此，如果文件中包含一个完整的文件系统，那么这个文件就能如同磁盘设备一般被挂载。

那么意味着我们可以通过创建本地回环设备，来模拟磁盘分区使用。那么下面就来看看如何使用文件来模拟swap分区。

**1、查看系统swap分区**
<pre class="crayon-plain-tag">[root@localhost&nbsp;~]#&nbsp;cat&nbsp;/proc/swaps&nbsp;
Filename				Type		Size	Used	Priority
/dev/sda2&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;partition	1052248	71776	-1</pre>

**2、使用dd命令创建大文件**

使用下面这条命令，就可以创建一个512M大小的文件，名为swapfile
<pre class="crayon-plain-tag">[root@localhost&nbsp;~]#&nbsp;dd&nbsp;if=/dev/zero&nbsp;of=swapfile&nbsp;bs=1M&nbsp;count=512
512+0&nbsp;records&nbsp;in
512+0&nbsp;records&nbsp;out
536870912&nbsp;bytes&nbsp;(537&nbsp;MB)&nbsp;copied,&nbsp;15.0813&nbsp;seconds,&nbsp;35.6&nbsp;MB/s</pre>

**3、使用mkswap命令创建swap文件系统**
<pre class="crayon-plain-tag">[root@localhost&nbsp;~]#&nbsp;mkswap&nbsp;swapfile
Setting&nbsp;up&nbsp;swapspace&nbsp;version&nbsp;1,&nbsp;size&nbsp;=&nbsp;536866&nbsp;kB</pre>

**4、使用swapon命令启用swap分区**
<pre class="crayon-plain-tag">[root@localhost&nbsp;~]#&nbsp;cat&nbsp;/proc/swaps
Filename				Type		Size	Used	Priority
/dev/sda2&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;partition	1052248	71792	-1
[root@localhost&nbsp;~]#&nbsp;free&nbsp;-m
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;total&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;used&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;free&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;shared&nbsp;&nbsp;&nbsp;&nbsp;buffers&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cached
Mem:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;122&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;119&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;50
-/+&nbsp;buffers/cache:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;68&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;54
Swap:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1027&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;70&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;957
[root@localhost&nbsp;~]#&nbsp;swapon&nbsp;swapfile
[root@localhost&nbsp;~]#&nbsp;cat&nbsp;/proc/swaps
Filename				Type		Size	Used	Priority
/dev/sda2&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;partition	1052248	71792	-1
/root/swapfile&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;file		524280	0	-6
[root@localhost&nbsp;~]#&nbsp;free&nbsp;-m
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;total&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;used&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;free&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;shared&nbsp;&nbsp;&nbsp;&nbsp;buffers&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cached
Mem:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;122&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;119&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;50
-/+&nbsp;buffers/cache:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;68&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;53
Swap:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1539&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;70&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1469</pre>

**5、使用swapoff关闭swap分区**
<pre class="crayon-plain-tag">[root@localhost&nbsp;~]#&nbsp;swapoff&nbsp;swapfile</pre>

**6、设置开机自动挂载swap分区**

编辑/etc/fstab文件，写入下面这一行
<pre class="crayon-plain-tag">echo&nbsp;&quot;/root/swapfile&nbsp;swap&nbsp;swap&nbsp;defaults&nbsp;0&nbsp;0&quot;&nbsp;&amp;gt;&amp;gt;&nbsp;/etc/fstab</pre>

总结：

1\. dd if=/dev/zero of=/path/swapfile bs=1k count=2048000

2\. mkswap /path/swapfile

3\. swapon /path/swapfile

4\. 修改/etc/fstab使其启动时自动mount：

在/etc/fstab中增加如下语句：

/path/swapfile  swap  swap    defaults 0 0

&nbsp;

转载自：http://blog.51cto.com/skypegnu1/1429558