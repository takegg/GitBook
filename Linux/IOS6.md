# IOS

### 安装pip

1. 安装GCC

```shell
#1、下载源码
$ wget ftp://ftp.gnu.org/gnu/gcc/gcc-8.2.0/gcc-8.2.0.tar.gz

$ tar zxf gcc-8.2.0.tar.gz

$ cd gcc-8.2.0

$ ./contrib/download_prerequisites

#2、编译安装
$ mkdir gcc-build-8.2.0
$ cd gcc-build-8.2.0
$ ../configure --prefix=/usr
$ make && make install

#3、查看版本号
$ gcc --version
$ g++ --version
$ which gcc
$ which g++
```