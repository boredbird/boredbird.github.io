---
title: python：argparse包基本使用
date: 2018-07-16 15:55:12
categories: "Python"
tags:
     - Python
     - argparse
description: python：argparse包基本使用
---

### step 1、导入argparse模块
import argparse

### step 2、创建解析器对象ArgumentParser，可以添加参数。
description：描述程序
parser=argparse.ArgumentParser(description="This is a example program ")
add_help：默认是True，可以设置False禁用

### step 3、add_argument()方法，用来指定程序需要接受的命令参数
#### 定位参数：
parser.add_argument("echo",help="echo the string")
#### 可选参数：
parser.add_argument("--verbosity", help="increase output verbosity")
在执行程序的时候，定位参数必选，可选参数可选。


<!--more-->

add_argument()常用的参数：
* dest：如果提供dest，例如dest="a"，那么可以通过args.a访问该参数
* default：设置参数的默认值
* action：参数触发的动作
* store：保存参数，默认
* store_const：保存一个被定义为参数规格一部分的值（常量），而不是一个来自参数解析而来的值。
* store_ture/store_false：保存相应的布尔值
* append：将值保存在一个列表中。
* append_const：将一个定义在参数规格中的值（常量）保存在一个列表中。
* count：参数出现的次数
* parser.add_argument("-v", "--verbosity", action="count", default=0, help="increase output verbosity")
* version：打印程序版本信息
* type：把从命令行输入的结果转成设置的类型
* choice：允许的参数值
* parser.add_argument("-v", "--verbosity", type=int, choices=[0, 1, 2], help="increase output verbosity")
* help：参数命令的介绍
* example: argparse_example.py

#### example: argparse_example.py
```python
import argparse

parser = argparse.ArgumentParser()
parser.add_argument("--echo", type=str，help="echo the string you use here")
parser.add_argument("--square", type=int, help="display a square of a given number")
args = parser.parse_args()
print(args.echo)
print(args.square**2)
```
这里第一个参数调用了系统的echo工具，将函数名称后的字符串打印在控制台显示。第二个参数做了平方运算。运行：
`python argparse_example.py --echo ‘hello!’ --square 4`
返回
```
hello!
16
```
