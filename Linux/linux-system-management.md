# Command
1. Linux top命令用于实时显示 process 的动态。 
    
    1. 显示进程信息
    
    `top`

    2. 设置信息更新时间

    `top -d 3
    //表示更新周期为3秒`

2. 重定向符>>，比如cmd >> file 把 stdout 重定向到 file 文件中(追加)；

    `top -d 1 >> record.log`
    