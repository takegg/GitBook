# Variable

```py 
tf.Variable（initializer， name）
```

 - initializer: 是初始化参数，可以有tf.random_normal，tf.constant，tf.constant等
 - name: 就是变量的名字

### 例如：

```py
import tensorflow as tf
import numpy as np
import matplotlib.pyplot as plt

a1 = tf.Variable(tf.random_normal(shape=[2, 3], mean=0, stddev=1), name='a1')
a2 = tf.Variable(tf.constant(1), name='a2')
a3 = tf.Variable(tf.ones(shape=[2, 3]), name='a3')
a4 = tf.Variable(tf.zero(shape=[2, 3]), name='a4')

with tf.Session() as sess:
    sess.run(tf.global_variables_initializer())
    print(sess.run(a1))
    print(sess.run(a2))
    print(sess.run(a3))
    print(sess.run(a4))
```
> 输出：
> 
> [[ 0.4663596   0.46181905  0.9918087 ]
> [ 1.0729748  -0.6219984   0.60982907]]
> 
> 1
>
>[[1. 1. 1.]
 [1. 1. 1.]]
>
>[[0. 0. 0.]
 [0. 0. 0.]]