# python
实践出真知——一文教你搭建Nginx+Tomcat集群，实现负载均衡及动静分离
前言
​ 想必大家对于Nginx和Tomcat都非常熟悉了，Nginx的应用非常广泛，不仅是对web静态资源非常友好，而且也是非常实用的反向代理和负载均衡软件。结合后端Tomcat的服务，从而搭建Nginx+Tomcat集群。

​ 对于直接想要实践的朋友而言可以获取本文的链接中的软件包后直接看第三备份的内容。

一、集群搭建结构及拓扑
1.1集群架构图示
Nginx+Tomcat集群的结构示意图如下：

实践出真知——一文教你搭建Nginx+Tomcat集群，实现负载均衡及动静分离

1.2系统环境与地址规划
使用三台Centos7服务器（7.4），规划如下：

服务器	网卡模式	IP地址
Nginx	NAT	20.0.0.128
Tomcat1	NAT	20.0.0.130
Tomcat2	NAT	20.0.0.136
1.3拓扑图如下
实践出真知——一文教你搭建Nginx+Tomcat集群，实现负载均衡及动静分离

1.4相关资源软件
链接：https://pan.baidu.com/s/1Qdla-vrpcspcAKJucZdSUg
提取码：40it

二、搭建思路及核心部分配置
​ 根据上述的结构图示，为了完成该实践内容，需要先梳理搭建的思路，搞清楚核心部分的操作与配置。

1、首先我们需要在三台服务器上编译安装对应的服务（软件包在上面的链接中），测试服务是否正常；

2、其次基于核心功能：负载均衡以及动态分离，需要一步一步理清楚

基于负载均衡
​ 负载均衡是在Nginx服务器上配置的，就需要对nginx的主配置文件进行配置，实现负载均衡的模块是使用upstream模块以及对应需要的算法（本文使用简单的加权轮循算法实现负载均衡）。核心配置：

#server指令外层
upstream tomcat-server {
                server 20.0.0.130:8080 weight=1;
                server 20.0.0.136:8080 weight=1;
        }
#server指令中
location / {
            root   html;
            index  index.html index.htm;
            proxy_pass http://tomcat-server;
        }
访问nginx的服务器地址，可以轮循访问后端的两台真实的Tomcat服务器。

基于动态分离
​ 我们知道对于Nginx而言，其对静态资源的支持是非常友好的，而Tomcat对于java的动态web页面的支持非常好。所以需要实现动态分离就是将静态请求给予nginx服务器运行，Tomcat负责处理类似jsp文件的动态请求。

​ 本次案例使用nginx服务器和一台Tomcat服务器做动态分离。最终将结合静态图片让nginx负责处理，而使用Tomcat处理动态页面。

核心配置：

nginx服务器：

location ~.*\.(gif|jpg|jpeg|png|bmp|swf|css)$ {
            root html/demo;
            expires 30d;
        }
location ~.*.jsp$ {       ##匹配jsp页面跳转代理服务器池
           proxy_pass http://tomcat-server;
           proxy_set_header Host $host;
        }
 location / {
            root   html;
            index  index.html index.htm;
            #proxy_pass http://tomcat-server;
        }
tomcat服务器：


        <Context docBase="/usr/local/tomcat/webapps/demo" path="" reloadable="false">
         </Context>
3、在部署和配置的过程中，进行必要的验证

好了大致的流程和核心配置讲完了，下面开始本次案例的完整演示。

三、部署流程与实践过程
负载均衡集群搭建
3.1部署配置两个tomcat服务器
​ 由于部署两个tomcat服务器的流程几乎一致（除了页面显示的内容部分不一致，当然是为了验证负载均衡），并且不显得本文过于冗长，就演示tomcat1服务器上的部署。

