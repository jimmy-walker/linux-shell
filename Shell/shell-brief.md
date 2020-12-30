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

# Example

在38的结点上运行脚本，会自动调用全部集群。

J理解为从任何结点都可以提交作业。

## hive of shell

```shell
#!/bin/bash
##********************************************************************#
##
## 日期支持运算，通过以下方式：
## ${DATA_DATE offset field formatter}，
## DATE_DATE：*固定值，为当前作业的业务时间
## offet：*必填，当前的日期偏移量，根据field判定偏移字段，取值为数值可正可负
## field：*必填，偏移的字段，取值可以为：day，month，year，minute，hour，week，second
## formatter：选填，计算偏移后的日期格式，如：yyyy-MM-dd HH:mm:ss
## 如：${DATA_DATE -1 day 'yyyy-MM-dd HH:mm'}
##********************************************************************#
source $BIPROG_ROOT/bin/shell/common.sh

###定义内部变量##################
vDay=${DATA_DATE} #yesterday
#yyyy_mm_dd_1=`date -d "$vDay" +%Y-%m-%d` #yesterday
yyyy_mm_dd_1="2020-12-13"
yyyy_mm_dd_2=`date -d "$vDay -1 days" +%Y-%m-%d` #2 days ago
yyyy_mm_dd_3=`date -d "$vDay -2 days" +%Y-%m-%d` #3 days ago
yyyy_mm_dd_5=`date -d "$vDay -4 days" +%Y-%m-%d` #5 days ago
#vEdition="9156"
vEdition="9355"
start_time="${yyyy_mm_dd_1} 00:00:00.000"
end_time="${yyyy_mm_dd_1} 23:59:59.999"

############################ 功能执行部分 ############################

dst_path=/data1/baseDepSarch/search_doublecheck_qq
#dst_path=/data2/web_service/play_time
filename="correctfind_qq"
filename_txt="${filename}_${yyyy_mm_dd_1_format}.txt"

CMD="hive -e \"
set hive.cli.print.header=false;
set mapreduce.job.queuename=root.XXXXXXXXXXXQueue;
select prev_word, final, qq_check from temp.XXXXXXX_query_find_correct_part_qq_double_request_orc_search_hot 
where cdt='${yyyy_mm_dd_1}' and qq_check='true'; \"
> '${dst_path}/tmp_${filename_txt}'"
EXESH_CMD

check_file_size "${dst_path}/tmp_${filename_txt}"

rm "${dst_path}/tmp_${filename_txt}"
```

## spark of shell

```shell
#!/bin/bash
##********************************************************************#
##
## 日期支持运算，通过以下方式：
## ${DATA_DATE offset field formatter}，
## DATE_DATE：*固定值，为当前作业的业务时间
## offet：*必填，当前的日期偏移量，根据field判定偏移字段，取值为数值可正可负
## field：*必填，偏移的字段，取值可以为：day，month，year，minute，hour，week，second
## formatter：选填，计算偏移后的日期格式，如：yyyy-MM-dd HH:mm:ss
## 如：${DATA_DATE -1 day 'yyyy-MM-dd HH:mm'}
##********************************************************************#
source $BIPROG_ROOT/bin/shell/common.sh
vDay=${DATA_DATE} #yesterday
yyyy_mm_dd_1=`date -d "$vDay" +%Y-%m-%d` #yesterday
yyyy_mm_dd_2=`date -d "$vDay -1 days" +%Y-%m-%d` #2 days ago
yyyy_mm_dd_3=`date -d "$vDay -2 days" +%Y-%m-%d` #3 days ago
yyyy_mm_dd_5=`date -d "$vDay -4 days" +%Y-%m-%d` #4 days ago
#vEdition="9156"
vEdition="9355"
start_time="${yyyy_mm_dd_2} 00:00:00.000"
end_time="${yyyy_mm_dd_2} 23:59:59.999"
thisTable="extern.jimmylian_query_rank_correct"
sourceTable="temp.jimmylian_query_rank_correct"
max_word=20
threshold=15
#thresholdcount=2
#to activate chocie_multiple
thresholdcount=0

spark-submit \
--name jimmy_spark_query_suggest \
--jars jieba-analysis-1.0.2.jar,diff-match-patch-1.2.jar,jpinyin-1.1.8.jar,hanlp-portable-1.7.8.jar \
--master yarn \
--queue root.XXXXXXXXXXXQueue \
--deploy-mode client \
--executor-memory 20G \
--driver-memory 2g \
--executor-cores 3 \
--num-executors 3 \
--conf spark.sql.shuffle.partitions=2001 \
--conf spark.network.timeout=800 \
--conf spark.scheduler.listenerbus.eventqueue.size=100000 \
--conf spark.sql.hive.convertMetastoreOrc=false \
--class CorrectCheck \
CorrectCheck-1.0.jar \
${yyyy_mm_dd_2} \
${yyyy_mm_dd_2} \
${vEdition} \
"${start_time}" \
"${end_time}" \
${thisTable} \
${max_word} \
${sourceTable} \
${threshold} \
${thresholdcount}
```

