# argmax

```py
tf.argmax(
    input,
    axis=None,
    name=None,
    dimension=None,
    output_type=tf.int64
)
```

tf.argmax(vector, 1)：返回的是vector中的最大值的索引号，如果vector是一个向量，那就返回一个值，如果是一个矩阵，那就返回一个向量，这个向量的每一个维度都是相对应矩阵行的最大值元素的索引号。

```py
import tensorflow as tf
import numpy as np
 
A = [[1,3,4,5,6]]
B = [[1,3,4], [2,4,1]]
 
with tf.Session() as sess:
    print(sess.run(tf.argmax(A, 1)))
    print(sess.run(tf.argmax(B, 1)))

# 输出：
# [4]
# [2 1]
```