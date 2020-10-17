---
title: "Useradd"
date: 2020-07-19T08:54:39+08:00
draft: false
tags: [linux]
categories: [linux]
---
用户和组的基本信息
<!--more-->



# 组和用户的详细信息与操作  （重点）  
## 用户的配置和修改
#<font color=“greem”>useradd （用户名）</font>            
>// 创建一个用户

#<font color=“greem”>tail /etc/passwd</font>             
> // 可以查看用户 

>例如:gopher:X:13:30:gopher:/var/gopher/:/sbin/nologin  
>解释:用户名:密码:用户id:用户所在组id:备注:用户家目录:shell命令所在目录。

>如果想改变uid号和组id号则：  
usermod -u （新id号） -g （对应组的id号） -c （注释信息） -d （后面加目录） -s（修改的用户的shell） （用户名称  ）

#<font color=“greem”>usermod(参数)</font> 
## 参数: 
-u 

>//设置用户ID（UID），用户ID和账号一样必须是唯一的。

-g         
>//指定用户所属的主（私有）组（组必须存在），参数可以是组名称或组ID(GID)。

-d        
>//建立用户目录，参数即所建的用户目录（通常与用户账号相同）。

-s       
>//设置用户环境，即设置用户的shell环境。

-e      
>//设置用户账号的使用期限。

-G     
>//用户组，指定用户所属的附加组。 

-c  
>//修改注释信息 


#<font color=“greem”>usermod -l （你要改的用户名） （原来的用户名）</font>    
>//修改用户名

#<font color=“greem”>usermod （要删除的用户名）</font>  
>//删除用户名      
# 密码文件 
#<font color=“greem”>tail /etc/shadow</font>       
>//查看密码文件。

#<font color=“greem”>passwd （用户名）</font> 

>//设置密码。

#<font color=“greem”>tail /etc/shadow</font>
>/查看组密码信息

>例如:user1:!!:17464:0:99999:7:::  
>>含义:用户名：密码（无法破解）：最后一次修改时间：密码还有多少天不能更改：密码到期时间：密码到期前的期限：密码失效期限：账号生命周期：保留字/etc/passwd（用户信息）

# 组的应用和修改 
#<font color=“greem”>userdel -r (用户名）</font>     
>//删除用户和目录。

#<font color=“greem”>groupadd （组名称）</font>      
>//创建一个用户组 

#<font color=“greem”>tail /etc/group</font>
>//查看用户组文件

>例如:ip:X:7:deamon:ip  
>解释:用户组:用户组口令:UID和该用户组包含的用户  

#<font color=“greem”> usermod -g （要修改的组）（用户名称）</font>   
>//修改用户的组 

#<font color=“greem”>usermod -d  （主目录）（用户名）</font>       
>//修改用户的主目录为.....

#<font color=“greem”>passwd -l （用户名）</font>          
>//锁定用户  

#<font color=“greem”>passwd -u （用户名）</font>          
>//解锁用户  

#<font color=“greem”>gpasswd -d （用户名） （组名）</font>  
>//从组中删除用户 

#<font color=“greem”>groupdel （组名）</font>               
>//删除组  

#<font color=“greem”>gpasswd （组名称）</font>              
>//给组设置密码  

#<font color=“greem”>gpasswd -d （用户名） （组名</font>）    
>//从组中删除用户 

#<font color=“greem”>gpasswd -a  （用户名）</font>            
>//为组增加用户

 
# id的应用     
#<font color=“greem”>id (用户名) </font> 
>//查看用户id信息

#<font color=“greem”>id-g （用户名）</font>    
>//显示用户所属群组的ID 

#<font color=“greem”>id-G （用户名）</font>    
>//显示用户所属附加群组的ID

#<font color=“greem”>id-u （用户名）</font>   
>//显示用户ID     













