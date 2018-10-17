# set_random_seed

```TensorFlow
tf.set_random_seed(seed)
```
计算图整体级别的随机种子数

依赖随机种子的操作实际上是从两个种子派生出来的：graph-level 和 operation-level 种子。这里设置的是graph-level的种子。

它与操作级别种子的交互如下：
1. 如果既未设置图级别也未设置操作种子：随机种子用于此操作。
2. 如果设置了图级别种子，但操作种子没有：系统确定性地挑选操作种子与图级种子结合，以便它获得唯一的随机序列。
3. 如果未设置图级别种子，但设置了操作种子：默认的图级别种子和指定的操作种子用于确定随机序列。
4. 如果设置了图级别和操作种子：两个种子一起用于确定随机序列。
   
要说明用户可见的效果，请考虑以下示例：要生成跨会话的不同序列，请既不设置图级别也不设置操作级种子：

```Python
a = tf.random_uniform([1])
b = tf.random_normal([1])

print("Session 1")
with tf.Session() as sess1:
  print(sess1.run(a))  # generates 'A1'
  print(sess1.run(a))  # generates 'A2'
  print(sess1.run(b))  # generates 'B1'
  print(sess1.run(b))  # generates 'B2'

print("Session 2")
with tf.Session() as sess2:
  print(sess2.run(a))  # generates 'A3'
  print(sess2.run(a))  # generates 'A4'
  print(sess2.run(b))  # generates 'B3'
  print(sess2.run(b))  # generates 'B4'
```

要OP的跨会话生成相同的可重复序列，请为操作级设置种子：

```Python
a = tf.random_uniform([1], seed=1)
b = tf.random_normal([1])

# Repeatedly running this block with the same graph will generate the same
# sequence of values for 'a', but different sequences of values for 'b'.
print("Session 1")
with tf.Session() as sess1:
  print(sess1.run(a))  # generates 'A1'
  print(sess1.run(a))  # generates 'A2'
  print(sess1.run(b))  # generates 'B1'
  print(sess1.run(b))  # generates 'B2'

print("Session 2")
with tf.Session() as sess2:
  print(sess2.run(a))  # generates 'A1'
  print(sess2.run(a))  # generates 'A2'
  print(sess2.run(b))  # generates 'B3'
  print(sess2.run(b))  # generates 'B4'
```

使所有操作生成的随机序列在会话中可重复，请设置图级别的种子：

```Python
tf.set_random_seed(1234)
a = tf.random_uniform([1])
b = tf.random_normal([1])

# Repeatedly running this block with the same graph will generate the same
# sequences of 'a' and 'b'.
print("Session 1")
with tf.Session() as sess1:
  print(sess1.run(a))  # generates 'A1'
  print(sess1.run(a))  # generates 'A2'
  print(sess1.run(b))  # generates 'B1'
  print(sess1.run(b))  # generates 'B2'

print("Session 2")
with tf.Session() as sess2:
  print(sess2.run(a))  # generates 'A1'
  print(sess2.run(a))  # generates 'A2'
  print(sess2.run(b))  # generates 'B1'
  print(sess2.run(b))  # generates 'B2'

```

参数：
- seed：整数
