#CentOS安装JDK

首先卸载openJDk
第一步：查看Linux自带的JDK是否已安装 （卸载centOS已安装的1.4）

安装好的CentOS会自带OpenJdk,用命令 java -version ，会有下面的信息：

java version "1.6.0"
OpenJDK Runtime Environment (build 1.6.0-b09)
OpenJDK 64-Bit Server VM (build 1.6.0-b09, mixed mode)

最好还是先卸载掉openjdk,在安装sun公司的jdk.

先查看 rpm -qa | grep java

显示如下信息：

java-1.4.2-gcj-compat-1.4.2.0-40jpp.115
java-1.6.0-openjdk-1.6.0.0-1.7.b09.el5

卸载：

rpm -e --nodeps java-1.4.2-gcj-compat-1.4.2.0-40jpp.115
rpm -e --nodeps java-1.6.0-openjdk-1.6.0.0-1.7.b09.el5

1.在/usr/目录下创建java目录 

[root@localhost ~]# mkdir/usr/java
[root@localhost ~]# cd /usr/java

2.下载，然后解压

[root@localhost java]# curl -O http://download.oracle.com/otn-pub/java/jdk/7u79-b15/jdk-7u79-linux-x64.tar.gz 
[root@localhost java]# tar -zxvf jdk-7u79-linux-x64.tar.gz

3.设置环境变量

[root@localhost java]# vi /etc/profile

添加如下内容：

JAVA_HOME=/usr/java/jdk1.7.0_79
JRE_HOME=/usr/java/jdk1.7.0_79/jre
CLASS_PATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
export JAVA_HOME JRE_HOME CLASS_PATH PATH

让修改生效：

[root@localhost java]# source /etc/profile

4.验证

[root@localhost java]# java -version
java version "1.7.0_79"
Java(TM) SE Runtime Environment (build 1.7.0_79-b15)
Java HotSpot(TM) 64-Bit Server VM (build 24.79-b02, mixed mode)

#centOS装tomcat
[root@admin local]# cd /usr/local  
[root@admin local]# wget http://apache.fayea.com/apache-mirror/tomcat/tomcat-7/v7.0.57/bin/apache-tomcat-7.0.57.tar.gz  
[root@admin local]# tar -zxv -f apache-tomcat-7.0.29.tar.gz // 解压压缩包  
[root@admin local]# rm -rf apache-tomcat-7.0.29.tar.gz // 删除压缩包  
[root@admin local]# mv apache-tomcat-7.0.29 tomcat 

#centos6.5关闭防火墙
关闭命令：  service iptables stop
        永久关闭防火墙：chkconfig iptables off

两个命令同时运行，运行完成后查看防火墙关闭状态
        service iptables status 

#centos7关闭防火墙
systemctl stop firewalld.service #停止
systemctl disable firewalld.service #禁用
之前的版本：
service iptables stop #停止
chkconfig iptables off #禁用

#centOS装mysql数据库
http://www.cnblogs.com/xiaoluo501395377/archive/2013/04/07/3003278.html
