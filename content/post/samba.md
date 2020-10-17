---
title: "Samba服务"
date: 2020-07-19T08:54:39+08:00
draft: false
tags: [linux]
categories: [linux]
---
<!--more-->
# Linux网络服务之一        ------samba(文件共享)服务
## Samba服务(共享文件)
#<font color=“green”>rpm -q samba</font>
>//检查samba服务是否安装

#<font color=“green”>yum install -y samba</font>
>//安装samba

#<font color=“green”>service smb start</font>
>//启动samba服务

#<font color=“green”>systemctl stop firewalld</font>
>//停止防火墙

#<font color=“green”>setenforce 0</font>
>//设置关闭临时策略(临时)

#<font color=“green”>vi/etc/selinux/config</font> 

>//设置 SELINUX=disabled
>,永久设置安全策略

#<font color=“green”>vi/etc/samba/smb.conf</font>

>//smb的配置文件

## 在配置文件中

><font color=“green”>global</font>  
>//(全局配置)  

><font color=“green”>homes </font>   
>//(共享文件夹) 

><font color=“green”>print$</font>  
>//(共享打印机)
## 例子:配置匿名用户访问
### 对应配置:
<font color=“green”>[xxxx]</font>  
>//共享文件的名字

<font color=“green”>comment=XXX</font>  
>//共享描述

<font color=“green”>path=XXX</font>
>//共享的文件夹名称

<font color=“green”>browseable=yes</font>
>//共享目录是否显示，yes为显示，no为不显示

<font color=“green”>map to guest=bad user</font>
>//和browseable配套使用(此命令在全局配置中输入:允许匿名访问)

<font color=“green”>writable=yes</font>
>//共享目录是否可写，如果是yes需要同时设置共享的目录的用户权限为可写，可以使用chomd命令来设置  
>//注意:配置文件中的命令和文件夹的权限是两码事。

<font color=“green”>guest ok=yes</font>
>//是否允许匿名访问

<font color=“green”>service smb restart</font>
>//重启服务

<font color=“green”>testparm</font>
>//检查配置文件错误


### 注意:工作当中一般匿名用户是没有权限写入的

## 例子2:配置普通用户的访问
#<font color=“green”>useradd XXX</font>
>//添加用户

#<font color=“green”>smbpasswd -a XXX</font>
>//给xxx用户设置密码

<font color=“green”>writable=yes</font>
>//允许写入操作，同时要设置共享文件夹的权限

<font color=“green”>valid users=XXX</font>
>//可以访问的用户列表，如果多用户用逗号隔开

<font color=“green”>write list=XXX</font>
>//有写入权限的用户列表，如果多用户用逗号隔开  
>注意:如果有writable，会冲突，可以把writable删除掉

<font color=“green”>net use * /del /y</font>
>//删除用户登录信息（可以达到更换用户）

## 注意:<font color=“#FF00000”>
>此条命令是在win10/7的cmd里执行，进入cmd的方法:win+r键，然后输入cmd即可进入cmd</font>

# Win7注意:
## 如果前提配置文件都配置完整后还不能访问samba服务则:
>1.Win+r，然后输入secpol.msc  
>2.点击本地策略  
>3.点击安全选项  
>4.在右侧找到:网络安全:LAN管理器身份验证级别并更改为发送LM和HTLM-如果以协商，则使用NTLMv2会话安全即可。
# 如果设置了普通用户访问samba文件夹不能访问
>1.修改 /etc/samba/smb.conf，在Global项下增加:  
>2.client lanman auth = YES      
>3.lanman auth = YES  
>4.ntlm auth = YES   
>即可


