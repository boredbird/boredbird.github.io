---
title: hive和presto语句对比
date: 2018-07-16 14:53:12
categories: "Python"
tags:
     - presto
     - hive
description: hive和presto语句对比
---

### presto常用语句
语句|说明
-------------|---------------------------
show catalogs|显示catalog
show session|查看当前session的主要属性
show tables like 'app_idata%'|查看有哪些表


hive|presto|说明
----|------|---
select my_array1|select my_arrayCARDINALITY(my_array)|SQL中的下标运算符支持完整的表达式与Hive
数组从0开始|数组从1开始|count(distinct a,b)
show partitions orders|SHOW PARTITIONS FROM orders|查看分区
 |show partitions from app_idata_bdl_all_order_app_log <br/>where dt>='2016-10-01' and biz_type='rec'</br>order by dt desc;|根据限制条件查看分区
SHOW SCHEMAS [ FROM catalog ]|SHOW TABLES [ FROM schema ] [ LIKE pattern ]|
count(distinct order_id,sku_id)|count(distinct concat(order_id,sku_id))|计算订单行
substring(str,start,len)|substr(str,start,len)	 |
a rlike('^T')|	regexp_like(a, '^T')|处理正则表达式的函数不一致,且字段所处位置也不一样https://prestodb.io/docs/0.132/functions/regexp.html
lateral view explode()|<br/>  SELECT student, score </br><br/> FROM tests </br><br/> CROSS JOIN UNNEST(scores) AS t (score);</br>|<br/>presto暂时不支持此行转列函数.</br><br/>http://yugouai.iteye.com/blog/2017528</br>
pmod(99,10)	|mod(99,10)	|取模


<!--more-->
