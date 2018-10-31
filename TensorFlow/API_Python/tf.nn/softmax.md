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
  - dim:弃用的axis的别名。

### return:
    一个类型和形状如logits的Tensor。

<a href="https://www.zhihu.com/question/23765351">知乎的详解</a>
