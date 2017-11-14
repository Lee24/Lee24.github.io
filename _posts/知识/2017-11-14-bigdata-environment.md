---
layout:     post
title:     环境搭建相关
tags:   大数据
---
## 操作系统 —— centos7
### 总结
1. 用U盘安装，在安装界面中点击“install centos 7”安装不成功
> 需要修改安装参数来指定安装文件在哪个盘下（U盘）.    
在安装界面上选择“install centos 7”    
按下tab建，把下面出来的命令修改为： >vmlinuz initrd=initrd.img linux dd quiet 以此来查看U盘的盘符    
输入C返回到上一层的安装界面，再次选中“install centos 7” 按下tab建，把下面出来的命令修改为： >vmlinuz initrd=initrd.img inst.stage2=hd:/dev/sdb4 quiet  (sdb4为U盘具体的盘符) ，然后按下enter建进入安装界面

2. 安装时可用硬盘空间太小
> 在安装界面中选择“自动配置分区”，再勾选“我想让额外空间可用”，点击完成进入下一个界面进行“回收空间”操作，操作完后重新回到上一个界面点击“我要配置分区”对硬盘进行重新分区

3. 服务器重启后网卡处于未激活状态
> 编辑 vim /etc/sysconfig/network-scripts/ifcfg-ens33(文件名因系统和网卡的不同而不同) 把ONBOOT属性由 no 改为 yes 然后重启网卡：service network restart

4. 系统分区问题
> centos7的话可以在分区界面中点击自动分区，这样安装程序会更具系统硬件情况推荐一套分区方案。通常至少分配出以下几个分区：1. / 2. /boot 3. swap 4. /home    
swap分区可在系统安装好增加或减少

## hadoop安装（伪分布模式）
### 步骤
1. 下载解压，配置环境变量：配置HADOOP_HOME,把bin、sbin目录配置到path里

2. 添加hadoop用户及用户组     
sudo useradd hadoop    
sudo passwd hadoop    

3. 给用户设置超级权限    
su root    
vi /etc/sudoers    
在root ALL=(ALL) ALL 下面添加 hadoop ALL=(ALL) ALL

4. 设置ssh免密登录    
在/home/hadoop目录下执行    
$ ssh-keygen -t rsa   #一路回车    
$ cat .ssh/id_rsa.pub >> .ssh/authorized_keys    
$ chmod 600 .ssh/authorized_keys

5. 配置hadoop-env.sh  
在配置文件中加入：  export JAVA_HOME=/usr/java/jdk1.8(具体路径)

6. 配置core-site.xml

```xml
<configuration>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://localhost:9000</value>
    </property>
    <property>
        <name>hadoop.tmp.dir</name>
        <value>/home/hadoop/tmp</value>
   </property>
</configuration>
```

- fs.default.name 这是一个描述集群中NameNode结点的URI(包括协议、主机名称、端口号)，集群里面的每一台机器都需要知道NameNode的地址。DataNode结点会先在NameNode上注册，这样它们的数据才可以被使用。独立的客户端程序通过这个URI跟DataNode交互，以取得文件的块列表。
- hadoop.tmp.dir 是hadoop文件系统依赖的基础配置，很多路径都依赖它。如果hdfs-site.xml中不配置namenode和datanode的存放位置，默认就放在/tmp/hadoop-${user.name}这个路径中



7. hdfs-site.xml

```xml
<configuration>  
    <property>  
        <name>dfs.replication</name>  
        <value>1</value>  
    </property>  
    <property>  
        <name>dfs.name.dir</name>  
        <value>/usr/local/hadoop/hdfs/name</value>  
    </property>  
    <property>  
        <name>dfs.data.dir</name>  
        <value>/usr/local/hadoop/hdfs/data</value>  
    </property>  
</configuration>
```


8. mapred-site.xml






### 总结
1. haoop启动、停止:  
> start-all.sh   //启动
start-dfs.sh start-yarn.sh  

2. 查看hdfs集群情况
命令： hdfs dfsadmin -report

## hive安装
### 步骤
### 遇到问题
1. MySQL添加新用户出现mysql]ERROR 1364 (HY000): Field 'ssl_cipher' doesn't have a default value
>解决： grant usage on *.* to 'username'@'hostname' identified by 'passwd' with grant option;  //添加用户    
grant all privileges on *.* to 'username'@'hostname' identified by 'passwd';  //添加权限    
flush privileges; //更新权限    


## spark安装


## sqoop安装
