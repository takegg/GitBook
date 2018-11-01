# softmax
```py
tf.nn.softmax(
    logits,
    axis=None,
    name=None,
    dim=None
)
```
### 参数
  - logits:非空Tensor，必须是half, float32, float64中的一种。
  - axis：softmax将执行的维度。默认-1表示最后一维。
  - name:操作名。
  - dim:已弃用，请改用axis参数。

此函数执行相当于此：
```py
softmax = tf.exp(logits) / tf.reduce_sum(tf.exp(logits), axis)
```

### return:
    一个类型和形状如logits的Tensor。

<a href="https://www.zhihu.com/question/23765351">知乎的详解</a>


## 详解

### 描述：
  卷积神经网络使用许多层来理解数据的各个部分。但是要对数据进行分类，我们必须有一个概率集合使我们做出最终论断。
### 使用
  使用softmax，我们得到一组和为1的概率。Softmax是一个众所周知的函数，可将我们的规范化为标准范围（0到1）。

### TensorFlow程序可以将每种可能性的证据（在向量中的已知位置）相加。然后softmax（）可以在这些证据计数之间做出判断。

### 示例一：
我们有一个4个数字的向量。-1是最低值，3是最高值。这些值都规范化为0到1。

### 示例二：
我们可以在tensor内的某个维度上使用softmax。我们制作一个3D矩阵（带有reshape）并定位第二个维度。

```py
import tensorflow as tf

# Use softmax on vector.
x = [0., -1., 2., 3.]
softmax_x = tf.nn.softmax(x)

# Create 2D tensor and use softmax on the second dimension.
y = [5., 4., 6., 7., 5.5, 6.5, 4.5, 4.]
y_reshape = tf.reshape(y, [2, 2, 2])
softmax_y = tf.nn.softmax(y_reshape, 1)

session = tf.Session()
print("X")
print(x)
print("SOFTMAX X")
print(session.run(softmax_x))
print("Y")
print(session.run(y_reshape))
print("SOFTMAX Y")
print(session.run(softmax_y))
```
> 输出：
```shell
X 
[0.0, -1.0, 2.0, 3.0] 
----
SOFTMAX X # softmax处理后的X值
[0.03467109 0.01275478 0.25618663 0.69638747] 
----
Y # reshape后的Y值
[[[5.  4. ]
  [6.  7. ]]
 [[5.5 6.5]
  [4.5 4. ]]]
----
SOFTMAX Y # softmax处理后的Y值
[[[0.26894143 0.04742587]
  [0.7310586  0.95257413]]
 [[0.7310586  0.9241418 ]
  [0.26894143 0.07585818]]]
```

## 备忘：
该方法用于卷积神经网络的最后阶段。Softmax “压缩”值，去除异常值。
## 提示：
数学家拥有最好的术语。我们可以用softmax“压缩”我们的数字。
## 引用：
Softmax是广义化的逻辑函数，其将任意实数值的K维向量“压缩”到范围[0,1]中的实数值的K维向量，其加起来为1。
## 回顾：
经过多个阶段后，我们的机器学习模型必须做出决定。Softmax是这里的关键。这个函数得到了我们的最终概率。