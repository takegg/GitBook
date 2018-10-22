# Session

## 1. run

```py
run(
    fetches,
    feed_dict=None,
    options=None,
    run_metadata=None
)
```

运行操作并评估提fetches中的张量。

此方法运行TensorFlow计算的一个“step”，通过运行必要的图形片段来执行每个操作并评估fetches中的每个Tensor，将feed_dict中的值替换为相应的输入值。

### 参数

- fetches: 单个图元素，图元素列表或字典，其值是图元素或图元素列表（如上所述）。
- feed_dict: 将图元素映射到值的字典（如上所述）。
- options: 一个[RunOptions]协议缓冲区
- run_metadata: 一个[RunMetadata]协议缓冲区