# install

##  通过coda安装
1. 安装anacoda(**以下安装均通过anacoda安装，不要通过其他管理器**)
2. 创建虚拟环境env
3. 切换到env
4. 按装jupyterNotebook，并测试，如不成功则参考base中的默认安装包。
5. 安装TensorFlow
    ```shell
    # 引入模块错误
    ImportError: No module named 'tensorflow'
    # 错误解决
    pip install --upgrade -I setuptools
    # https://www.tensorflow.org/install/pip 查看Tensorflow的版本
    pip install --ignore-installed --upgrade https://storage.googleapis.com/tensorflow/mac/cpu/tensorflow-1.12.0-py3-none-any.whl
    ```
6. 安装matplotlib
7. 安装pandas
8. 安装scikit-learn
9. 安装seaborn
10. 启动tensorboard
11.  vscode切换编译器按F1，切换到env
```shell
tensorboard --logdir mylogdir
# 或
tensorboard --db sqlit.tensorboard.db
# 或 
# tensorboard --helpfull 
```
