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
#<font color=“greem”>mkfs （参数） （格式化的文件系统类型）（分区名称）</font>    
+ <font color=“greem”>-t </font> 
>//指定要创建的文件系统类型（常见ext类型）  
+ <font color=“greem”>-c </font> 
>//建立文件系统先检查坏块  
+ <font color=“greem”>-l file </font> 
>//从文件file中读磁盘坏块列表，file文件一般是由磁盘坏块检查程序产生的  
+ <font color=“greem”>-V </font> 
>//输出建立文件系统详情信息  
# 检查文件系统的正确性  
+ <font color=“greem”>fsck （参数）（分区名称）</font>  
## 参数: 
+ <font color=“greem”>-t</font>  
>//给定文件系统类型，若在/etc/fstab中已有定义或kernel本身以支持的不需添加此项  
+ <font color=“greem”>-s</font> 
>//一个一个地执行fsck命令进行检查  
+ <font color=“greem”>-A</font>  
>//对/etc/fstab中所有列出来的分区进行检查  
+ <font color=“greem”>-C</font>  
>//显示完整的检查进度  
+ <font color=“greem”>-d</font>  
>//列出fsck的debug结果  
+ <font color=“greem”>-P</font>  
>//在同时有-A选项时，多个fsck的检查一起执行  
+ <font color=“greem”>-a</font>  
>//如果检查中发现错误，则自动修复  
+ <font color=“greem”>-r</font>  
>//如果检查有错误，询问是否修复  
# 文件的挂载与卸载 
#<font color=“greem”>mount （选项（可有可无））（分区）（挂载点）</font>  
例如：  
>mount -t ext3/dev/sdb1 /mnt/m1

<br>卸载命令格式：  
 + #<font color=“greem”>umount 分区|挂载点</font>  
例如：  
 > umount /dev/sdb1

## 自动挂载：  
1.设置开机自动挂载，查看磁盘UUID信息  
#<font color=“greem”>blkid</font>   
2.增加自动挂载磁盘信息， 修改（vim /etc/fstab）配置文件：  
#<font color=“greem”>vi/etc/fstab</font>  
3.添加以下信息  
UUID=f495dd82-2924-4af4-9262-d4a71f1156e3 /data ext4 defaults 0 0  
>//UUID是你要挂载的硬盘的UUID

4.查看    
#<font color=“greem”>mount -a </font> 
