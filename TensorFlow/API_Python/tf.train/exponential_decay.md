# exponential_decay

```py
tf.train.exponential_decay(
    learning_rate,
    global_step,
    decay_steps,
    decay_rate,
    staircase=False,
    name=None
)
```
### 参数：
    - learning_rate:            事先设定的初始学习率；
    - global_step:              用于衰减计算，是一个init32或init64的Tensor标量，或者一个python数字，不能为负。
    - decay_rate:               衰减系数；
    - decay_steps:              衰减速度
    - staircase:                设置不同衰减方式。默认值为False,当为True时，（global_step/decay_steps）则被转化为整数。如果True则学习速率将以离散间隔方式衰减。

### return
    每一轮优化时使用的学习率；

### 作用
    在Tensorflow中，为解决设定学习率(learning rate)问题，提供了指数衰减法来解决。

    通过tf.train.exponential_decay函数实现指数衰减学习率。

### 函数运行步骤
    1.  首先使用较大学习率(目的：为快速得到一个比较优的解);
    2.  然后通过迭代逐步减小学习率(目的：为使模型在训练后期更加稳定);


### staircase参数的示例
```py
    global_step = tf.Variable(0)  

    learning_rate = tf.train.exponential_decay(0.1, global_step, 100, 0.96, staircase=True)     #生成学习率  

    learning_step = tf.train.GradientDescentOptimizer(learning_rate).minimize(....., global_step=global_step)  #使用指数衰减学习率  
```
learning_rate：0.1；staircase=True;则每100轮训练后要乘以0.96.
通常初始学习率，衰减系数，衰减速度的设定具有主观性(即经验设置)，而损失函数下降的速度与迭代结束之后损失的大小没有必然联系，
所以神经网络的效果不能单一的通过前几轮损失函数的下降速度来比较。

### 应用示例：
```py
import tensorflow as tf;  
import numpy as np;  
import matplotlib.pyplot as plt;  
  
learning_rate = 0.1  
decay_rate = 0.96  
global_steps = 1000  
decay_steps = 100  
  
global_ = tf.Variable(tf.constant(0))  
c = tf.train.exponential_decay(learning_rate, global_, decay_steps, decay_rate, staircase=True)  
d = tf.train.exponential_decay(learning_rate, global_, decay_steps, decay_rate, staircase=False)  
  
T_C = []  
F_D = []  
  
with tf.Session() as sess:  
    for i in range(global_steps):  
        T_c = sess.run(c,feed_dict={global_: i})  
        T_C.append(T_c)  
        F_d = sess.run(d,feed_dict={global_: i})  
        F_D.append(F_d)  
  
  
plt.figure(1)  
plt.plot(range(global_steps), F_D, 'r-')  
plt.plot(range(global_steps), T_C, 'b-')  
      
plt.show()  
```
### 分析：
初始的学习速率是0.1，总的迭代次数是1000次，如果staircase=True，那就表明每decay_steps次计算学习速率变化，更新原始学习速率，如果是False，那就是每一步都更新学习速率。红色表示False，绿色表示True。