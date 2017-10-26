---
layout:     post
title:      基础知识
category:   wait
tags:		[待整理]
---
1. JVM参数问题
-Xms128m -Xmx500m -XX:MaxPermSize=350m -XX:ReservedCodeCacheSize=96m

2. 常用命令

scp

3. HTTP 报头的Content-Disposition作用：Content-disposition 是 MIME 协议的扩展，MIME 协议指示 MIME 用户代理如何显示附加的文件。当 Internet Explorer 接收到头时，它会激活文件下载对话框，它的文件名框自动填充了头中指定的文件名。（请注意，这是设计导致的；无法使用此功能将文档保存到用户的计算机上，而不向用户询问保存位置。）Content-Disposition就是当用户想把请求所得的内容存为一个文件的时候提供一个默认的文件名。


5. 一般来说著名的Linux系统基本上分两大类：1.RedHat系列：Redhat、Centos、Fedora等2.Debian系列：Debian、Ubuntu等
RedHat 系列
1 常见的安装包格式 rpm包,安装rpm包的命令是“rpm -参数”2 包管理工具 yum 3 支持tar包
Debian系列
1 常见的安装包格式 deb包,安装deb包的命令是“dpkg -参数”2 包管理工具 apt-get 3 支持tar包tar 只是一种压缩文件格式，所以，它只是把文件压缩打包而已。

6. IDE是英文Integrated Drive Electronics的缩写，翻译成中文叫做“集成驱动器电子装置”， 它的本意是指把控制器与盘体集成在一起的硬盘驱动器。通常我们所说的IDE指的是硬盘等设备的一种接口技术。
            目前，我们的电脑中标配的IDE设备无非两类——硬盘和光驱

7. ATA是广为使用的IDE和EIDE设备的相关标准。 sata指串行的ata，比ata快。 随着IDE/EIDE得到的日益广泛的应用，全球标准化协议将该接口自诞生以来使用的技术规范归纳成为全球硬盘标准，这样就产生了ATA（Advanced Technology Attachment）。 简单来说就是硬盘接口标准

8. raid分为软件raid和硬件raid

9. 把多个jar包打成一个jar包

10. cpu个数、核数、逻辑cpu数
        # 总核数 = 物理CPU个数 X 每颗物理CPU的核数
        # 总逻辑CPU数 = 物理CPU个数 X 每颗物理CPU的核数 X 超线程数

        # 查看物理CPU个数
        cat /proc/cpuinfo| grep "physical id"| sort| uniq| wc -l

        # 查看每个物理CPU中core的个数(即核数)
        cat /proc/cpuinfo| grep "cpu cores"| uniq

        # 查看逻辑CPU的个数
        cat /proc/cpuinfo| grep "processor"| wc -l

         查看CPU信息（型号）
        cat /proc/cpuinfo | grep name | cut -f2 -d: | uniq -c


11. md5  含义：消息摘要算法第五版，用于校验数据是否为原数据（消息的完整性保护），确保信息传输完整一致。

12. beeline中执行如下命令
	1、driver端想返回1000条记录，则在整个回话中设置属性
	      set spark.sql.thriftServer.limitCollectNumber = 1000
	2、driver端想全部返回查询记录条数，则在整个回话中设置属性
	      set spark.sql.thriftServer.limitCollectNumber = 0

13 window 下强制删除文件和文件夹
rd/s/q 盘符:\某个文件夹  （强制删除文件文件夹和文件夹内所有文件）
del/f/s/q 盘符:\文件名  （强制删除文件，文件名必须加文件后缀名）

         14. scp -r root@10.9.234.74:/home/netnumen/ems/ums-server/procs/ppus/webgis.ppu/webgis-web.pmu/webgis.ear/webgis.war /home/netnumen/ems/ums-server/procs/ppus/webgis.ppu/webgis-web.pmu/webgis.ear
