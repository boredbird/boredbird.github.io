---
title: TensorFlow图变量tf.Variable的用法解析
date: 2018-07-16 14:28:12
categories: "深度学习"
tags:
     - Tensorflow
description: TensorFlow图变量tf.Variable的用法解析
toc: true
---

## 图变量的初始化方法
对于一般的Python代码，变量的初始化就是变量的定义，向下面这样：
```python
In [1]: x = 3
In [2]: y = 3 * 5
In [3]: y
Out[3]: 15
```
如果我们模仿上面的写法来进行TensorFlow编程，就会出现下面的”怪现象”：
```python
In [1]: import tensorflow as tf
In [2]: x = tf.Variable(3, name='x')
In [3]: y = x * 5
In [4]: print(y)
Tensor("mul:0", shape=(), dtype=int32)
```

<!--more-->

y的值并不是我们预想中的15，而是一个莫名其妙的输出。
```python
In [1]: import tensorflow as tf
In [2]: x = tf.Variable(3, name='x')
In [3]: y = x * 5
In [4]: sess = tf.InteractiveSession()
In [5]: sess.run(tf.global_variables_initializer())
In [6]: sess.run(y)
Out[6]: 15
```
在TensorFlow的世界里，变量的定义和初始化是分开的，所有关于图变量的赋值和计算都要通过tf.Session的run来进行。想要将所有图变量进行集体初始化时应该使用tf.global_variables_initializer。

## 两种定义图变量的方法
### tf.Variable
tf.Variable.init(initial_value, trainable=True, collections=None, validate_shape=True, name=None)

参数名称| 参数类型| 含义
----|---------|---------
initial_value	|所有可以转换为Tensor的类型	|变量的初始值
trainable	|bool	|如果为True，会把它加入到GraphKeys.TRAINABLE_VARIABLES，才能对它使用Optimizer
collections	|list	|指定该图变量的类型、默认为[GraphKeys.GLOBAL_VARIABLES]
validate_shape	|bool	|如果为False，则不进行类型和维度检查
name	|string	|变量的名称，如果没有指定则系统会自动分配一个唯一的值

虽然有一堆参数，但只有第一个参数initial_value是必需的，用法如下（assign函数用于给图变量赋值）：
```python
In [1]: import tensorflow as tf
In [2]: v = tf.Variable(3, name='v')
In [3]: v2 = v.assign(5)
In [4]: sess = tf.InteractiveSession()
In [5]: sess.run(v.initializer)
In [6]: sess.run(v)
Out[6]: 3
In [7]: sess.run(v2)
Out[7]: 5
```

### Args:
* `initial_value`: A Tensor, or Python object convertible to a Tensor, which is the initial value for the Variable. The initial value must have a shape specified unless validate_shape is set to False. Can also be a callable with no argument that returns the initial value when called. In that case, dtype must be specified. (Note that initializer functions from init_ops.py must first be bound to a shape before being used here.)
* `trainable`: If True, the default, also adds the variable to the graph collection GraphKeys.TRAINABLE_VARIABLES. This collection is used as the default list of variables to use by the Optimizer classes.
* `collections`: List of graph collections keys. The new variable is added to these collections. Defaults to [GraphKeys.GLOBAL_VARIABLES].
* `validate_shape`: If False, allows the variable to be initialized with a value of unknown shape. If True, the default, the shape of initial_value must be known.
* `caching_device`: Optional device string describing where the Variable should be cached for reading. Defaults to the Variable's device. If not None, caches on another device. Typical use is to cache on the device where the Ops using the Variable reside, to deduplicate copying through Switch and other conditional statements.
* `name`: Optional name for the variable. Defaults to 'Variable' and gets uniquified automatically.
variable_def: VariableDef protocol buffer. If not None, recreates the Variable object with its contents, referencing the variable's nodes in the graph, which must already exist. The graph is not changed. variable_def and the other arguments are mutually exclusive.
* `dtype`: If set, initial_value will be converted to the given type. If None, either the datatype will be kept (if initial_value is a Tensor), or convert_to_tensor will decide.
* `expected_shape`: A TensorShape. If set, initial_value is expected to have this shape.
import_scope: Optional string. Name scope to add to the Variable. Only used when initializing from protocol buffer.
* `constraint`: An optional projection function to be applied to the variable after being updated by an Optimizer (e.g. used to implement norm constraints or value constraints for layer weights). The function must take as input the unprojected Tensor representing the value of the variable and return the Tensor for the projected value (which must have the same shape). Constraints are not safe to use when doing asynchronous distributed training.

### tf.get_variable
tf.get_variable跟tf.Variable都可以用来定义图变量，但是前者的必需参数（即第一个参数）并不是图变量的初始值，而是图变量的名称。

tf.Variable的用法要更丰富一点，当指定名称的图变量已经存在时表示获取它，当指定名称的图变量不存在时表示定义它，用法如下：
```python
In [1]: import tensorflow as tf
In [2]: init = tf.constant_initializer([5])
In [3]: x = tf.get_variable('x', shape=[1], initializer=init)
In [4]: sess = tf.InteractiveSession()
In [5]: sess.run(x.initializer)
In [6]: sess.run(x)
Out[6]: array([ 5.], dtype=float32)
```

```
tf.get_variable(
    name,
    shape=None,
    dtype=None,
    initializer=None,
    regularizer=None,
    trainable=True,
    collections=None,
    caching_device=None,
    partitioner=None,
    validate_shape=True,
    use_resource=None,
    custom_getter=None,
    constraint=None
)
```

