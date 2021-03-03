# Command

##文件传输
###上传文件
`rz`
如果报错：zmodem transfer canceled by remote side
原因：是上传文件中可能含有控制字符的问题
解决：使用 rz -e 命令可以解决这个问题

###下载文件
`sz 文件名`

##文件解压缩
###压缩文件
把/home目录下面的mydata目录压缩为mydata.zip
`zip -r mydata.zip mydata #压缩mydata目录`

###解压缩文件
把/home目录下面的mydata.zip解压到mydatabak目录里面
`unzip mydata.zip -d mydatabak`

##文件切割

`split -b 4000M SMP-Weibo.7z SMP-Weibo`

```
split [-b ][-C ][-][-l ][要切割的文件][输出文件名前缀][-a ]
```

- -b<字节>：指定按多少字节进行拆分，也可以指定 K、M、G、T 等单位。

- -<行数>或-l<行数>：指定每多少行要拆分成一个文件。
- 输出文件名前缀：设置拆分后的文件的名称前缀，split 会自动在前缀后加上编号，默认从 aa 开始。
- -a<后缀长度>：默认的后缀长度是 2，也就是按 aa、ab、ac 这样的格式依次编号。