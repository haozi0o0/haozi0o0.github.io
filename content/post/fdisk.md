---
title: "fdisk"
date: 2020-07-19T08:54:39+08:00
draft: false
tags: [linux]
categories: [linux]
---
磁盘管理
<!--more-->

# fdisk磁盘分区操作  
>+ 接口：SCSI和IDE和SATA  
主分区（最多1-4个）、扩展分区（最多0-1个）、逻辑分区（无数个）  
磁盘编号：由三位字母与一位数字组成  
主分区：/dev/sdb1、/dev/sdb2  
扩展分区：/dev/sdb3  
逻辑分区：/dev/sdb5、/dev/sdb6......（以此类推） 
+ #<font color=“greem”>fdisk -l </font>  
>查看分区情况  
+ #<font color=“greem”>fdisk /dev/sdb</font>    
>进入磁盘编辑模式      
## 子命令：  
+ <font color=“greem”>n</font>   
>//新建一个分区  
+ <font color=“greem”>p </font>   
>//列出分区表  
+ <font color=“greem”> l </font>   
>//显示分区文件类型列表  
+ <font color=“greem”>t  </font>  
>//改变分区文件类型  
+ <font color=“greem”>m   </font> 
>//列出帮助信息  
+ <font color=“greem”>d  </font>  
>//删除分区  
+ <font color=“greem”>w  </font>    
>//保存分区  
+ <font color=“greem”>q  </font>   
>//不保存退出分区  
## 磁盘的格式化操作  
#<font color=“greem”>mkfs（格式化的文件系统类型）（分区名称）</font> 
# 文件的挂载与卸载 
#<font color=“greem”>mount （选项（可有可无））（分区）（挂载点）</font>  
例如：  
>mount /dev/sdb1 /mnt/m1

<br>卸载命令格式：  
 + #<font color=“greem”>umount 分区|挂载点</font>  
例如：  
 > umount /dev/sdb1 /mnt/m1

## 自动挂载：  
1.设置开机自动挂载   
2.增加自动挂载磁盘信息， 修改（vim /etc/fstab）配置文件：  
#<font color=“greem”>vi/etc/fstab</font>  
3.添加以下信息  

## gdisk分区格式：（gpt格式，没有主分区和扩展分区的概念了）  
gdisk （要分区的磁盘）

> //进入分区，开始划分

里面和fdisk一样，保存后要格式化才能使用

