#Brief

Shell 是一个用C语言编写的程序，它是用户使用Linux的桥梁。Shell既是一种命令语言，又是一种程序设计语言。

Shell 是指一种应用程序，这个应用程序提供了一个界面，用户通过这个界面访问操作系统内核的服务。

#Script
Shell 脚本（shell script），是一种为shell编写的脚本程序。

业界所说的shell通常都是指shell脚本，**shell编程都是指shell脚本编程**。

Linux的Shell种类众多，其中**Bash( Bourne Again Shell)（/bin/bash）**在日常工作中被广泛使用。同时，Bash也是大多数Linux系统默认的Shell。

我们可以在执行 Shell 脚本时，向脚本传递参数，脚本内获取参数的格式为：**$n**。**n** 代表一个数字，1 为执行脚本的第一个参数，2 为执行脚本的第二个参数，以此类推。

```shell
#!/bin/bash
echo "Shell 传递参数实例！";
echo "执行的文件名：$0";
echo "第一个参数为：$1";
echo "第二个参数为：$2";
echo "第三个参数为：$3";

$ chmod +x test.sh 
$ ./test.sh 1 2 3
Shell 传递参数实例！
执行的文件名：./test.sh
第一个参数为：1
第二个参数为：2
第三个参数为：3
```



#Command

1. 编辑shell脚本：打开文本编辑器(可以使用vi/vim命令来创建文件)，新建一个文件test.sh，扩展名为sh（sh代表shell）

    ```shell
    #!/bin/bash # "#!"是一个约定的标记，它告诉系统这个脚本需要什么解释器来执行，即使用哪一种Shell。"#!"告诉系统其后路径所指定的程序即是解释此脚本文件的Shell程序。
    echo "Hello World !"
    ```

2. 执行shell脚本，作为可执行程序。**注意，一定要写成./test.sh，而不是test.sh，**运行其它二进制的程序也一样，直接写test.sh，linux系统会去PATH里寻找有没有叫test.sh的，而只有/bin, /sbin, /usr/bin，/usr/sbin等在PATH里，你的当前目录通常不在PATH里，所以写成test.sh是会找不到命令的，要用./test.sh告诉系统说，就在当前目录找。

    ```shell
    chmod +x ./test.sh #使脚本具有执行权限
    ./test.sh #执行脚本
    ```


