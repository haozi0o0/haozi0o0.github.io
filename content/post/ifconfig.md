---
title: "ifconfig"
date: 2020-07-19T08:54:39+08:00
draft: false
tags: [linux]
categories: [linux]
---
<!--more-->


# 关于linux(ifconfig)网络的知识   
作用:用于操作网卡相关指令    
#<font color=“greem”>ifconfig </font>
>//获取网卡信息  
#<font color=“greem”>vi /etc/sysconfig/network-scripts/ifconfig-XXX</font>      
>//进入XXX网卡配置文件

><font color=“greem”>inet addr </font>  
>//ip地址    
><font color=“greem”>netmask</font>                               
>//子网掩码    
><font color=“greem”>ipaddr</font>    
>//配置文件的ip地址  
><font color=“greem”>GATEWAY</font>   
>//网关地址  
><font color=“greem”>DNS</font>   
>//DNS服务  
## 在网卡配置文件里更改ip操作  
>1.bootproto=static                                      
>//变成静态  
>2.ONBOOT=yes
>//在系统启动时，是否启动网卡                                          
>3.IPADDR=.....                                               
>//ip地址  
>4.NETMASK=.......                                              
>//子网掩码  
>5.GATEWAY=......                                                   
>//网关，网络上默认网关:8.8.8.8  
>6.DNS1=........                                                  
>//DNS服务  
>7.配置完要重启网络服务  
>#<font color=“greem”>service network restart</font> 或 <font color=“greem”>systemctl restart network </font>  
>//reh7或者centos7以上版本可以使用  
>>启动网络服务:  
>>#<font color=“greem”>service network start</font>或 <font color=“greem”>systemctl start network</font>   
>>//(reh7或者centos7以上版本可以使用)  
>>>停止网络服务:    
>#<font color=“greem”>service network stop</font> 或 <font color=“greem”>systemctl stop network</font>  
>// (reh7或者centos7以上版本可以使用)  
>>>客户端域名解析服务器的配置文件（临时修改dns）:  
>#<font color=“greem”>/etc/resolv.conf</font>        
>//DNS客户机配置文件（重启会被重置）    
## reboot指令  
>>作用:重新启动计算机  
#<font color=“greem”>reboot -w </font>  
作用:模拟重启，达到只写关机和开机的日志  
# ping
作用:网络检测命令   
#<font color=“greem”>ping（参数）（主机名或ip地址）</font>  
>参数:  
-c  
//数目:在发送指定数目的包后停止  
-i  
//秒数:设定间隔几秒发送一个网络包给另一台机器，预设值是一秒  
-s  
//字节数:指定发送的数据字节数，预设值56，加上8字节的ICMP头，一共是64ICMP数据字节  
-t  
//存活数值:设置存活数值TTL的大小  
>例如:
>#<font color=“greem”>ping -c 3 192.168.1.20</font>
# nmcli
作用:设置网络状态信息    
#<font color=“greem”>nmcli（参数） （命令）</font>    
>参数:  
>connection:连接设备  
>device:设备  
>例如:  
>显示连接:  
>#<font color=“greem”>nmcli connection show </font>   
>//查看连接状态:    
>#<font color=“greem”>nmcli device status  </font>  
>//启用连接eth0    
>#<font color=“greem”>nmcli connection up eth0</font>    
>//创建新连接neweth0    
# route
作用:查看路由表信息  
<font color=“greem”>#ROUTE</font>  
>例如:添加一条默认路由:  
 #<font color=“greem”>rout add default gw 192.168.0.254 </font> 