## scope如何划分命名空间
一个深度学习模型的参数变量往往是成千上万的，不加上命名空间加以分组整理，将会成为可怕的灾难。TensorFlow的命名空间分为两种，tf.variable_scope和tf.name_scope。

下面示范使用tf.variable_scope把图变量划分为4组：
```python
for i in range(4):
    with tf.variable_scope('scope-{}'.format(i)):
        for j in range(25):
             v = tf.Variable(1, name=str(j))
```
可视化输出的结果如下：
![tf.variable_scope](assets/tf.variable_scope.jpg)

下面让我们来分析tf.variable_scope和tf.name_scope的区别：
### tf.variable_scope
当使用tf.get_variable定义变量时，如果出现同名的情况将会引起报错
```python
In [1]: import tensorflow as tf
In [2]: with tf.variable_scope('scope'):
   ...:     v1 = tf.get_variable('var', [1])
   ...:     v2 = tf.get_variable('var', [1])
ValueError: Variable scope/var already exists, disallowed. Did you mean to set reuse=True in VarScope? Originally defined at:
```

而对于tf.Variable来说，却可以定义“同名”变量
```python
In [1]: import tensorflow as tf
In [2]: with tf.variable_scope('scope'):
   ...:     v1 = tf.Variable(1, name='var')
   ...:     v2 = tf.Variable(2, name='var')
   ...:
In [3]: v1.name, v2.name
Out[3]: ('scope/var:0', 'scope/var_1:0')
```
但是把这些图变量的name属性打印出来，就可以发现它们的名称并不是一样的。

如果想使用tf.get_variable来定义另一个同名图变量，可以考虑加入新一层scope，比如：
```python
In [1]: import tensorflow as tf
In [2]: with tf.variable_scope('scope1'):
   ...:     v1 = tf.get_variable('var', shape=[1])
   ...:     with tf.variable_scope('scope2'):
   ...:         v2 = tf.get_variable('var', shape=[1])
   ...:
In [3]: v1.name, v2.name
Out[3]: ('scope1/var:0', 'scope1/scope2/var:0')
```
### tf.name_scope
当tf.get_variable遇上tf.name_scope，它定义的变量的最终完整名称将不受这个tf.name_scope的影响，如下：
```python
In [1]: import tensorflow as tf
In [2]: with tf.variable_scope('v_scope'):
   ...:     with tf.name_scope('n_scope'):
   ...:         x = tf.Variable([1], name='x')
   ...:         y = tf.get_variable('x', shape=[1], dtype=tf.int32)
   ...:         z = x + y
   ...:
In [3]: x.name, y.name, z.name
Out[3]: ('v_scope/n_scope/x:0', 'v_scope/x:0', 'v_scope/n_scope/add:0')
```

## 图变量的复用
想象一下，如果我们正在定义一个循环神经网络RNN，想复用上一层的参数以提高模型最终的表现效果，应该怎么做呢？

### 做法一：
```python
In [1]: import tensorflow as tf
In [2]: with tf.variable_scope('scope'):
   ...:     v1 = tf.get_variable('var', [1])
   ...:     tf.get_variable_scope().reuse_variables()
   ...:     v2 = tf.get_variable('var', [1])
   ...:
In [3]: v1.name, v2.name
Out[3]: ('scope/var:0', 'scope/var:0')
```

### 做法二：
```python
In [1]: import tensorflow as tf
In [2]: with tf.variable_scope('scope'):
   ...:     v1 = tf.get_variable('x', [1])
   ...:
In [3]: with tf.variable_scope('scope', reuse=True):
   ...:     v2 = tf.get_variable('x', [1])
   ...:
In [4]: v1.name, v2.name
Out[4]: ('scope/x:0', 'scope/x:0')
```

## 图变量的种类
TensorFlow的图变量分为两类：local_variables和global_variables。

如果我们想定义一个不需要长期保存的临时图变量，可以向下面这样定义它：
```python
with tf.name_scope("increment"):
    zero64 = tf.constant(0, dtype=tf.int64)
    current = tf.Variable(zero64, name="incr", trainable=False, collections=[ops.GraphKeys.LOCAL_VARIABLES])
```

## tf.trainable_variables方法
```python
import tensorflow as tf

v1 = tf.get_variable('v1', shape=[1])
v2 = tf.get_variable('v2', shape=[1], trainable=False)

with tf.variable_scope('scope1'):
    s1 = tf.get_variable('s1', shape=[1], initializer=tf.random_normal_initializer())
g1=tf.Graph()
g2=tf.Graph()

with g1.as_default():
    g1v1 = tf.get_variable('g1v1', shape=[1])
    g1v2 = tf.get_variable('g1v2', shape=[1], trainable=False)
    g1vs = tf.trainable_variables()
    # [<tf.Variable 'g1v1:0' shape=(1,) dtype=float32_ref>]
    print(g1vs)

with g2.as_default():
    g2v1 = tf.get_variable('g2v1', shape=[1])
    g2v2 = tf.get_variable('g2v2', shape=[1], trainable=False)
    g2vs = tf.trainable_variables()
    # [<tf.Variable 'g2v1:0' shape=(1,) dtype=float32_ref>]
    print(g2vs)

with tf.Session() as sess:
    vs = tf.trainable_variables()
    # [<tf.Variable 'v1:0' shape=(1,) dtype=float32_ref>, <tf.Variable 'scope1/s1:0' shape=(1,) dtype=float32_ref>]
    print(vs)
```
tf.trainable_variables 返回所有 当前计算图中 在获取变量时未标记 trainable=False 的变量集合

从1.4版本开始可以支持传入scope，来获取指定scope中的变量集合
