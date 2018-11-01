# conv2d

```py
tf.nn.conv2d(
    input,
    filter,
    strides,
    padding,
    use_cudnn_on_gpu=True,
    data_format='NHWC',
    dilations=[1, 1, 1, 1],
    name=None
)
```

## 参数：

- input： 
指需要做卷积的输入图像，它要求是一个Tensor，具有[batch, in_height, in_width, in_channels]这样的shape，具体含义是[训练时一个batch的图片数量, 图片高度, 图片宽度, 图像通道数]，注意这是一个4维的Tensor，要求类型为float32和float64其中之一

- filter： 
相当于CNN中的卷积核，它要求是一个Tensor，具有[filter_height, filter_width, in_channels, out_channels]这样的shape，具体含义是[卷积核的高度，卷积核的宽度，图像通道数，卷积核个数]，要求类型与参数input相同，有一个地方需要注意，第三维in_channels，就是参数input的第四维

- strides：卷积时在图像每一维的步长，这是一个一维的向量，长度4

- padding： 
string类型的量，只能是”SAME”,”VALID”其中之一，这个值决定了不同的卷积方式（后面会介绍）

- use_cudnn_on_gpu： 
bool类型，是否使用cudnn加速，默认为true

结果返回一个Tensor，这个输出，就是我们常说的feature map

## 简介：
在机器学习中，卷积用于检测输入的特征（如图像）。在卷积神经网络中，我们使用许多层来揭示许多特征。
## 数据：
在TensorFlow中，我们可以使用tf.nn中的conv2d方法（这指的是“神经网络”）。我们必须将输入数据转换为4D矩阵，并使用4D过滤器。

## 示例：
- Conv2d 样本：
此代码除了显示conv2d如何转换输入之外没有用。卷积层的目标是在图像中揭示（或强调）特征（如同书页折角以标注重点）。
- 输入：
我们使用16像素的图像（可能是一个小图标）。我们使用reshape来确保它是四维的。
- 过滤器：
对于2D卷积（通常用于图像识别），我们应用过滤器使每个卷积层不同。
- Conv2d:
我们调用tf.nn.conv2d对我们的数据运行卷积。这里使用**过滤器**和**步幅数组**来尝试检测重要特征。
```py
import tensorflow as tf

# The input data (could be an image).
temp = tf.constant([0, 1, 0, 1, 2, 1, 1, 0, 3, 1, 1, 0, 4, 4, 5, 4], tf.float32)
temp2 = tf.reshape(temp, [2, 2, 2, 2])

# A filter (affects the convolution).
filter = tf.constant([1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], tf.float32)
filter2 = tf.reshape(filter, [2, 2, 2, 2])

# Use convolution layer on 4D matrices.
convolution = tf.nn.conv2d(temp2, filter2, [1, 1, 1, 1], padding="SAME")

# Initialize session.
session = tf.Session()
tf.global_variables_initializer()

# Evaluate all our variables.
print("INPUT")
print(session.run(temp2))
print("FILTER")
print(session.run(filter2))
print("CONVOLUTION")
print(session.run(convolution))
```
> 输出：
```py
INPUT # 对input做reshape变换
[[[[0. 1.]
   [0. 1.]]

  [[2. 1.]
   [1. 0.]]]


 [[[3. 1.]
   [1. 0.]]

  [[4. 4.]
   [5. 4.]]]]

----

FILTER # 对filter做reshape变换
[[[[1. 1.]
   [1. 1.]]

  [[0. 0.]
   [0. 0.]]]


 [[[0. 0.]
   [0. 0.]]

  [[0. 0.]
   [0. 0.]]]]

----

CONVOLUTION  #对input和fileter的reshape变换后的矩阵做conv2d
[[[[1. 1.]
   [1. 1.]]

  [[3. 3.]
   [1. 1.]]]


 [[[4. 4.]
   [1. 1.]]

  [[8. 8.]
   [9. 9.]]]]
```
### 笔记：
- 如果检查输入数据，可以看到较早的数组具有较低的值，并且它们往往会增长至结束。这个很重要。
还有，在卷积中，我们可以看到强调相同的“增加值” - 卷积中的底部4个数字更大些。 
- conv2d的“strides”参数表示经过原始数据并用于应用卷积的滑动窗口的大小。
- 重点：
  对于strides，4个元素数组中的第一个和最后一个整数必须为1。通常，您可以仅复制样本就行。

<a href="https://blog.csdn.net/mao_xiao_feng/article/details/78004522">【TensorFlow】tf.nn.conv2d是怎样实现卷积的？</a>
