---
title: "chmod"
date: 2020-07-19T08:54:39+08:00
draft: false
tags: [linux]
categories: [linux]
---
<!--more-->



# chmod文件权限应用  
#<font color="greem"> ll (文件路径) </font>   
> //查看文件权限信息   
>例如:-:rw-:r--:r--:.root:root:19mb:03月17:19:43:passwd  
>详细:(文件类型)(文件所属者权限)(文件组权限)(其他用户权限)(所属者)(所属用户)(文件大小)(创建时间)(文件名)  
>>rw-r--r--  
>>rwx(读、写、运行)  
>>-(代表没有这个权限)  
>>>文件类型:  
管道文件  (p)  
链接文件  (l)  
块设备文件  (b)  
# chmod命令  (修改文件权限)  
#chmod<font color="FF1493"> [给谁]</font><font color="A0522D">[+或者-或＝]</font><font color="#0000FF">[mode]</font><font color="FF00FF">[文件名]  </font>  
>＋//添加权限  
> —//删除权限  
>＝//添加新的权限删除以前的权限    
>>u//文件或目录的所有者    
>>g//组用户  
>>o//其他用户  
>>a//所有    
>>> 每种身份的数字类型:  
 r:4  
 w:2  
 x:1  
 o:0  
可以连写，比如u+rwx，g+rwx，中间用逗号隔开即可。