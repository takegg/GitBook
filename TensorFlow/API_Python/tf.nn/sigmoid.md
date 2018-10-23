# sigmoid

### 别名
- tf.nn.sigmoid
- tf.sigmoid

```py
tf.nn.sigmoid(
    x,
    name=None
)
```
其公式：y = 1/(1 + exp (-x))

### 参数:
- x: float16, float32, float64, complex64, or complex128类型的tensor
- name: 操作名称(可选)

### 返回：
一个类似x类型的tensor

### 实例：

```
import tensorflow as tf

a = tf.constant([[1.0, 2.0], [3.0, 4.0], [5.0, 6.0]])
sess = tf.Session()
print(sess.run(tf.sigmoid(a)))
```
**返回**
> [[0.7310586  0.880797  ]
> 
> [0.95257413 0.98201376]
> 
> [0.9933072  0.9975274 ]]