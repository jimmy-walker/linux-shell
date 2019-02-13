#Brief

##定义变量

定义变量时，变量名不加美元符号。

**注意，变量名和等号之间不能有空格**。 同时，变量名的命名须遵循如下规则：

- 命名只能使用英文字母，数字和下划线，首个字符不能以数字开头。
- 中间不能有空格，可以使用下划线（_）。
- 不能使用标点符号。
- 不能使用bash里的关键字（可用help命令查看保留关键字）。

```shell
yyyy_mm_dd_1=`date -d "$vDay" +%Y-%m-%d` #yesterday
vEdition="7471"
start_time="${yyyy_mm_dd_1} 00:00:00.000"
end_time="${yyyy_mm_dd_1} 23:59:59.999"
```

#Command
##使用变量

使用一个定义过的变量，只要在变量名前面加美元符号即可。**变量名外面的花括号是可选的，加不加都行**，加花括号是为了帮助解释器识别变量的边界。(J**建议加括号**)

```shell
your_name="qinjx"
echo $your_name
echo ${your_name}
```
## 字符串

字符串是shell编程中最常用最有用的数据类型（除了数字和字符串，也没啥其它类型好用了），字符串可以用单引号，也可以用双引号，也可以不用引号。单双引号的区别跟PHP类似。

###单引号

```shell
str='this is a string'
```

单引号字符串的限制：

- 单引号里的任何字符都会原样输出，**单引号字符串中的变量是无效的**；
- 单引号字串中不能出现单独一个的单引号（对单引号使用转义符后也不行），但**可成对出现，作为字符串拼接使用。**

### 双引号

```shell
your_name='runoob'
str="Hello, I know you are \"$your_name\"! \n"
echo -e $str
```

输出结果为：

```
Hello, I know you are "runoob"! 
```

双引号的优点：

- **双引号里可以有变量**
- **双引号里可以出现转义字符**

### 拼接字符串

```shell
your_name="runoob"
# 使用双引号拼接
greeting="hello, "$your_name" !"
greeting_1="hello, ${your_name} !"
echo $greeting  $greeting_1
# 使用单引号拼接
greeting_2='hello, '$your_name' !'
greeting_3='hello, ${your_name} !'
echo $greeting_2  $greeting_3
```

输出结果为：

```
hello, runoob ! hello, runoob !
hello, runoob ! hello, ${your_name} !
```