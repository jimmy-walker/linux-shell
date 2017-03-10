#Brief
bash shell 中主要提供了三种循环:for,while,until

```shell
#！/bin/bash
while [ condition ]
do
   command1
   command2
   command3
done
```

#Command
自动生成随机数，用于测试实时推荐系统使用

```shell
#！/bin/bash
while true
do
    echo $(($RANDOM%10+1)) >> top.log
    sleep 3
done
```