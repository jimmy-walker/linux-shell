#Brief
bash shell 中的时间控制命令date：**使用-d等命令（其中减号可以进行偏移）；利用+设置格式。**

```shell
date [OPTION]... [+FORMAT]
-d, --date=STRING
              display time described by STRING, not ‘now’

date -d "2017-11-22 -28 days" +%Y-%m-%d
```

#Command
给定日期生成指定的间隔日子

```shell
#！/bin/bash
echo "起始日期为：$(date -d "$1 -28 days" +%Y-%m-%d)";
echo "截止日期为：$(date -d "$1 -1 days" +%Y-%m-%d)";

$ chmod +x test.sh 
$ ./test.sh 2017-11-22
起始日期为：2017-10-25
截止日期为：2017-11-21
```