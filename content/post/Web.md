---
title: "Web服务"
date: 2020-07-19T08:54:39+08:00
draft: false
tags: [linux]
categories: [linux]
---
<!--more-->
# Linxu中的网络服务之一    <p>----Web服务(httpd)</p>
#<font color=“green”>rpm -q httpd</font>  
>//检查Web服务是否安装

#<font color=“green”>yum install -y httpd</font>  
>//安装httpd软件包  

#<font color=“green”>service httpd start</font>  
>//启动httpd服务  

#<font color=“green”>service  firewalld  stop</font>  
>//关闭防火墙  

#<font color=“green”>setenforce  0</font>  
>//关闭安全策略  

#<font color=“green”>cd /var/www/html</font>  
>//默认网页的文本储存位置  
>//var是用户文件  

#<font color=“green”>vi index.html</font>  
>//是网站(index)默认(首页)的文档  

#<font color=“green”>vi /etc/httpd/conf/httpd.conf</font>  
>//http的配置服务  
## 配置文件里的参数(全局配置):  
<font color=“green”>ServerRoot "/etc/httpd"(31行)</font>  
>//软件包总目录  

<font color=“green”>Listen 80</font>   
>//设置服务的端口，默认省略ip，表示监听本机所有ip的80端口，如果添加其他端口在下一行输入Listenxx即可  

<font color=“green”>Include conf.modules.d/*.conf </font> 
>//补充服务，Include(路径) ,引用      

<font color=“green”>
User</br>
Group</font>  

>//当阿帕奇安装的时候，系统会自动创建一个用户和用户组,(66行和67行)  


<font color=“green”>
< Directory ></br> 
AllowOverride none</br>    
Require all denied|granted</br>      
< /Directory ></font>  

>//网站目录的访问权限，默认都是拒绝的(102行-105行)，如果设置成granted表示允许访问。

<font color=“green”>DocumentRoot "/var/www/html"</font>  
> //网站的根目录(119行) 

<font color=“green”>< IfModule dir_module>  
  DirectoryIndex index.html  
  < /IfModule></font>  

>//设定网站的默认页(首页,162行-164行)  

<font color=“green”>IncludeOptional conf.d/*.conf</font> 

>//加载其他的配置文件(352行),/etc/httpd/conf.d/ (完整路径)  


# 基于多个ip地址的虚拟主机  
### 实现多个网站，一个端口，多ip实现  
为主机网卡配置多个ip  
临时增加ip  
#<font color=“green”>ip addr add 192.168.159.128/24 dev ens33</font> 

>//临时配置多ip，然后重启，再次重启后就消失  
## 如何配置永久的单网卡多ip  
1.#<font color=“green”>cd /etc/sysconfig/network-scripts/</font>  
  >//进入网卡配置文件  

2.#<font color=“green”>vi ifcfg-ens33</font> 
  >//目前已经配置了一个ip  

3.#<font color=“green”>cp ifcfg-ens33 ifcfg-ens33:1</font> 
  >//在同等目录复制出一个一样的网卡配置文件，:1为网卡的子接口  

4.#<font color=“green”>vi ifcfg-ens33:1</font> 

  >//进入ens33:1配置文件，修改配置DEVICE="ens33:1",然后在更改ip地址即可。  

# 实现多ip一个端口:  
在httpd配置文件里增加:  
a文件  
<font color=“green”>< VirtualHost 192.168.159.120:80></font>   
<font color=“green”>ServerName a.com </font>
>//域名  

<font color=“green”>DocumentRoot "/a"</font>
>//根目录

<font color=“green”>< Directory "/a">  
AllowOverride none  
Require all granted  
< /Directory>  
< /VirtualHost> </font>

b文件  
<font color=“green”>< VirtualHost 192.168.159.121:80> </font> 
<font color=“green”>ServerName a.com</font>
>//域名  

<font color=“green”>DocumentRoot "/b" </font>
>//根目录

<font color=“green”>< Directory "/b">  
AllowOverride none  
Require all granted  
< /Directory>  
< /VirtualHost> </font> 

# 实现单ip多端口的http配置  
## 只需更改:  
<font color=“green”>< VirtualHost 192.168.159.121:80>    
...  
< /VirtualHost></font>  
<font color=“green”>< VirtualHost 192.168.159.121:801>    
...  
< /VirtualHost> </font>   
### 还要在Listen 80处添加语句来表示你新添加的端口号  
#<font color=“green”>httpd -t </font> 
>//检查配置文件错误  

