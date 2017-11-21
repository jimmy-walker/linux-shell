#Brief
if,else,fi语句的语法。
```shell
if [ expression ]
then
   Statement(s) to be executed if expression is true
else
   Statement(s) to be executed if expression is not true
fi
```

#Command
遍历文件，生成字符串。

```shell
FILENAME='query.txt'
i=0
dt_start='2017-10-24' #Shell变量赋值语句不能有空格，所以不能隔开空格
dt_end='2017-11-20'
temp=''
while read LINE;do
  echo "Query is $LINE"
  if [ $i == 0 ] #expression和方括号([ ])之间必须有空格，否则会有语法错误
  then
    temp+="'$LINE'" #+= operator可以不断加入字段
  else   
    temp+=", '$LINE'"  
  fi
  ((i++))
done < $FILENAME
echo "Total Query is $temp"

hive -hivevar dt_start=$dt_start -hivevar dt_end=$dt_end -hivevar "query=$temp" -f search_count_period.sql >> "$dt_start-$dt_end.txt"
```