# Linux系统目录结构
Linux系统目录

![](/assets/linux system dictionary.png)

![](/assets/linux system dictionary.jpg)

在linux系统中，有几个目录是比较重要的，平时需要注意不要误删除或者随意更改内部文件。

**/etc：**这个目录用来存放所有的系统管理所需要的配置文件和子目录，如果你更改了该目录下的某个文件可能会导致系统不能启动。 

/bin, /sbin, /usr/bin, /usr/sbin: 这是系统预设的执行文件的放置目录，比如ls就是在/bin/ls目录下的。

**/bin：**bin是Binary的缩写, 这个目录存放着最经常使用的命令。 



值得提出的是，/bin, /usr/bin 是给系统用户使用的指令（除root外的通用户），而/sbin, /usr/sbin 则是给root使用的指令。

/var： 这是一个非常重要的目录，系统上跑了很多程序，那么每个程序都会有相应的日志产生，而这些日志就被记录到这个目录下，具体在/var/log 目录下，另外mail的预设放置也是在这里。