3.1.1安装jdk
====================================================================================
tomcat1
[root@localhost ~]# hostnamectl set-hostname tomcat1
[root@localhost ~]# su
[root@tomcat1 ~]# cd /opt/
[root@tomcat1 opt]# ls
apache-tomcat-9.0.16.tar.gz  jdk-8u91-linux-x64.tar.gz  rh
[root@tomcat1 opt]# tar zxf jdk-8u91-linux-x64.tar.gz -C /usr/local/
[root@tomcat1 opt]# vim /etc/profile  #声明环境变量
#末尾
export JAVA_HOME=/usr/local/jdk1.8.0_91
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_NAME}/bin:$PATH
[root@tomcat1 opt]# source /etc/profile
3.1.2部署安装tomcat
[root@tomcat1 opt]# ls
apache-tomcat-9.0.16.tar.gz  jdk-8u91-linux-x64.tar.gz  rh
[root@tomcat1 opt]# tar zxf apache-tomcat-9.0.16.tar.gz -C /usr/local/
[root@tomcat1 opt]# cd /usr/local/
[root@tomcat1 local]# ls
apache-tomcat-9.0.16  bin  etc  games  include  jdk1.8.0_91  lib  lib64  libexec  sbin  share  src
[root@tomcat1 local]# mv apache-tomcat-9.0.16/ tomcat
[root@tomcat1 local]# cd tomcat/
[root@tomcat1 tomcat]# ls
bin           conf             lib      logs    README.md      RUNNING.txt  webapps
BUILDING.txt  CONTRIBUTING.md  LICENSE  NOTICE  RELEASE-NOTES  temp         work
[root@tomcat1 bin]# ls  #将下面中的启动脚本和关闭脚本建立软链接
bootstrap.jar       ciphers.sh                    daemon.sh     setclasspath.bat  startup.sh            version.bat
catalina.bat        commons-daemon.jar            digest.bat    setclasspath.sh   tomcat-juli.jar       version.sh
catalina.sh         commons-daemon-native.tar.gz  digest.sh     shutdown.bat      tomcat-native.tar.gz
catalina-tasks.xml  configtest.bat                makebase.bat  shutdown.sh       tool-wrapper.bat
ciphers.bat         configtest.sh                 makebase.sh   startup.bat       tool-wrapper.sh
[root@tomcat1 bin]# ln -s /usr/local/tomcat/bin/startup.sh /usr/local/bin
[root@tomcat1 bin]# ln -s /usr/local/tomcat/bin/shutdown.sh /usr/local/bin

#创建站点目录以及文件（web页面）
[root@tomcat1 local]# mkdir -p /web/webapp1
[root@tomcat1 local]# cd /web/webapp1/
[root@tomcat1 webapp1]# vim index.jsp
<%@ page language="java" import="java.util.*" pageEncoding="UTF-8"%>
<html>
 <head>
    <title>JSP test1 page</title>  #网页标题名字
 </head>
 <body>
    <% out.println("Welcome tomcat1 Web");%> #网页内容为：welcome tomcat1 web 唯一需要在tomcat2上面更改配置的部分（再次声明这样是为了验证效果，生产环境中是一致的哈~）
 </body>
</html>
[root@tomcat1 webapp1]# vim /usr/local/tomcat/conf/server.xml #配置服务文件在149行添加context标签语句 
148       <Host name="localhost"  appBase="webapps"
149             unpackWARs="true" autoDeploy="true">
150          <Context docBase="/web/webapp1" path="" reloadable="false">
151          </Context>
[root@tomcat1 webapp1]# startup.sh #开启服务
Using CATALINA_BASE:   /usr/local/tomcat
Using CATALINA_HOME:   /usr/local/tomcat
Using CATALINA_TMPDIR: /usr/local/tomcat/temp
Using JRE_HOME:        /usr/local/jdk1.8.0_91/jre
Using CLASSPATH:       /usr/local/tomcat/bin/bootstrap.jar:/usr/local/tomcat/bin/tomcat-juli.jar
Tomcat started.
[root@tomcat1 webapp1]# netstat -ntap | grep 8080 #检查tomcat服务是否开启
tcp6       0      0 :::8080                 :::*                    LISTEN      2020/java 

[root@tomcat1 webapp1]# systemctl status firewalld.service  #查看防火墙对防火墙进行设置
● firewalld.service - firewalld - dynamic firewall daemon
   Loaded: loaded (/usr/lib/systemd/system/firewalld.service; enabled; vendor preset: enabled)
   Active: active (running) since 日 2020-04-05 11:04:32 CST; 19min ago
   ......
