#Bref

Linux系统是一种典型的多用户系统，不同的用户处于不同的地位，拥有不同的权限。为了保护系统的安全性，Linux系统对不同的用户访问同一文件（包括目录文件）的权限做了不同的规定。

#Command

1. 在Linux中我们可以使用ll或者`ls –l`**(list long format)**命令来显示一个文件的属性以及文件所属的用户和组。

    ```shell
 [root@www /]# ls -l
 total 64
 dr-xr-xr-x 2 root root 4096 Dec 14 2012 bin
 dr-xr-xr-x 4 root root 4096 Apr 19 2012 boot
    ```

    1. 第一个字符代表这个文件是目录、文件或链接文件等等。

    2. 接下来的字符中，以三个为一组，且均为『rwx』 的三个参数的组合。其中，[ r ]代表可读(read)、[ w ]代表可写(write)、[ x ]代表可执行(execute)。 要注意的是，这三个权限的位置不会改变，如果没有权限，就会出现减号[ - ]而已。

    ![](/assets/linux file property.png)

    3. 第0位确定文件类型，第1-3位确定属主owner（该文件的所有者）拥有该文件的权限。第4-6位确定属组group（所有者的同组用户）拥有该文件的权限，第7-9位确定其他用户others拥有该文件的权限。

2. chmod：**(change mode)**更改文件9个属性。**Linux文件属性有两种设置方法，一种是数字（r:4；w:2；x:1），一种是符号（rwx）**。

    1. 数字类型改变文件权限：Linux文件的基本权限就有九个，分别是owner/group/others三种身份各有自己的read/write/execute权限。例如当权限为： [-rwxrwx---] 分数则是：

    ```
owner = rwx = 4+2+1 = 7
group = rwx = 4+2+1 = 7
others= --- = 0+0+0 = 0
    ```

    ```
chmod [-R] xyz 文件或目录
xyz : 就是数字类型的权限属性，为 rwx 属性数值的相加。
-R : 进行递归(recursive)的持续变更，亦即连同次目录下的所有文件都会变更
    ```

    ```shell
 [root@www ~]# ls -al .bashrc
 -rw-r--r-- 1 root root 395 Jul 4 11:45 .bashrc
 [root@www ~]# chmod 777 .bashrc
 [root@www ~]# ls -al .bashrc
 -rwxrwxrwx 1 root root 395 Jul 4 11:45 .bashrc
    ```

    2. 符号类型改变文件权限：**可以藉由u, g, o来代表三种身份的权限，a则代表all亦即全部的身份！那么读写的权限就可以写成r, w, x**。

     ![](/assets/change mode code.PNG)

    ```shell
 chmod +x ./test.sh #chmod +x somefile is the same as chmod a+x somefile
    ```


