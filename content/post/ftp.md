---
title: "ftp服务"
date: 2020-07-19T08:54:39+08:00
draft: false
tags: [linux]
categories: [linux]
---
<!--more-->
# Linux的网络服务之一    -----FTP服务
## 安装ftp软件(vsftpd)  
>安装方式1:  
>通过光盘，优盘等存储介质安装(本地安装)  
>方式2:  
>网络安装(已经配置网络能够正常访问) 

#<font color=“green”>yum install -y vsftpd</font>
>//通过网络安装vsftpd服务  

#<font color=“green”>rpm -q vsftpd</font>   
>//确认软件是否安装
## 配置ftp服务

#<font color=“green”>service vsftpd start</font>  
>//启动(临时，每次重启都得开启)    

#<font color=“green”>service vsftpd stop </font>   
>//停止vsftpd服务

#<font color=“green”>service vsftpd restart </font> 
>//重启ftp服务  

#<font color=“green”>systemctl enable vsftpd </font> 
>//每次开机自启动vsftpd服务

## 安全设置  
#<font color=“green”>systemctl stop firewalld</font>  
>//关闭防火墙  

#<font color=“green”>systemctl status firewalld</font>      
>//查看防火墙状态 

#<font color=“green”>systemctl start firewalld</font>  
>//启动防火墙

#<font color=“green”>setenforce 0</font>            
>//关闭安全策略或设置配置文件 /etc/selinux/config  设置 SELINUX=disabled(临时)   

#<font color=“green”>firewall-cmd --permanent --zone=public --add-service=ftp</font>   
>//允许通过vsftpd服务的通过  

<!-- firewall-cmd --reload  
//重新加载防火墙  
--permanent有这个则ftp服务永久通过  
--zone=public也可以不写  
或关闭或设置selinux 允许ftp服务  
方式1:setsebool ftpd_full_access on  
//设置允许ftp-->  
## 访问ftp服务器  
>在计算机里输入ftp://linux的ip地址  
>在浏览器里输入ftp://linux的ip地址  
>在cmd里输入 ftp linux的ip地址  
>默认匿名用户的名字Anonymous  
>密码为空密码  
## 匿名用户
#<font color=“green”>cd /var/ftp</font>
>//vsftpd对于匿名用户的存储位置   

#<font color=“green”>cd /home</font>  
>//vsftpd对于登录用户的文件存储位置是  
  
## 配置ftp服务的文件
#<font color=“green”>etc/vsftpd/vsftpd.conf </font>  
>//vtp的配置文件位置
 
<font color=“green”>anonymous_enable=YES</font> 
>//设置匿名用户是否可以访问(第12行)  

<font color=“green”>load_enable=YES</font>  
>//允许本地用户访问(第16行)  

<font color=“green”>write_enable=YES</font>  
>//所有用户是否可写(第19行)  

#<font color=“green”>anon_upload_enbale=YES </font> 
>//前面有#是被注释掉了，不执行 ,匿名用户是否可以上传(第29行)

<font color=“green”>anon_mkdir_write_enable=YES </font> 
>//是否匿名用户是否可以创建目录（第33行）

<font color=“green”>anon_other_write_enable=YES</font>  
>//打开匿名用户删除和重新命名的权限(手动添加)

## <font color=“#FF00000”>注意:</font>
>1.配置完之后重启服务  
2.除了设置设置配置文件，还要更改文件的读、写、可读权限。  
anon_umask=022  
//匿名用户的掩码(如果需要，自己添加，含义:如umask是022，这时新建一个权限为666的文档，文件的实际权限为666-022=644)   
umask是在linux中常见的一个东西，它其实是一个掩码。当然，也有umask这样一个命令，它是对用户建立的文件的默认属性的定义。该 定义为：
假设umask为022，则对于一个文件夹的话，它的默认属性为 777-022=755,这也就是我们平时建立文件夹的权限。而对于一般的文件的话，则是用 666-022=644.


## 普通用户访问ftp配置  
 
<font color=“green”>ftpusers=</font>     
>//黑名单，写在这个里的用户不能访问 

<font color=“green”>user_list=</font>  
>//黑白(名单)即可,如果不经过配置，默认的是黑名单   
怎么配置才能变成白名单呢？    
在user_list=的后面添加用户即可。 

<font color=“green”>userlist_enable=YES</font>  
>//用户列表文件是否启用 

<font color=“green”>userlist_deny=YES</font>       
>//用户列表是否为黑名单，YES（user_list）为黑名单，NO为白名单

<font color=“green”>userlist_file=1.txt(文件)</font>  
>//指定文件,在1.txt里设置白名单
  



