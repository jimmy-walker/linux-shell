# Brief

tmux和screen适合后端执行。

# Command

1. tmux

    ```shell
    #加载tmux
    export PATH=/data7/xxxx/.tmux_depend/bin:$PATH
    
    # 查看有所有tmux会话
    tmux ls
    
    # 分离会话
    tmux detach  或者使用  exit(关闭窗口)
    #快捷键：Ctrl+b d
    
    # 杀死会话
    tmux kill-session -t 
    
    # 新建tmux窗口
    tmux new -s <session-name>
    
    # 重新连接会话
    tmux attach -t <session-name>  或者使用 tmux at -t <session-name>
    ```

    

2. screen

    ```shell
    #新建
    screen -S jianjie 
    #退出
    ctrl+a ，再按 d ，即可保持这个screen到后台并回到主终端
    #重新连接
    screen -r jianjie
    #删除
    screen -S jianjie -X quit
    ```

    
