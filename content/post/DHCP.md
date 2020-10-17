---
title: dhcp服务
date: 2020-07-19T08:54:39+08:00
draft: false
tags: [linux]
categories: [linux]
---
<!--more-->


# Linux的网络服务之一      -----dhcp服务
## dhcp服务  
#<font color=“green”>rpm -q dhcp</font>  
>//检查是否安装dhcp服务  

#<font color=“green”>yum install -y dhcp</font>   
>//安装dhcp服务 

#<font color=“green”>service dhcpd start</font>

>//开启dhcp服务

#<font color=“green”>service dhcp restart</font>  
>//重启dhcp服务 
## <font color=“#FF00000”>注意:</font>
>在虚拟机上的编辑菜单中的虚拟网络编辑器中取消dhcp服务,
>由于取消了虚拟机网卡的dhcp服务，我们要给网卡手动配置一个ip。  
>linux上的dhcp服务分配的ip必须和你网卡的ip一样。 

#<font color=“green”>vi /etc/sysconfig/network-scripts/ifcfg-ens33</font>  
>//进入网卡的配置文件(ens33不是固定的) 
## 更改网卡配置文件:
<font color=“green”>bootproto=static</font>                                     
>//变成静态  

<font color=“green”>ONBOOT=yes</font>                                          
<font color=“green”>IPADDR=.....</font>                                               
>//ip地址 

<font color=“green”>NETMASK=.......</font>                                              
>//子网掩码 

<font color=“green”>GATEWAY=.....</font>
>//网关 ,网络上默认网关:8.8.8.8  

<font color=“green”>DNS1=........</font>
>//DNS服务  

配置完要重启网络服务  
#<font color=“green”>service network restart</font>  
>//重启网卡 

## 配置dhcp的配置文件:
#<font color=“green”>vi /etc/dhcp/dhcpd.conf</font>  
>//dhcp的配置文件

<font color=“green”>subnet 192.168.100.0 netmask 255.255.255.0{</font>    
>//定义网络地址和子网掩码

<font color=“green”>range 192.168.100.200 192.168.100.251;</font>    
>//分配ip地址的范围(写完加分号) 

<font color=“green”>option routers 192.168.100.2;</font>   
>//配置网关  

<font color=“green”>option domain-name-servers 8.8.8.8;</font>  
>//配置DNS  

<font color=“green”>default-lease-time 600;</font>  
>//配置租约时间(默认,单位为秒)  

<font color=“green”>max-lease-time 7200;</font>  
>//配置租约时间(最大,单位为秒)  

<font color=“green”>host xxx{</font>  
>//指定机器使用ip(xxx代表主机机器名，自行取名)  

<font color=“green”>hardware ethernet xx:xx:xx:xx:xx:xx:;</font>  
>//指定机器的物理地址(xxx代表指定机器的物理地址)  

<font color=“green”>fixed-address xxxxxx;</font>  
>//指定机器的ip地址(xxx代表你要给的ip地址)  

}  
}  
#<font color=“green”>service dhcp restar</font>   
>//重启dhcp服务  
## <font color=“#FF00000”>注意:</font>
>1.在dhcp配置文件中，记得要在第一段和最后一段后添加大括号，在大括号里面的每一条语句都要添加分号。  
>2.在文中的给指定PC设置ip可以不选择，看要求.
## 测试:  
设置客户端网卡为自动获取，如果不能获取，Linux进行安全设置  
#<font color=“green”>service  firewalld  stop</font>  
#<font color=“green”>setenforce  0</font>  

