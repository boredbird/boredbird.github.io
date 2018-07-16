---
title: python __getattr__ 和 __setattr__
date: 2018-07-16 15:53:12
categories: "Python"
tags:
     - Python
description: python __getattr__ 和 __setattr__
---

### `__getattr__方法`
拦截点号运算。当对未定义的属性名称和实例进行点号运算时，就会用属性名作为字符串调用这个方法。如果继承树可以找到该属性，则不调用此方法。
```python
class empty:
    def__getattr__(self, attrname):
        ifattrname =="age":
            return40
        else:
            raiseAttributeError, attrname

x =empty()
print(x.age)       #40
print(x.name)      #error text omitted.....AttributeError, name
```
这里empty类和实例x并没有属性age，所以执行x.age时，就会调用__getattr__方法，对于name也是同样。


<!--more-->

### `__setattr__方法`
```
会拦截所有属性的的赋值语句。如果定义了这个方法，self.arrt = value 就会变
成self,__setattr__("attr", value).这个需要注意。当在__setattr__方法内对属性进行赋值是，
不可使用self.attr = value,因为他会再次调用self,__setattr__("attr", value),则会形成无穷递归循
环，最后导致堆栈溢出异常。应该通过对属性字典做索引运算来赋值任何实例属性，也就是使
用self.__dict__['name'] = value.
```

#### 实现属性的私有化
```python
class PrivateExc(Exception):
    pass

class Privacy:
    def__setattr__(self, attrname, value):
        ifattrname inself.privates:
            raisePrivateExc(attrname, self)
        else:
            self.__dict__[attrname]= value

classTest1(Privacy):
    privates= ["age"]

classTest2(Privacy):
    privates= ["name","age"]
    def__init__(self):
        self.__dict__["name"]= "sun"

x =Test1()
y =Test2()
x.name = "Tom"         #执行成功
x.age =20              #执行失败，产生异常，该属性在privates列表内
y.name = "Mike"        #执行失败，产生异常，该属性在privates列表内
y.age =20              #执行成功
```
