#Brief

一般来说著名的 linux 系统基本上分两大类：

1. RedHat系列：Redhat、CentOS、Fedora等

    1. 常见的安装包格式 rpm包,安装rpm包的命令是“rpm -参数”，rpm是redhat公司的一种软件包管理机制，直接通过rpm命令进行安装删除等操作。

    2. 包管理工具 yum

    3. 支持tar包

2. Debian系列：Debian、Ubuntu等

    1. 常见的安装包格式 deb包,安装deb包的命令是“dpkg -参数”，dpkg 是Debian Package的简写，为 Debian专门开发的套件管理系统，方便软件的安装、更新及移除。

    2. 包管理工具 apt-get（Advanced Packaging Tools，缩写为APT）

    3. 支持tar包

#Command

Ubuntu中的高级包管理方法apt-get。（dpkg绕过apt包管理数据库对软件包进行操作，所以你用dpkg安装过的软件包用apt可以再安装一遍，系统不知道之前安装过了，将会覆盖之前dpkg的安装。）

`sudo apt-get update`：更新源

`sudo apt-get install package`：安装包

`sudo apt-get remove package`：删除包

#Reference

- [apt-get 与 yum 的区别](http://www.cnblogs.com/ivantang/p/4620961.html)
- [dpkg ---- apt-get ------ aptitude 三种方式的区别 及命令格式](http://blog.csdn.net/xiaoyanghuaban/article/details/22946987)
