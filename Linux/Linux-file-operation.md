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
