# ubuntu_server_install

使用fdisk -l 查看硬盘　

## 挂载exfat
```shell
$ sudo apt-get install exfat-fuse exfat-utils
$ sudo mkdir /media/exfat
$ sudo mount -t exfat /dev/sdb1 /media/exfat
$ sudo umount /dev/sdc1 # 卸载U盘
$ sudo umount -l /dev/sdb1  强制卸载 
```
每个文件夹只能挂载一个盘
- -o 指定挂载文件系统时的选项 

- ro 以只读方式挂载

- rw 以读写方式挂载

## 查看结果
df -h：查看磁盘占用情况
df -T：查看所有磁盘的文件系统类型(type)
fdisk -l：查看所有被系统识别的磁盘
mount -t type device dir：挂载device到dir

##minidlna
```shell
$ minidlnad
```
1、安装

sudo apt-get install minidlna

2、修改配置


#打开配置文件

sudo vi /etc/minidlna.conf

#可参考修改的项有：

参数名	说明
port	服务端口，默认为8200。如果有防火墙配置，需要开放。
media_dir
媒体目录可以设置多个，如：media_dir=V,/noah/videos（逗号前为类型标识：A音频，P图片，V视频）
friendly_name
服务名称，在其它设备中看到的名称
inotify
设置为true，将自动发现媒体目录中的新文件

3、你可以选择让minidlna随机启动

sudo update-rc.d minidlna defaults

4、启动minidlna服务

sudo service minidlna start

5、当你修改配置文件及媒体资源更新时，需要强制刷新，以便minidlna将最新的媒体文件进行索引

sudo service minidlna force-reload

6、查看资源个数

http://192.168.1.106:8200/

7、取消minidlna的开机自动启动

sudo update-rc.d -f minidlna remove

8、停止minidlna服务

sudo service minidlna stop

9、停止minidlna所有进程

sudo killall minidlna

10、卸载minidlna

sudo apt-get remove --purge minidlna