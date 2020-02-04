# usual-command

## 文件及文件夹个数

1. 统计当前文件夹下文件的个数，包括子文件夹里的
  ```bash
  ls -lR|grep "^-"|wc -l
  ```
2. 统计文件夹下目录的个数，包括子文件夹里的
  ```bash
  ls -lR|grep "^d"|wc -l
  ```
3. 统计当前文件夹下文件的个数
  ```bash
  ls -l |grep "^-"|wc -l
  ```
4. 统计当前文件夹下目录的个数
  ```bash
  ls -l |grep "^d"|wc -l
  ```
2. 统计文件夹下目录的个数，包括子文件夹里的
  ```bash
  ls -lR|grep "^d"|wc -l
  ```
2. 统计文件夹下包含某string的文件个数
  ```bash
  ls -l | grep string | wc -l
  ```

## shell快捷键
1. ctrl+c 杀死进程
2. ctrl+z 暂停进程

## 批量重命名
```shell
sudo apt install rename
sudo rename -v 's/.webm/.mp4/' *.webm
```
  >https://www.linuxidc.com/Linux/2016-11/137041.htm

## du命令

```
//查看系统中文件的使用情况
df -h
//查看当前目录下各个文件及目录占用空间大小
du -sh *

//方法一：切换到要删除的目录，删除目录下的所有文件
rm -f *

//方法二：删除logs文件夹下的所有文件，而不删除文件夹本身
rm -rf log/*
```
> <a href="https://blog.csdn.net/justdoithai/article/details/70216480">更多</a>

## 命令安装位置
```sh
which '命令'
#或
ls -al
```

## vi 
```
清空文档
鼠标至首行然后:.,$d
```