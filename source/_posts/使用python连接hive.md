---
title: 使用python连接hive
date: 2017-09-19 21:10:12 
categories: "Python" 
tags: 
     - Python
     - Hive
description: 使用python连接hive
---

Python连接hive的包有很多，我没有一一尝试，只是演示了工作当中用到的方法。
本文主要采用[PyHive](https://github.com/dropbox/PyHive)来进行对hive的增删改查。
PyHive is a collection of Python DB-API and SQLAlchemy interfaces for Presto and Hive.

## Requirements
### install using

```
pip install SQLALchemy
```

```
pip install pyhive[presto]
```

```
pip install pyhive[hive]
```

## Presto engine
### Create engine

``` engine = create_engine('presto://url:port/hive/schema')
```
### Presto Select
```df = pd.read_sql(sql=(r'select * from '+ 'schema.tablename') , con=engine)
```
### Presto Insert
```df.to_sql(tablename, con=engine, flavor=None, if_exists='append', index=False, chunksize=2000000)
```
### Presto Update
Hive does not support update.
### Presto Delete
```
engine.execute("drop table schema.tablename")
```

## Hive engine

### Create engine

``` engine = create_engine('hive://url:port/hive/schema')
```
### Hive Select
```df = pd.read_sql(sql=(r'select * from '+ 'schema.tablename') , con=engine)
```
### Hive Insert
```df.to_sql(tablename, con=engine, flavor=None, if_exists='append', index=False, chunksize=2000000)
```
### Hive Update
Hive does not support update.
### Hive Delete
```
engine.execute("drop table schema.tablename")
```
