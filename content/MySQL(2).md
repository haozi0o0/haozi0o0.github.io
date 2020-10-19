---
title: "MySQL入门第二篇"
date: 2020-07-19T08:54:39+08:00
draft: false
tags: [MySQL]
categories: [MySQL]
---
<!--more-->

# 插入数据

insert into <表名> values (在表中插入的数据);   
> //在表中插入数据，方法有很多种，这里只写一种，注意，在表里插入的数据要对应你建表的格式。

例如:  
    insert into xs ('201901','张三', '计算机',1,'2000-01-02',58);  
    //此条数据对应上一篇文章的表，字符型数据添加时必须带单引号，然后两条数据之间用逗号隔开，注意，MySQL只能识别英文标点。  

delete from <表名> where <条件>;
> //删除表中记录

update <表明> set 字段名='值' where <条件>;
> //修改表中记录

select * from <表名>;
> //查询表中记录

