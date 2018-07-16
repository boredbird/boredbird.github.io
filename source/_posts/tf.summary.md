---
title: tf.summary
date: 2018-07-16 14:28:12
categories: "深度学习"
tags:
     - Tensorflow
description: tf.summary
toc: true
---

TensorBoard可以将训练过程中的各种绘制数据展示出来，包括标量（scalars），图片（images），音频（Audio）,计算图（graph）,数据分布，直方图（histograms）和嵌入式向量。

使用TensorBoard展示数据，需要在执行Tensorflow就算图的过程中，将各种类型的数据汇总并记录到日志文件中。然后使用TensorBoard读取这些日志文件，解析数据并生产数据可视化的Web页面，让我们可以在浏览器中观察各种汇总数据。

summary_op包括了summary.scalar、summary.histogram、summary.image等操作，这些操作输出的是各种summary protobuf，最后通过summary.writer写入到event文件中。
Tensorflow API中包含系列生成summary数据的API接口，这些函数将汇总信息存放在protobuf中，以字符串形式表达。


<!--more-->

### tf.summary.FileWriter
将汇总的protobuf写入到event文件中去的相关的类： SummaryWriter是一个类，它可以调用以下成员函数来往event文件中添加相关的数据 addsummary(), add sessionlog(), add_event(), or add_graph()
```
Writes `Summary` protocol buffers to event files.

The `FileWriter` class provides a mechanism to create an event file in a
given directory and add summaries and events to it. The class updates the
file contents asynchronously. This allows a training program to call methods
to add data to the file directly from the training loop, without slowing down
training.
```

```python
...create a graph...
# Launch the graph in a session.
sess = tf.Session()
# Create a summary writer, add the 'graph' to the event file.
writer = tf.summary.FileWriter(<some-directory>, sess.graph)
```
#### example
ummary_waiter = tf.summary.FileWriter("log",tf.get_default_graph())

log是事件文件所在的目录，这里是工程目录下的log目录。第二个参数是事件文件要记录的图，也就是tensorflow默认的图。

### tf.summary.scalar
对标量数据汇总和记录使用tf.summary.scalar，函数格式如下：
`tf.summary.scalar(tags, values, collections=None, name=None)`
```
Outputs a `Summary` protocol buffer containing a single scalar value.

The generated Summary has a Tensor.proto containing the input Tensor.

Args:
  name: A name for the generated node. Will also serve as the series name in
    TensorBoard.
  tensor: A real numeric Tensor containing a single value.
  collections: Optional list of graph collections keys. The new summary op is
    added to these collections. Defaults to `[GraphKeys.SUMMARIES]`.
  family: Optional; if provided, used as the prefix of the summary tag name,
    which controls the tab name used for display on Tensorboard.

Returns:
  A scalar `Tensor` of type `string`. Which contains a `Summary` protobuf.

Raises:
  ValueError: If tensor has the wrong shape or type.
```
一般在画loss,accuary时会用到这个函数。

### tf.summary.histogram
使用tf.summary.histogram直接记录变量var的直方图，输出带直方图的汇总的protobuf，函数格式如下：`tf.summary.histogram(tag, values, collections=None, name=None)`
```
Outputs a `Summary` protocol buffer with a histogram.

Adding a histogram summary makes it possible to visualize your data's
distribution in TensorBoard. You can see a detailed explanation of the
TensorBoard histogram dashboard
[here](https://www.tensorflow.org/get_started/tensorboard_histograms).

The generated
[`Summary`](https://www.tensorflow.org/code/tensorflow/core/framework/summary.proto)
has one summary value containing a histogram for `values`.

This op reports an `InvalidArgument` error if any value is not finite.

Args:
  name: A name for the generated node. Will also serve as a series name in
    TensorBoard.
  values: A real numeric `Tensor`. Any shape. Values to use to
    build the histogram.
  collections: Optional list of graph collections keys. The new summary op is
    added to these collections. Defaults to `[GraphKeys.SUMMARIES]`.
  family: Optional; if provided, used as the prefix of the summary tag name,
    which controls the tab name used for display on Tensorboard.

Returns:
  A scalar `Tensor` of type `string`. The serialized `Summary` protocol
  buffer.
```

