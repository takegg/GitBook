# equal

别名tf.equal或tf.math.equal

两个张量有很多元素，但在每个张量中有多少元素是相等的，使用tf.equal()得到一个Boolean值的矢量。

例如：

```py
import tensorflow as tf

x = [1., 2., 3.]
y = [1., 2., 3.]
z = [0., 1., 3.]

# 使用等于测试每个元素是否相等。
result1 = tf.equal(x, y)
result2 = tf.equal(y, z)

session = tf.Session()
print(session.run(result1))
print(session.run(result2))

# 输出
# [ True  True  True]
# [False False  True]
```

```py
import tensorflow as tf

x = [1., 2., 3.]
y = [1., 2., 3.]
z = [0., 1., 3.]

result1 = tf.equal(x, y)
result2 = tf.equal(y, z)

# Use reduce_all and reduce_any to test the results of equal.
result3 = tf.reduce_all(result1)
result4 = tf.reduce_all(result2)
result5 = tf.reduce_any(result1)
result6 = tf.reduce_any(result2)

session = tf.Session()
print("EQUAL     ", session.run(result1))
print("EQUAL     ", session.run(result2))
print("REDUCE ALL", session.run(result3))
print("REDUCE ALL", session.run(result4))
print("REDUCE ANY", session.run(result5))
print("REDUCE ANY", session.run(result6))

Output

EQUAL      [ True  True  True]
EQUAL      [False False  True]
REDUCE ALL True
REDUCE ALL False
REDUCE ANY True
REDUCE ANY True
```