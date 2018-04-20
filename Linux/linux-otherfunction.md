# Other function

## grep(**Globally search a Regular Expression and Print**)

grep （缩写来自**Globally search a Regular Expression and Print**）是一种强大的文本搜索工具，它能使用正则表达式搜索文本，并把匹配的行打印出来。

### 命令格式

`grep [option] pattern file`

举例：查找以‘在人间|’开头的行。

```linux
grep '^在人间|' 2018-04-19suggest.txt
```

### 管道操作

管道操作就是把前面一条命令的输出作为后面一条命令的输入，从而把很多简单的命令组合起来完成复杂的功能。例如，如果我们想查找包含apple的行，但又想过滤掉pineapple，可以用下面的命令：

```linux
grep apple fruitlist.txt | grep -v pineapple
```

### 结果重定向

如果我们想把搜索结果保存起来，那么可以把命令的标准输出重定向到文件：如果想以追加方式写到文件，可以用>>。

```linux
grep apple fruitlist.txt | grep -v pineapple > apples.txt
```

### 更多option

- -a或--text 不要忽略二进制的数据。
- -A<显示列数>或--after-context=<显示列数> 除了显示符合范本样式的那一列之外，并显示该列之后的内容。
- -b或--byte-offset 在显示符合范本样式的那一列之前，标示出该列第一个字符的位编号。
- -B<显示列数>或--before-context=<显示列数> 除了显示符合范本样式的那一列之外，并显示该列之前的内容。
- -c或--count 计算符合范本样式的列数。
- -C<显示列数>或--context=<显示列数>或-<显示列数> 除了显示符合范本样式的那一列之外，并显示该列之前后的内容。
- -d<进行动作>或--directories=<进行动作> 当指定要查找的是目录而非文件时，必须使用这项参数，否则grep指令将回报信息并停止动作。
- -e<范本样式>或--regexp=<范本样式> 指定字符串做为查找文件内容的范本样式。
- -E或--extended-regexp 将范本样式为延伸的普通表示法来使用。
- -f<范本文件>或--file=<范本文件> 指定范本文件，其内容含有一个或多个范本样式，让grep查找符合范本条件的文件内容，格式为每列一个范本样式。
- -F或--fixed-regexp 将范本样式视为固定字符串的列表。
- -G或--basic-regexp 将范本样式视为普通的表示法来使用。
- -h或--no-filename 在显示符合范本样式的那一列之前，不标示该列所属的文件名称。
- -H或--with-filename 在显示符合范本样式的那一列之前，表示该列所属的文件名称。
- -i或--ignore-case 忽略字符大小写的差别。
- -l或--file-with-matches 列出文件内容符合指定的范本样式的文件名称。
- -L或--files-without-match 列出文件内容不符合指定的范本样式的文件名称。
- -n或--line-number 在显示符合范本样式的那一列之前，标示出该列的列数编号。
- -q或--quiet或--silent 不显示任何信息。
- -r或--recursive 此参数的效果和指定"-d recurse"参数相同。
- -s或--no-messages 不显示错误信息。
- -v或--revert-match 反转查找。
- -V或--version 显示版本信息。
- -w或--word-regexp 只显示全字符合的列。
- -x或--line-regexp 只显示全列符合的列。
- -y 此参数的效果和指定"-i"参数相同。
- --help 在线帮助。