# softmax_cross_entropy_with_logits

```py
tf.nn.softmax_cross_entropy_with_logits(
    _sentinel=None,
    labels=None,
    logits=None,
    dim=-1,
    name=None
)
```

计算`logits`和`labels'之间的softmax交叉熵。（弃用）
TensorFlow的未来主要版本将允许梯度在默认情况下流入backprop上的标签输入。
未来使用tf.nn.softmax_cross_entropy_with_logits_v2。

测量离散分类任务中的概率误差，其中类是互斥的（每个条目恰好在一个类中）。例如，每个CIFAR-10图像都标有一个且只有一个标签：图像可以是狗或卡车，但不能同时是两者。

- _sentinel:用于预防参数定位。内部参数，不使用。
- labels:实际的标签，大小同下。
- logits:就是神经网络最后一层的输出，如果有batch的话，它的大小就是[batchsize，num_classes]，单样本的话，大小就是num_classes.
- dim:分类维度。最后一个维度默认为-1。
- name:操作的名称（可选）。

### return

包含softmax交叉熵损失的张量。它的类型与logits相同，其形状与标签相同，只是它没有标签的最后一个纬度。


### 注解

第一步是先对网络最后一层的输出做一个softmax，这一步通常是求取输出属于某一类的概率，对于单样本而言，输出就是一个num_classes大小的向量（[Y1，Y2,Y3...]其中Y1，Y2，Y3...分别代表了是属于该类的概率）

softmax的公式是：

<img src="/TENsorFlow/img/softmax_cross_entropy_with_logits.png"/>

第二步是softmax的输出向量[Y1，Y2,Y3...]和样本的实际标签做一个交叉熵，公式如下：

<img src="/TENsorFlow/img/softmax_cross_entropy_with_logits01.png"/>

其中{% math %}y'_i{% endmath %}指代实际的标签中第i个的值（用mnist数据举例，如果是3，那么标签是[0，0，0，1，0，0，0，0，0，0]，除了第4个值为1，其他全为0）

{% math %}y_i{% endmath %}就是softmax的输出向量[Y1，Y2,Y3...]中，第i个元素的值

显而易见，预测{% math %}y_i{% endmath %}越准确，结果的值越小（别忘了前面还有负号），最后求一个平均，得到我们想要的loss

### 示例：

```
import tensorflow as tf
 
#our NN's output
logits=tf.constant([[1.0,2.0,3.0],[1.0,2.0,3.0],[1.0,2.0,3.0]])
#step1:do softmax
y=tf.nn.softmax(logits)
#true label
y_=tf.constant([[0.0,0.0,1.0],[0.0,0.0,1.0],[0.0,0.0,1.0]])
#step2:do cross_entropy
cross_entropy = -tf.reduce_sum(y_*tf.log(y))
#do cross_entropy just one step
cross_entropy2=tf.reduce_sum(tf.nn.softmax_cross_entropy_with_logits(logits, y_))#dont forget tf.reduce_sum()!!
 
with tf.Session() as sess:
    softmax=sess.run(y)
    c_e = sess.run(cross_entropy)
    c_e2 = sess.run(cross_entropy2)
    print("step1:softmax result=")
    print(softmax)
    print("step2:cross_entropy result=")
    print(c_e)
    print("Function(softmax_cross_entropy_with_logits) result=")
    print(c_e2)
```
输出：
> step1:softmax result=
[[ 0.09003057  0.24472848  0.66524094]
 [ 0.09003057  0.24472848  0.66524094]
 [ 0.09003057  0.24472848  0.66524094]]
>
> step2:cross_entropy result=1.22282
> 
> Function(softmax_cross_entropy_with_logits) result=1.2228
