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