[root@tomcat1 webapp1]# firewall-cmd --zone=public --add-port=8080/tcp --permanent
success
[root@tomcat1 webapp1]# firewall-cmd --reload
success
3.2部署配置nginx服务器
3.2.1手工编译安装nginx服务（这里不必多说了哈）
[root@nginx opt]# tar zxf nginx-1.12.0.tar.gz -C /usr/local/
[root@nginx opt]# yum install -y gcc gcc-c++ make zlib-devel pcre-devel

[root@nginx opt]# useradd -M -s /sbin/nologin nginx
[root@nginx opt]# cd /usr/local/nginx-1.12.0/
[root@nginx nginx-1.12.0]# ./configure --prefix=/usr/local/nginx --user=nginx --group=nginx --with-http_stub_status_module --with-http_gzip_static_module --with-http_flv_module
[root@nginx nginx-1.12.0]# make && make install
[root@nginx nginx-1.12.0]# ln -s /usr/local/nginx/sbin/nginx /usr/local/sbin/
3.3配置验证实现负载均衡
3.3.1upstream模块实现负载均衡
[root@nginx nginx-1.12.0]# vim /usr/local/nginx/conf/nginx.conf
#在nginx.conf的gzip下面写入tomcat服务器池，tomcat-server表示一个名称，可以理解为服务器的域名
#gzip  on;

    upstream tomcat-server {
                server 20.0.0.130:8080 weight=1;#根据加权轮循算法调度访问后端的tomcat服务器
                server 20.0.0.136:8080 weight=1;
                }
location / {
            root   html;
            index  index.html index.htm;
            proxy_pass http://tomcat-server; #配置代理服务器
        }
[root@nginx nginx-1.12.0]# nginx -t #检查配置文件的语法
nginx: the configuration file /usr/local/nginx/conf/nginx.conf syntax is ok
nginx: configuration file /usr/local/nginx/conf/nginx.conf test is successful
[root@nginx nginx-1.12.0]# nginx #启动服务
[root@nginx nginx-1.12.0]# netstat -napt | grep nginx
tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN      53804/nginx: master 
[root@nginx nginx-1.12.0]# firewall-cmd --zone=public --add-port=80/tcp --permanent
success
[root@nginx nginx-1.12.0]# firewall-cmd --reload
success
3.3.2验证负载均衡
​ 客户机上访问nginx服务器地址，然后刷新一次，结果如下面两张图：

实践出真知——一文教你搭建Nginx+Tomcat集群，实现负载均衡及动静分离

实践出真知——一文教你搭建Nginx+Tomcat集群，实现负载均衡及动静分离

动态分离实现过程演示
​ 此次只是为了实现动静分离的目的，所以只需要进行必要的演示即可，采用nginx服务器和一台tomcat服务器即可。

3.4模拟访问动静态资源（非同一web页面）
为了方便管理还是推荐写一个nginx服务的管理脚本

[root@nginx nginx-1.12.2]# vim /etc/init.d/nginx  ##编写service启动脚本
#!/bin/bash
# chkconfig: - 99 20
# description: Nginx Service Control Script
PROG="/usr/local/nginx/sbin/nginx"
PIDF="/usr/local/nginx/logs/nginx.pid"
case "$1" in
    start)
        $PROG
        ;;
    stop)
        kill -s QUIT $(cat $PIDF)
        ;;
    restart)
        $0 stop
        $0 start
        ;;
    reload)
        kill -s HUP $(cat $PIDF)
        ;;
    *)
                echo "Usage: $0 {start|stop|restart|reload}"
                exit 1
esac
exit 0
[root@nginx nginx-1.12.2]# chmod +x /etc/init.d/nginx 
[root@nginx nginx-1.12.2]# chkconfig --add nginx
3.4.1暂时注释原有的nginx的代理服务配置
location / {
            root   html;
            index  index.html index.htm;
            #proxy_pass http://tomcat-server;
        }