### tf.summary.merge
将上面几种类型的汇总再进行一次合并，具体合并哪些由inputs指定，格式如下：
`tf.summary.merge(inputs, collections=None, name=None)`

### tf.summaries.merge_all
合并默认图形中的所有汇总：`tf.summaries.merge_all(key='summaries')  `


### add_summary
```
Adds a `Summary` protocol buffer to the event file.

This method wraps the provided summary in an `Event` protocol buffer
and adds it to the event file.

You can pass the result of evaluating any summary op, using
@{tf.Session.run} or
@{tf.Tensor.eval}, to this
function. Alternatively, you can pass a `tf.Summary` protocol
buffer that you populate with your own data. The latter is
commonly done to report evaluation results in event files.

Args:
  summary: A `Summary` protocol buffer, optionally serialized as a string.
  global_step: Number. Optional global step value to record with the
    summary.
```

### 一个完整的例子
```python
from __future__ import print_function
import tensorflow as tf
import numpy as np


def add_layer(inputs, in_size, out_size, n_layer, activation_function=None):
    # add one more layer and return the output of this layer
    layer_name = 'layer%s' % n_layer
    with tf.name_scope(layer_name):
        with tf.name_scope('weights'):
            Weights = tf.Variable(tf.random_normal([in_size, out_size]), name='W')
            tf.summary.histogram(layer_name + '/weights', Weights)
        with tf.name_scope('biases'):
            biases = tf.Variable(tf.zeros([1, out_size]) + 0.1, name='b')
            tf.summary.histogram(layer_name + '/biases', biases)
        with tf.name_scope('Wx_plus_b'):
            Wx_plus_b = tf.add(tf.matmul(inputs, Weights), biases)
        if activation_function is None:
            outputs = Wx_plus_b
        else:
            outputs = activation_function(Wx_plus_b, )
        tf.summary.histogram(layer_name + '/outputs', outputs)
    return outputs


# Make up some real data
x_data = np.linspace(-1, 1, 300)[:, np.newaxis]
noise = np.random.normal(0, 0.05, x_data.shape)
y_data = np.square(x_data) - 0.5 + noise

# define placeholder for inputs to network
with tf.name_scope('inputs'):
    xs = tf.placeholder(tf.float32, [None, 1], name='x_input')
    ys = tf.placeholder(tf.float32, [None, 1], name='y_input')

# add hidden layer
l1 = add_layer(xs, 1, 10, n_layer=1, activation_function=tf.nn.relu)
# add output layer
prediction = add_layer(l1, 10, 1, n_layer=2, activation_function=None)

# the error between prediciton and real data
with tf.name_scope('loss'):
    loss = tf.reduce_mean(tf.reduce_sum(tf.square(ys - prediction),
                                        reduction_indices=[1]))
    tf.summary.scalar('loss', loss)

with tf.name_scope('train'):
    train_step = tf.train.GradientDescentOptimizer(0.1).minimize(loss)

sess = tf.Session()
merged = tf.summary.merge_all()

writer = tf.summary.FileWriter("logs/", sess.graph)

init = tf.global_variables_initializer()
sess.run(init)

for i in range(1000):
    sess.run(train_step, feed_dict={xs: x_data, ys: y_data})
    if i % 50 == 0:
        result = sess.run(merged,
                          feed_dict={xs: x_data, ys: y_data})
        writer.add_summary(result, i)
```

#### tf_graph
![tf_graph](assets/tf_graph.png)
#### tf_loss
![tf_loss](assets/tf_loss.png)
#### tf_distributions
![tf_distributions](assets/tf_distributions.png)
#### tf_histograms
![tf_histograms](assets/tf_histograms.png)
