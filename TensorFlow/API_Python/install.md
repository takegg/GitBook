# install

##  通过coda安装
1. 安装anacoda(**以下安装均通过anacoda安装，不要通过其他管理器**)
2. 创建虚拟环境env
3. 切换到env
4. 按装jupyterNotebook，并测试，如不成功则参考base中的默认安装包。
5. 安装TensorFlow
6. 安装matplotlib
7. vscode切换编译器按F1，切换到env
8. 安装pandas
9. 安装scikit-learn
10. 启动tensorboard
```shell
tensorboard --logdir mylogdir
# 或
tensorboard --db sqlit.tensorboard.db
# 或 
# tensorboard --helpfull 
```