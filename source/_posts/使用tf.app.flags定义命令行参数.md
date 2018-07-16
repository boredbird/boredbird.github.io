---
title: 使用tf.app.flags定义命令行参数
date: 2018-07-16 14:28:12
categories: "深度学习"
tags:
     - Tensorflow
description: 使用tf.app.flags定义命令行参数
toc: true
---

tf定义了tf.app.flags，用于支持接受命令行传递参数，相当于接受argv。

新建test_tf_flags.py文件内容如下：
```python
import tensorflow as tf

#第一个是参数名称，第二个参数是默认值，第三个是参数描述
tf.app.flags.DEFINE_string('str_name', 'def_v_1',"descrip1")
tf.app.flags.DEFINE_integer('int_name', 10,"descript2")
tf.app.flags.DEFINE_boolean('bool_name', False, "descript3")

FLAGS = tf.app.flags.FLAGS

#必须带参数，否则：'TypeError: main() takes no arguments (1 given)';   main的参数名随意定义，无要求
def main(_):
    print(FLAGS.str_name)
    print(FLAGS.int_name)
    print(FLAGS.bool_name)

if __name__ == '__main__':
    tf.app.run()  #执行main函数
```

<!--more-->


执行：
```
(python3) E:\Code\NN_NER_tensorFlow-master>python test_tf_flags.py
def_v_1
10
False

(python3) E:\Code\NN_NER_tensorFlow-master>python test_tf_flags.py  --str_name test_str --int_name 99 --bool_name True
test_str
99
True
```
