---
title: python类属性和方法的封装
date: 2017-10-14 15:00:12 
categories: "Python" 
tags: 
     - Python
description: python类属性和方法的封装
---
封装是一种限制直接访问目标属性和方法的机制，但同时它又有利于对数据（对象的方法）进行操作。

封装是一种将抽象性函数接口的实现细节部分包装、隐藏起来的方法。同时，它也是一种防止外界调用端，去访问对象内部实现细节的手段，这个手段是由编程语言本身来提供的。

对象所有的内部表征对于外部来说都是隐藏的，只有对象能直接与内部数据交互。首先，我们需要理解公开（public）和私有（non-public）实例变量和方法。

# 公开实例变量

对于 Python 的类，我们可以使用 constructor 方法初始化公开实例变量：

``` python
	class Person:
		def __init__(self,first_name):
			self.first_name = first_name
```

下面我们应用 first_name 的值作为公开实例变量的变元。

``` python
	a = Person('zhang')
	print a.first_name  # -> zhang
```

在类别内：

``` python
	class Person:
		first_name = 'zhang'
```

现在我们不需要再对 first_name 赋值，所有赋值到 a 的目标都将有类的属性：

``` python
	a = Person()
	print a.first_name # -> zhang
```

现在我们已经学会如何使用公开实例变量和类属性。除此之外，我们还能管理公开部分的变量值，即对象可以管理其变量的值：Get 和 Set 变量值。保留 Person 类，我们希望能给 first_name 变量赋另外一个值：

``` python
	a = Person('zhang')
	a.first_name = 'Z'
	print a.first_name # -> Z
```

如上我们将另外一个值赋予了 first_name 实例变量，因为它又是一个公开变量，所以会更新变量值。


# 私有实例变量

和公开实例变量一样，我们可以使用 constructor 方法或在类的内部声明而定义一个私有实例变量。语法上的不同在于私有实例变量在变量名前面加一个下划线：

``` python
	class Person:
		def __init__(self,first_name,email):
			self.first_name = first_name
			self._email = email
```

上述定义的 email 变量就是私有变量。
``` python
	a = Person('zhang','zhang@mail.com')
	print a._email # -> zhang@mail.com
```

我们可以访问并且更新它，私有变量仅是一个约定，即他们需要被视为 API 非公开的部分。所以我们可以使用方法在类的定义中完成操作，例如使用两种方法展示私有实例的值与更新实例的值：

``` python
class Person:
	def __init__(self,first_name,email):
		self.first_name = first_name
		self.__email = email
	
	def update_email(self,new_email):
		self.__email = new_email

	def email(self):
		return self.__email
```

现在我们可以使用方法更新或访问私有变量。

``` python
a = Person('zhang','zhang@mail.com')
print a.email() # -> zhang@mail.com

a.__email = 'new_email@mail.com'
print a.__email # -> new_email@mail.com
print a.email() # -> zhang@mail.com

a.update_email('update_email@mail.com')
print a.__email # -> new_email@mail.com
print a.email() # -> update_email@mail.com

```


![](/assets/python/private1.png)


从上面可见，以双下划线打头的名称会导致出现名称重整的行为。具体来说就是上面的这个类中的私有属性会被分别重命名为_C__private 和 _C__private_name。
但是为啥两个值不一样？？

![](/assets/python/private3.png)

![](/assets/python/private4.png)

![](/assets/python/private5.png)

![](/assets/python/private6.png)

豁然开朗！

``` python
a = Person('zhang','zhang@mail.com')
print a.email() # -> zhang@mail.com

a._email = 'new_email@mail.com'
print a._email # -> new_email@mail.com
print a.email() # -> new_email@mail.com

a.update_email('update_email@mail.com')
print a._email # -> update_email@mail.com
print a.email() # -> update_email@mail.com

```

![](/assets/python/private2.png)








