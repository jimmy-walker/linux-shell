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
- **-E或--extended-regexp 将范本样式为延伸的普通表示法来使用。（J就是用正则）**
- -f<范本文件>或--file=<范本文件> 指定范本文件，其内容含有一个或多个范本样式，让grep查找符合范本条件的文件内容，格式为每列一个范本样式。
- -F或--fixed-regexp 将范本样式视为固定字符串的列表。
- -G或--basic-regexp 将范本样式视为普通的表示法来使用。
- -h或--no-filename 在显示符合范本样式的那一列之前，不标示该列所属的文件名称。
- -H或--with-filename 在显示符合范本样式的那一列之前，表示该列所属的文件名称。
- -i或--ignore-case 忽略字符大小写的差别。
- -l或--file-with-matches 列出文件内容符合指定的范本样式的文件名称。
- -L或--files-without-match 列出文件内容不符合指定的范本样式的文件名称。
- **-n或--line-number 在显示符合范本样式的那一列之前，标示出该列的列数编号。(J会显示出所有行号)**
- -q或--quiet或--silent 不显示任何信息。
- **-r或--recursive 此参数的效果和指定"-d recurse"参数相同。（循环遍历）**
- -s或--no-messages 不显示错误信息。
- **-v或--revert-match 反转查找（J就是不匹配）**。
- -V或--version 显示版本信息。
- **-w或--word-regexp 只显示全字符合的列。（J只返回全部命中的）**
- -x或--line-regexp 只显示全列符合的列。
- -y 此参数的效果和指定"-i"参数相同。
- --help 在线帮助。

### 实例

#### 获取最新的分区

```bash
mixsongid_partition="set hive.cli.print.header=false;show partitions temp.search_near_mixsong_info "
mixsongid_lastest_partition=`hive -S -e  "$mixsongid_partition" | grep -E '[0-9]{4}-[0-1][0-9]-[0-3][0-9]' | grep '=2' | sort | tail -n 1` #hive -S 静默模式，不输出调试信息，只输出结果，否则会输出耗时信息，-e 从命令行执行指定的 HQL， -E正则表达式
vmixsongid=${mixsongid_lastest_partition:21:20}
echo ${vmixsongid}
```

#### 查找所有包含文字的文件

```bash
grep -rnw '/path/to/somewhere/' -e 'pattern'
grep --include=\*.{c,h} -rnw '/path/to/somewhere/' -e "pattern" #This will only search through those files which have .c or .h extensions
grep --exclude=\*.o -rnw '/path/to/somewhere/' -e "pattern" #This will exclude searching all the files ending with .o extension
grep --exclude-dir={dir1,dir2,*.dst} -rnw '/path/to/somewhere/' -e "pattern" #For directories it's possible to exclude one or more directories using the --exclude-dir parameter. For example, this will exclude the dirs dir1/, dir2/ and all of them matching *.dst/

```



## sed(stream editor)

用于修改，提取，删除文件。

### 命令格式

```
sed [-hnV][-e<script>][-f<script文件>][文本文件]
```

### 参数说明

- -e<script>或--expression=<script> 以选项中指定的script来处理输入的文本文件。
- **-E或--extended-regexp 将范本样式为延伸的普通表示法来使用。（J就是用正则）**
- -f<script文件>或--file=<script文件> 以选项中指定的script文件来处理输入的文本文件。
- -h或--help 显示帮助。
- -n或--quiet或--silent 仅显示script处理后的结果。
- -V或--version 显示版本信息。

### **动作说明**

- a ：新增， a 的后面可以接字串，而这些字串会在新的一行出现(目前的下一行)～
- c ：取代， c 的后面可以接字串，这些字串可以取代 n1,n2 之间的行！
- d ：删除，因为是删除啊，所以 d 后面通常不接任何咚咚；
- i ：插入， i 的后面可以接字串，而这些字串会在新的一行出现(目前的上一行)；
- p ：打印，亦即将某个选择的数据印出。通常 p 会与参数 sed -n 一起运行～
- **s ：取代，可以直接进行取代的工作哩！通常这个 s 的动作可以搭配正规表示法！例如 1,20s/old/new/g 就是啦！(Jg代表全部替换，没有g则是第一个替换)**

### 实例

#### 提取替换文件内容

```bash
cat newsongs.txt | sed -E 's/^([0-9]+).*|/\1/' > newsongs2.txt #没有-E就是说普通的替换，用了-E就是用正则替换
sed 's/^/添加的头部&/g' 　　　　 #在所有行首添加
sed 's/$/&添加的尾部/g' 　　　　 #在所有行末添加
sed '2s/原字符串/替换字符串/g'　 #替换第2行
sed '$s/原字符串/替换字符串/g'   #替换最后一行
sed '2,5s/原字符串/替换字符串/g' #替换2到5行
sed '2,$s/原字符串/替换字符串/g' #替换2到最后一行
```



## export

Linux export命令用于设置或显示环境变量。

在shell中执行程序时，shell会提供一组环境变量。export可新增，修改或删除环境变量，供后续执行的程序使用。**export的效力仅及于该次登陆操作。**

### 命令格式

```
export [-fnp][变量名称]=[变量设置值]
```

```linux
export -p //列出当前的环境变量值
export BERT_BASE_DIR=model/chinese_L-12_H-768_A-12
export INPUT_FILE=data/lm/test.zh.tsv
python run_lm_predict.py \
  --input_file=$INPUT_FILE \
  --vocab_file=$BERT_BASE_DIR/vocab.txt \
  --bert_config_file=$BERT_BASE_DIR/bert_config.json \
  --init_checkpoint=$BERT_BASE_DIR/bert_model.ckpt \
  --max_seq_length=128 \
  --output_dir=/tmp/lm_output/
```

###参数说明

- -f 　代表[变量名称]中为函数名称。
- -n 　删除指定的变量。变量实际上并未删除，只是不会输出到后续指令的执行环境中。
- -p 　列出所有的shell赋予程序的环境变量。

## help

**help命令**用于显示shell内部命令的帮助信息。help命令只能显示shell内部的命令帮助信息。而对于外部命令的帮助信息只能使用[man](http://man.linuxde.net/man)或者[info](http://man.linuxde.net/info)命令查看。 

###命令格式

```
help [option] command
```

## rsync

```
rsync -avz -e 'ssh -p 32200' senddir/ baseDepSarch@10.1.XXX.18:file/upload

rsync -avz -e 'ssh -p 32200' baseDepSarch@10.1.XXX.18:file/download/ receivedir/
```

在跳板机使用，从而替代`rz/sz`的作用进行传输文件。

```
-a --archive  ：归档模式，表示递归传输并保持文件属性
-v：显示rsync过程中详细信息。可以使用"-vvvv"获取更详细信息。
-z        ：传输时进行压缩提高效率。
```

## tr

translate的缩写。Linux tr 命令用于转换或删除文件中的字符。**（J只是单个换单个）**

```bash
cat tmp | tr " " "*" | tr "\t" "&"
#将空格和tab符号显示出啦
cat testfile |tr a-z A-Z 
#大小写转换
```

## find

统计文件夹内的文件个数

```bash
find DIR_NAME -type f | wc -l #-type f to include only files.
find . -name "*.c" #将当前目录及其子目录下所有文件后缀为 .c 的文件列出来
```

### 实例

#### 删除在文件夹中符合条件的文件

```bash
find . -name "*.swp" -type f -delete #remove all .swp files
```

