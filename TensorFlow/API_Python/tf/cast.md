# cast

```py
tf.cast(
    x,
    dtype,
    name=None
)
```
将x的数据格式转化成dtype.例如，原来x的数据格式是bool， 
那么将其转化成float以后，就能够将其转化成0和1的序列。反之也可以

```py
a = tf.Variable([1,0,0,1,1])
b = tf.cast(a,dtype=tf.bool)
sess = tf.Session()
sess.run(tf.initialize_all_variables())
print(sess.run(b))
#[ True False False  True  True]
```