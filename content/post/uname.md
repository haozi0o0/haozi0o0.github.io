---
title: "uname"
date: 2020-07-19T08:54:39+08:00
draft: false
tags: [linux]
categories: [linux]
---
<!--more-->
# 关于linux操作系统的知识
uname  
>作用:获取计算机操作系统相关的信息 

#<font color=“greem”>uname </font> 
>//获取操作系统的类型 

#<font color=“greem”>uname -a  </font>
>//表示获取全部的系统信息（包括，类型、全部主机版本、内核版本、发布时间、开源计划）

#<font color=“greem”>nestart -tnlp  </font>
>//查看网络的连接状态   
>选项说明:  
>+ -t:表示只列出tcp协议的链接  
>+ -n:表示列出ip地址，将协议转化成端口号  
>+ -l:表示过滤出“state（状态）”列中其值为listen（监听）的连接  
>+ -p:表示显示发起连接的进程的PID和进程的名称  