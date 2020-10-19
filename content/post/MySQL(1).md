---
title: "MySQL入门第一篇"
date: 2020-07-19T08:54:39+08:00
draft: false
tags: [MySQL]
categories: [MySQL]
---
<!--more-->


# 学习笔记


show database；  
> //显示所有数据库，数据库的语句格式都是分号结尾 

use <数据库名>  
> //进入数据库  

show tables； 
> //查看此数据库的所有表  

create databases <库名>；
> //新建库  

create table <新表名> （字段名,数据类型,字段名,数据类型....）    
> //创建表，注意：要先进库，才能建表   

例如:
    mysql> create table xs  
        (
            学号 char(6)    not null primary key,  
            姓名 char(8)    not null,  
            专业名 char(10) null,  
            性别 tinyint(1) not null default 1,  
            出生日期 date not null,  
            总学分 tinyint(1) null，  
            备注 text null  
          );  
 解释:  
    1.char：字符类型数据  
    2.not null：表示学号不能为空值  
    3.primary key：表示学号为主键  
    4.tinyint：整形数据，长度为1字节，0-255  
    5.default：默认  
    6.null ：可以为空值  
    7.date ：日期型  
    8.text:字符串型  

drop databases <数据库名>；
> //删除库
  
desc <表名>；
> //查看表结构

alter databases <库名>
> //修改数据库

alter table <表名>
> //修改表  

例如:  
    alter table <表名> add primary key (学号，课程号)  
      //为表中添加主键为学号，课程号。  




