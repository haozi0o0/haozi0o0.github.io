---
title: "shutdown"
date: 2020-07-19T08:54:39+08:00
draft: false
tags: [linux]
categories: [linux]
---
<!--more-->


# 关于linux关机的知识
shutdown    
作用:关机    
服务器慎用    
#<font color=“greem”>shutdown -h now</font>    
>//立即关机

#<font color=“greem”>shutdown -h （时间）</font>  
>//定时关机

>//按ctrl+c退出关机计划      
>//如果在centos7.x之前的版本：按ctrl+c退出关机计划    
>//如果在centos7.x之后的版本：#shutdown -c    
## 其他关机命令:    
<font color=“greem”>#init 0</font>    
<font color=“greem”>#halt  </font>  
<font color=“greem”>#poweroff  </font>  
> <font color=“greem”>#uptime  </font>   
//作用:输出计算机的持续在线时间（从计算机开机以来到现在运行的时间）  
