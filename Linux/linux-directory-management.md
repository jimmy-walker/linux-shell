#Bref

**Linux的目录结构为树状结构，最顶级的目录为根目录`/`，其他目录通过挂载可以将它们添加到树中，通过解除挂载可以移除它们**。

#Command

1. 绝对路径与相对路径。**即相对路径中前后路径相同部分可用`../`来表示；`./`表示当前目录**

    ```shell
[root@www /]# ls -l
total 64
 dr-xr-xr-x 2 root root 4096 Dec 14 2012 bin
 dr-xr-xr-x 4 root root 4096 Apr 19 2012 boot
 ```

    1. 绝对路径：路径的写法，由根目录`/`写起。例如`/usr/share/doc`

    2. 相对路径：路径的写法，不是由`/`写起。例如由`/usr/share/doc`要到`/usr/share/man`底下时，可以写成：`cd ../man`。

2. 目录处理命令，可以使用 man(manual)命令来查看各个命令的使用文档，如 ：`man cp`

    ls: 列出目录(list)

    ```shell
 [root@www ~]# ls -al
 #-a ：全部的文件，连同隐藏档( 开头为 . 的文件) 一起列出来(常用)
    ```

    cd：切换目录(change directory)

    ```shell
 # 表示回到自己的家目录，亦即是 /root 这个目录
 [root@www w3cschool.cc]# cd ~
 # 表示去到目前的上一级目录，亦即是 /root 的上一级目录的意思；
 [root@www ~]# cd ..
    ```

    pwd：显示目前的目录(print working directory)

    mkdir：创建一个新的目录(make directory)

    ```shell
 [root@www tmp]# mkdir test1/test2/test3/test4
 mkdir: cannot create directory `test1/test2/test3/test4':
 No such file or directory #<== 没办法直接创建此目录啊！
 [root@www tmp]# mkdir -p test1/test2/test3/test4
 #-p ：帮助你直接将所需要的目录(包含上一级目录)递回创建起来！
    ```

 rmdir：删除一个空的目录()，注意若尚有内容，则无法删除。

 cp: 复制文件或目录(copy)

 ```shell

 [root@www ~]# cp [options] source1 source2 source3 .... directory

 #-a：相当於 -pdr 的意思，至於 pdr 请参考下列说明；(常用)

 #-r：递回持续复制，用於目录的复制行为；(常用)

 ```

 rm: 移除文件或目录(remove)

 mv: 移动文件与目录，或修改名称(move)

 ```shell

 [root@www ~]# mv [options] source1 source2 source3 .... directory

 ```

3. 文件内容查看，可以使用 man(manual)命令来查看各个命令的使用文档，如 ：`man cp`

 **cat**：一次显示整个文件:`cat filename`；从键盘创建一个文件:`cat > filename`只能创建新文件,不能编辑已有文件；将几个文件合并为一个文件:`cat file1 file2 > file`(concatenate)

 ```shell

 [root@www ~]# cat /etc/issue

 CentOS release 6.4 (Final)

 Kernel \r on an \m

 #-n, --number 对输出的所有行编号,由1开始对所有输出的行数编号

 ```
