# placeholder

```Python
tf.placeholder(
    dtype,
    shape=None,
    name=None
)
```

为总是被提供的张量插入占位符。

重要提示：如果进行评估，此张量将产生错误。必须使用session.run（）的feed_dict可选参数来提供其值，Tensor.eval（）或Operation.run（）。

例如：

```
x = tf.placeholder(tf.float32, shape=(1024, 1024))
y = tf.matmul(x, x)

with tf.Session() as sess:
  print(sess.run(y))  # ERROR: will fail because x was not fed.

  rand_array = np.random.rand(1024, 1024)
  print(sess.run(y, feed_dict={x: rand_array}))  # Will succeed.
```

### 参数

- dtype：要提供的张量中的元素类型。
- shape：要提供的张量的形状（可选）。如果未指定形状，你可以提供任何形状的张量。
- name：操作的名称（可选）。

### Returns:

一个Tensor，可以用作提供值的句柄，但不能直接评估。

### 增加：

- RuntimeError：如果启用了紧急(eager)执行.

### Eager 兼容性

Placeholders 和 eager execution不兼容