# Brief

## 自定义指令

全局默认的路径为 /etc/profile，然后它会再加载 /etc/bash.bashrc
用户自己的就是 $HOME 目录下的 .profile，它默认会加载 .bashrc

## 操作流程

### 在$HOME 目录下编辑.bashrc

```shell
# .bashrc

# Source global definitions
alias gsong='cat /data1/xxxxx/data/xxxxxxx_data/xxxxxx_xxxxxx_xxxxinfo'
alias gsongm='cat /data1/xxxxx/data/xxxxxxx_data/xxxxxxxid_info_1'
alias goutput='cat /data1/xxxxx/xxxxxx/new_output_valid'
alias gvalid='cat /data1/xxxxx/xxxxxx/all_result_valid'
alias gremark='cat /data1/xxxxx/data/xxxxx_data/xxxxxx_xxxxxx_remark'
if [ -f /etc/bashrc ]; then
        . /etc/bashrc
fi
asong() {
    awk -v var="$@" -F '\t' '{if($1==var) print $0}' /data1/xxxxx/data/xxxxxxx_data/xxxxxx_xxxxxx_xxxxinfo
}
asongm() {
    awk -v var="$@" -F '\t' '{if($1==var) print $0}' /data1/xxxxx/data/xxxxxxx_data/xxxxxxxid_info_1
}
axxxxx() {
    awk -v var="$@" -F '\|' '{if($1==var) print $0}' /data1/xxxxx/data/xxxxx_data/xxxxxx_xxxxxx_xxxxx
}
aoutput() {
    awk -v var="$@" -F '\t' '{if($1==var) print $0}' /data1/xxxxx/xxxxxx/new_output_valid
}
avalid() {
    echo "$@"
    awk -v var="$@" -F '\t' '{if($1==var) print $0}' /data1/xxxxx/xxxxxx/all_result_valid
}

aresult() {
    echo "$@"
    awk -v var="$@" -F '\t' '{if($1==var) print $0}' /data1/xxxxxx/output/xxxxx_xxxxxx.txt
}

ashortresult() {
    echo "$@"
    awk -v var="$@" -F '\t' '{if($1==var) print $0}' /data1/xxxxxx/output/xxxxxxxxx_xxxxx_xxxxxx.txt
}
astat() {
    echo "$@"
    awk -v var="$@" -F '\t' '{if($1==var) print $0}' /data1/xxxxx/xxxx_xxxxxx/data/source_data/outs
}

abigxxxxxx() {
    echo "$@"
    awk -v var="$@" -F '\t' '{if($1==var) print $0}' /data1/xxxxxx/output/xxxxxxxx.txt
}
amodelbase() {
    echo "$@"
    awk -v var="$@" -F '\t' '{if($1==var) print $0}' /data1/xxxxx/xxxx_xxxxxx/data/result_data/model_base
}
acumulate() {
    echo "$@"
    awk -v var="$@" -F '\t' '{if($2==var) print $0}' /data1/xxxxx/xxxx_xxxxxx/data/result_data/cumulate
}
aentity() {
    echo "$@"
    awk -v var="$@" -F '\t' '{if($1==var) print $0}' /data1/xxxxx/xxxxxx/xxxxxx_all_line
}
arulebase() {
    echo "$@"
    awk -v var="$@" -F '\t' '{if($1==var) print $0}' /data1/xxxxx/xxxx_xxxxxx/data/result_data/rule_based
}

wgdata() {

    sudo wget http://xxxxxxxx.xxxxx.cn/xxxxxxxx_xxxxxx/xxxxxxxxxxxxx/xxxxxx_xxxxxx_"$@".txt
}
wgminjie() {
    sudo wget http://xxxxxxxx.xxxxx.cn/xxxxxxxx_xxxxxx/xxxxxx_xxxx/xxxxxxxid_info_1_"$@"
}
trys() {
   echo "$@"
   echo "$@"
}
scpdata() {
    rsync -ar rsync@xx.x.xx.xxx:/data1/tempforxxx/xxxxxxxid_info_1_"$@".txt ./xxxxxxxid_info_1
}
wgetdata() {
    wget http://xxxxxxxx.xxxxx.cn/xxxxxxxxxxxxx/xxxxxxxx_xxxxxx/xxxxxxxx.txt
}
# Uncomment the following line if you don't like systemctl's auto-paging feature:
# export SYSTEMD_PAGER=

# User specific aliases and functions
```

### 使用source .bashrc使其生效

source命令，也称“点命令”，也就是一个点符号（.），是bash的内部命令。 功能：使shell读入指定的shell程序文件并依次执行文件中的所有语句。 该命令通常用于重新执行刚修改的初始化文件，使之立即生效，而不必注销并重新登录。