3.4.2修改默认的站点目录文件（显示页面）（声明nginx作为静态资源访问的请求处理端）
[root@nginx html]# vim index.html
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p><em>this is a static web page.</em></p> #em表示斜体
</body>
</html>
重启服务此时访问nginx服务器，获取的是：

实践出真知——一文教你搭建Nginx+Tomcat集群，实现负载均衡及动静分离

3.4.3在tomcat1上写一个jsp的动态页面
#创建一个站点目录demo，编写一个jsp脚本
vim /usr/local/tomcat/webapps/demo/index.jsp 
<!DOCCTYPE html>
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<%@ page import="java.util.Date" %>
<%@ page import="java.text.SimpleDateFormat" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/ html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>动态页面</title>
</head>
<body>
<div>动态页面1</div>
</body>
</html>

更改server.xml
<Host name="localhost"  appBase="webapps"
            unpackWARs="true" autoDeploy="true">
        <Context docBase="/usr/local/tomcat/webapps/demo" path="" reloadable="false">
         </Context>
        <!--<Context docBase="/web/webapp1" path="" reloadable="false">
         </Context> -->
那么此时在nginx服务器上需要location对访问的jsp文件进行ip跳转访问的配置：

location ~.*.jsp$ {       ##匹配jsp页面跳转代理服务器池
           proxy_pass http://tomcat-server;
           proxy_set_header Host $host;
        }
3.4.4测试验证
实践出真知——一文教你搭建Nginx+Tomcat集群，实现负载均衡及动静分离

3.5对于同一web页面实现动态访问tomcat，静态资源从nginx上获取
使用一张图片作为jsp文件，其中包含一张jpg格式的图片从nginx服务器上获取

具体配置如下

nginx上：需要创建demo目录（demo和tomcat上的目录的名称必须一致）存放jpg

#首先取消上面的代理注释内容，因为测试的时候访问的是20.0.0.128
server {
        listen       80;
        server_name  localhost;

        location ~.*\.(gif|jpg|jpeg|png|bmp|swf|css)$ {
            root html/demo;
            expires 30d;
        }
        #charset koi8-r;

        #access_log  logs/host.access.log  main;
        location ~.*.jsp$ {       ##匹配jsp页面跳转代理服务器池
           proxy_pass http://tomcat-server;
           proxy_set_header Host $host;
        }
        location / {
            root   html;
            index  index.html index.htm;
            proxy_pass http://tomcat-server;
        }
tomcat：

jsp文件中添加一个图片链接：

[root@tomcat1 demo]# vim /usr/local/tomcat/webapps/demo/index.jsp 
<!DOCCTYPE html>
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<%@ page import="java.util.Date" %>
<%@ page import="java.text.SimpleDateFormat" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/ html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>动态页面</title>
</head>
<body>
<div>动态页面1</div><br>
<img src="cat.jpg"> #添加的内容
</body>
</html>
~         
jsp资源：在demo目录下

[root@tomcat1 demo]# ls
index.jsp
图片资源在：html目录下

[root@nginx html]# ls
50x.html  demo  index.html
[root@nginx html]# cd demo/
[root@nginx demo]# ls
cat.jpg
[root@nginx demo]# 
此时重启nginx服务访问20.0.0.128

第一次访问的是文字+图片，第二次由于在第二台服务器上没有进行相关配置则访问内容依旧和之前负载均衡的内容一样。

实践出真知——一文教你搭建Nginx+Tomcat集群，实现负载均衡及动静分离

实践出真知——一文教你搭建Nginx+Tomcat集群，实现负载均衡及动静分离

简单总结
​ 其实结合此次实践，可以理解如何将动静分离和负载均衡结合起来，从而搭建nginx+tomcat集群服务了。如果说最后实现动态文字所代表的动态资源，加上这个可爱的小猫代表的静态资源（理解动静分离），结合前面的负载均衡完善tomcat2服务器配置就可以根据算法实现负载均衡了。

​ 总之，我们需要对配置文件非常熟悉，了解其功能模块，最后需要明白是如何基于各种模块或指令上下文进行访问跳转的，匹配的关系需要理清楚（逻辑关系）。
