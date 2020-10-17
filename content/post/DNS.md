---
title: "dns服务"
date: 2020-07-19T08:54:39+08:00
draft: false
tags: [linux]
categories: [linux]
---
<!--more-->
# Linux的网络服务之一     </br>    -----DNS服务
## DNS服务器
#<font color="#greem">rpm -q bind</font>  
>//检查DNS是否安装  

#<font color="greem">yum install -y bind</font>
>//安装DNS服务

#<font color="greem">service  firewalld  stop</font>
>//关闭防火墙

#<font color="greem">setenforce  0</font>
>//关闭安全策略

#<font color="greem">vi /etc/named.conf</font>
>//配置文件位置

## 配置文件更多信息
DNS的配置文件分为:主配置文件，全局配置文件,区域配置文件,正向配置文件，反向配置文件.


## 在主配置文件中

<font color="greem">listen-on port 53 { 127.0.0.1; };</font>  
>//指定dns服务的端口和ip，dns默认监听端口为53，any代表主机的任何ip(ipv4)

<font color="greem">listen-on-v6 port 53 { ::1; };</font>
>//ipv6的配置

<font color="greem">directory       "/var/named";</font>
>//程序的主目录

<font color="greem">allow-query     { localhost; };</font>
>//指定可以查询的客户端，any代表任意客户端,把127.0.0.1和localhost改成any即可。

<font color="greem">include "/etc/named.rfc1912.zones";</font>
>//区域配置文件的位置

#<font color="greem">vi /etc/named.rfc1912.zones</font>
>//进入解析配置文件


## 在解析配置文件中

配置解析配置文件

<font color="greem">
zone "myweb.com" IN {</br>
        type master; </br> 
        file "myweb.com.zheng";  </br>
        allow-update { none; }; </br> 
};</br> 
</font> 
<font color="greem">
zone "159.168.192.in-addr.arpa" IN { </br> 
        type master;  </br>
        file "192.168.159.fan";  </br>
        allow-update { none; }; </br> 
};</br>  
</font>    
文中的myweb.com是你的域名地址</br>
file "myweb.com.zheng";是此域名的正向解析地址，其中引号里的语句可以自定义更改</br>
文中的zone "159.168.192.in-addr.arpa" IN {是反向地址解析，语句159.168.192是你虚拟机或者服务器的ip地址的反向ip</br>
file "192.168.159.fan";是填写反向地址解析的配置文件，192.168.159.fan语句可以自定义</br>



## 配置正向/反向地址解析文件

### 配置正向/反向解析配置文件

#<font color="greem">cp -a named.localhost myweb.com.zheng</font></br>

>#named.localhost为正向解析的模板，复制后的文件名字必须是你配置解析文件中file "myweb.com.zheng";里的名字。</br>

<font color="greem">
正向地址解析协议</br>
$TTL 1D</br>
@       IN SOA  abc.com. rname.invalid. (</br>
                                        0       ; serial</br>
                                        1D      ; refresh</br>
                                        1H      ; retry</br>
                                        1W      ; expire</br>
                                        3H )    ; minimum</br>
        NS      dns.abc.com.</br>
        A       127.0.0.1</br>
        AAAA    ::1</br>
dns     A       192.168.100.128</br>
www     A       192.168.100.129</br>
</font>

abc.com.是你域名的地址
dns是主机名，192.168.100.128是对应的ip地址
www是主机名，192.168.100.129是对应的ip地址  

#<font color="greem">cp -a named.loopback 192.168.159.fan</font>
>#named.loopback为反向解析的模板

## 反向地址解析配置文件</br>
<font color="greem">
$TTL 1D</br>
@       IN SOA  abc.com. rname.invalid. (
                                        0       ; serial
                                        1D      ; refresh
                                        1H      ; retry
                                        1W      ; expire
                                        3H )    ; minimum
        NS      dns.abc.com.
        A       127.0.0.1
        AAAA    ::1
        PTR     localhost.
128     PTR     dns.abc.com
129     PTR     www.abc.com
</font>
abc.com.是你域名的地址
128是dns.abc.com的端口
129是www.abc.com的端口
即可完成反向地址解析
dns.abc.com的正/反解析ip必须是网卡的dns
使用nslookup 命令，就可以查看解析

