# matmul

```Python
tf.matmul(
    a,
    b,
    transpose_a=False,
    transpose_b=False,
    adjoint_a=False,
    adjoint_b=False,
    a_is_sparse=False,
    b_is_sparse=False,
    name=None
)
```

将矩阵a乘以矩阵b，产生a * b。

输入必须在任何转换之后是 rank> = 2 的张量，其中内部 2 维度指定有效的矩阵乘法参数，并且任何其他外部维度匹配。 