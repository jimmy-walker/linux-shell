# Brief

无论是做开发还是做运维的程序猿，crontab命令是必须用到的命令。

##目录介绍

- /var/spool/cron/ 目录下存放的是每个用户包括root的crontab任务，每个任务以创建者的名字命名。**J在这里面改成自己的用户名，就能看到已经设置的crontab作业。**

> ```linux
> sudo cat /var/spool/cron/root
> ```

- /etc/crontab 这个文件负责调度各种管理和维护任务。J就是一些配置而已。

> ```linux
> sudo cat /etc/crontab
> 
> SHELL=/bin/bash
> PATH=/sbin:/bin:/usr/sbin:/usr/bin
> MAILTO=root
> HOME=/
> 
> # For details see man 4 crontabs
> 
> # Example of job definition:
> # .---------------- minute (0 - 59)
> # |  .------------- hour (0 - 23)
> # |  |  .---------- day of month (1 - 31)
> # |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
> # |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
> # |  |  |  |  |
> # *  *  *  *  * user-name command to be executed
> ```

- /etc/cron.d/ 这个目录用来存放任何要执行的crontab文件或脚本。我们还可以把脚本放在/etc/cron.hourly、/etc/cron.daily、/etc/cron.weekly、/etc/cron.monthly目录中，让它每小时/天/星期、月执行一次。J就是不用设置启动时间，直接放在这些目录下，就能定时执行。

## 流程介绍

### 1.查看crontab定时任务

```linux
crontab -l
sudo crontab -u root -l #查看指定用户的crontab
```

### 2.编辑定时任务【删除-添加-修改】

```linux
crontab -e
sudo crontab -u root -e #编辑指定用户的crontab
```

```linux
0 12 * * * (/usr/local/bin/python /data2/test2/data/GetDictData.py >/dev/null 2>&1 &)
```

- The & makes the command run in the background.
- 在shell脚本中，默认情况下，总是有三个文件处于打开状态，标准输入(键盘输入)、标准输出（输出到屏幕）、标准错误（也是输出到屏幕），它们分别对应的**文件描述符**是0，1，2 。
  - 1，对于下面两个命令其实效果一样。一般来说，"1>" 通常可以省略成 ">"。
    - `ls GetDictData.py 1> test.out`
    - `ls GetDictData.py > test.out`
  - **就是说指定1和2可以分别输出正确和错误的结果**。**&2表示2输出通道，&1表示1输出通道。**
    - `ls a.txt b.txt 1>file.out 2>&1`
    - 输出`ls: b.txt: No such file or directory
      a.txt`
  - 输出不只1和2，还有其他的类型，这两种只是最常用和最基本的。
- 可以将/dev/null看作"黑洞"。它非常等价于一个只写文件. 所有写入它的内容都会永远丢失。而尝试从它那儿读取内容则什么也读不到。然而，/dev/null对命令行和脚本都非常的有用。
  - 禁止标准输出。`cat $filename >/dev/null`   # 文件内容丢失，而不会输出到标准输出。
  - 禁止标准错误：`2>/dev/null`这样错误信息[标准错误]就被丢到太平洋去了。
- `1>/dev/null` 首先表示标准输出重定向到空设备文件，也就是不输出任何信息到终端，说白了就是不显示任何信息。 
  `2>&1` 接着，标准错误输出重定向等同于 标准输出，因为之前标准输出已经重定向到了空设备文件，所以标准错误输出也重定向到空设备文件。 

## 实际例子

```python
#!/usr/bin/env python
#coding=utf-8

import urllib
import urllib2
import sys
import os
import time
import datetime
import socket
import copy
import logging
import logging.handlers
reload(sys)
sys.setdefaultencoding('utf8')
socket.setdefaulttimeout(2.0)
__version = '1.1'
__author = 'jimmylian'

etcdir = ''
datadir = ''
logdir = ''

def GetLogger(logdir, loglevel):
        """keep logfile change another file everyday"""
        filename = r"/log_update"
        myloglevel = 20
        tmploglevel = int(loglevel) / 10 * 10
        if tmploglevel >= 0 and tmploglevel <= 50:
                myloglevel = tmploglevel

        handler = logging.handlers.RotatingFileHandler(logdir+filename, maxBytes = 20*1024*1024, backupCount = 10)
        fmt = '%(asctime)s [line:%(lineno)d] [%(levelname)s] %(message)s'
        formatter = logging.Formatter(fmt)
        handler.setFormatter(formatter)
        logger = logging.getLogger('GetDictData')
        logger.addHandler(handler)
        logger.setLevel(myloglevel)
        return logger

def GetDateBefore(daydelta,split=''):
        today = datetime.date.today()
        bfyesterday = today - datetime.timedelta(days = daydelta)
        if split != '':
                fmt = '%Y'+split+'%m'+split+'%d'
        else:
                fmt = '%Y%m%d'
        return bfyesterday.strftime(fmt)

def DownHttpFile(url, filename, logger):
        tmpfile = "%s%s_tmp"%(datadir, filename)
        try:
                f = urllib2.urlopen(url)
                data = f.read()
                with open(tmpfile, 'wb') as code:
                        code.write(data)
        except Exception, e:
                logger.error("download file error %s"%e)
                return False
        filepath = "%s%s"%(datadir, filename)
        os.rename(tmpfile, filepath)
        return True

def process(logger):
        url = "http://XXXX.cn/XXX_info_1_%s"%(GetDateBefore(1, ''))
        flag = DownHttpFile(url, "info_1.txt", logger)
        path = '%sinfo_1.txt'%(datadir)
        destpath = '/info_1_%s.txt'%(GetDateBefore(1, ''))
        if not flag:
                if os.path.exists(destpath):
                        os.unlink(destpath)
                logger.info("download file %s failed"%(url))
                return
        os.rename(path, destpath)
        logger.info("download file %s done"%(url))
        rmpath = '/info_1_%s.txt'%(GetDateBefore(3, ''))
        if os.path.exists(rmpath):
            os.remove(rmpath)
            logger.info("remove file %s done"%(rmpath))
        else:
            logger.info("remove file %s failed"%(rmpath))

def process1(logger):
        url = "http://XXXX.cn/XXX_info_2_%s"%(GetDateBefore(1, ''))
        flag = DownHttpFile(url, "info_2.txt", logger)
        path = '%sinfo_2.txt'%(datadir)
        destpath = '/info_2_%s.txt'%(GetDateBefore(1, ''))
        if not flag:
                if os.path.exists(destpath):
                        os.unlink(destpath)
                logger.info("download file %s failed"%(url))
                return
        os.rename(path, destpath)
        logger.info("download file %s done"%(url))
        rmpath = '/info_2_%s.txt'%(GetDateBefore(3, ''))
        if os.path.exists(rmpath):
            os.remove(rmpath)
            logger.info("remove file %s done"%(rmpath))
        else:
            logger.info("remove file %s failed"%(rmpath))

def __main__():
        global datadir
        global logdir
        mybasedir = "%s"%(os.path.dirname(sys.argv[0]))
        if mybasedir == '':
                mybasedir = '.'
        datadir = "%s/data/"%(mybasedir)
        logdir = "%s/log/"%(mybasedir)
        logger = GetLogger(logdir, 20)
        runstr = ''
        for keys in sys.argv:
                runstr = "%s %s"%(runstr, keys)
        logger.info(runstr)
        process(logger)
        process1(logger)

if __name__ == "__main__":
        __main__()
```

# Reference

- [Linux Crontab 定时任务](https://www.runoob.com/w3cnote/linux-crontab-tasks.html )