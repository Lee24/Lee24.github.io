---
layout:     post
title:      待整理笔记
category:   wait
tags:		[待整理]
---
【linux】
du -h --max-depth=1(能看到隐藏的文件) 查看子文件夹的大小
zip -rq ./part4874.zip ./20160318/
find -iname CSON.xml
crontab -e
crontab -l
find . -name "*" -type f -size 0c |xargs -n 1 rm -f  删除大小为0的文件
ls -l |grep "^-" |wc -l  查看目录的文件数
cat ./*  > ../temp.txt   合并目录文件
wget ftp://passward:username@hostip/path   从别的主机获取文件
ftp登陆：ftp ip (之后按提示输入用户名密码)
sftp登陆：
查看文件信息(比ll详细)： stat 文件
显示主机名： hostname
显示系统资源占用情况： top
查看网络情况： ifconfig
查看当前链接用户： who
查看命令详细说明：  man 命令名   如： man
显示当前用户： whoami
查看某端口情况： lsof -i:port
重启网卡： network restart
系统环境变量： /etc/profile
用户环境变量： bash_profile   或  .bashrc
切换用户，加载配置文件.bashrc  ：  su user
切换用户，加载配置文件/etc/profile ，加载bash_profile   ：  su - user
修改文件权限：sudo chmod [u所属用户 g所属组 o其他用户 a所有用户] [+增    加权限 -减少权限] [r w x] 目录名  如： chmod +x 文件名     如： chmod -R 777 文件名
更改文件的用户及用户组： sudo chown [-R] owner[:group]     {File|Directory}
查看文件末尾：  tail -f log.txt

【spark相关】
1. 报错： org.apache.hadoop.io.LongWritable cannot be cast to org.apache.hadoop.io.IntWritable
	原因： 存入的数据类型不匹配时，存的时候不会报错，但是取的时候就会报以上的错误
	解决： 改成一致的类型，做类型转换，或者改表类型

2. 在spark shell中df 早collect前map会报错，但是collect后再执行就不会有问题

3. spark rdd 不能序列化
报错： Task not serializable
原因： 出现“org.apache.spark.SparkException: Task not serializable"这个错误，一般是因为在map、filter等的参数使用了外部的变量，但是这个变量不能序列化。特别是当引用了某个类（经常 是当前类）的成员函数或变量时，会导致这个类的所有成员（整个类）都需要支持序列化。

【debug】
1. 安装了git之后不能从clone代代码，报不能链接服务器，链接超时的错误
	解决：给git配置代理： git config --global http.proxy http://proxy.zte.com.cn:80
	      配置好之后会在才c:/User/username 下生成一个.gitconfig文件

2. 用crontab调用python脚本的时候报错
原因：代码中用os.getcwd获取脚本当前路径的，但是crontab调用脚本的时候当前执行的路径为crontab用户的根目录，所以导致脚本获取数据出错

3. 处理pm数据时，报越界异常。
原因：用split函数时没有带第二个参数，导致丢失了后面为空的元素。 详细说明见：http://www.cnblogs.com/davidhaslanda/p/4050471.html
解决：把 split('|')  改成 split("\\|", -1)

4. spark-shell占用太多资源，影响其它任务运行
启动的是时候带上参数： ./spark-shell --executor-memory 4G \
                               --total-executor-cores 10 \
                               --executor-cores 1
--executor-memory 是指定每个executor(执行器)占用的内存
--total-executor-cores是所有executor总共使用的cpu核数
--executor-cores是每个executor使用的cpu核数

5. 在spark shell中需要带上hdfs://VMAXCluster/。 代码中不用是因为工程会自动从core-site.xml中的标签中读到hdfs://VMAXCluster/
val rdd = sc.textFile("hdfs://VMAXCluster/zxvmax/telecom/lte/tycj/source/lte_mr_tycj/p_provincecode=777778/p_date=2017-01-11/p_hour=10/ODM-A.WL.PM.FILE_WY_LTE_MRS_84401_op_rsrp_info_20161119100000-20161119110000_X1479533461964210.csv")
dataRDD.coalesce(numPartitions)   //定义rdd分片个数

【语言】
1. sql  limit x,y  作用，x为分页数，每次取y条数据
