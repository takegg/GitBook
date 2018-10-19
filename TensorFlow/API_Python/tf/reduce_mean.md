# reduce_mean

```py
tf.reduce_mean(
    input_tensor,
    axis=None,
    keepdims=None,
    name=None,
    reduction_indices=None,
    keep_dims=None
)
```

### 函数作用： 

沿着tensor的某一维度，计算元素的平均值。由于输出tensor的维度比原tensor的低，这类操作也叫降维。


### 参数： 

reduce_mean(input_tensor,axis=None,keep_dims=False,name=None, reduction_indices=None) 
input_tensor：需要降维的tensor。 
axis：axis=none, 求全部元素的平均值；axis=0, 按列降维，求每列平均值；axis=1，按行降维，求每行平均值。 
keep_dims：若值为True，可多行输出平均值。 
name：自定义操作的名称。 
reduction_indices：axis的旧名，已停用。


### 返回： 

> 降维后的tensor


```py
import tensorflow as tf;
import numpy as np;
 
A = np.array([[1,2], [3,4]])
 
with tf.Session() as sess:
	print sess.run(tf.reduce_mean(A))
	print sess.run(tf.reduce_mean(A, axis=0))
	print sess.run(tf.reduce_mean(A, axis=1))

# 输出：
# 2 #整体的平均值
# [2 3] #按列求得平均
# [1 3] #按照行求得平均
```

如果没有axis求得就是整体的平均。