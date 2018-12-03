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
```
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
```

### Ubuntu连接网线却连不上网

```shell
sudo vi /etc/NetworkManager/NetworkManager.conf
```
> dns=dnsmasq
> [ifupdown]
> managed=true


### 修改密码
```shell
sudo passwd
```

### Ubuntu18.04 静态ip
```shell
$ sudo vi /etc/netplan/50-cloud-init.yaml
# 修改为以下内容
network:
    ethernets:
        enp2s0:
            addresses: [192.168.1.20/24] # 20为ip末尾
            dhcp4: no
            gateway4: 192.168.1.1
            nameservers:
                addresses: [192.168.1.1]
    version: 2

$ sudo netplan apply ##应用修改，不行就sudo netplan  --debug apply。
```

### 挂载并访问iPhone

1.安装libimobiledevice-dev库("-dev"不能少了)
```
sudo apt-get update  (更新一下源,我用的163源)

sudo apt-get install libimobiledevice-dev
```
2.安装ifuse

sudo apt-get install ifuse

3.创建一个挂载点(随便创建，我在/media目录下创建了ｕ目录)

sudo mkdir /media/u

4.使用ifuse挂载

ifuse /media/u

5.使用ls和df检查

ls /media/u

显示以下内容:

AirFair  Downloads      PhotoData  PublicStaging  Recordings
Books     general_storage  Photos     Purchases        report_3K.plist
DCIM     iTunes_Control   Podcasts   Radio


df -h

显示以下内容:

ifuse            13G   13G  289M   98% /media/u

表明已经挂载iphone成功!!!!

6.卸载

fusermount -u /media/u

7.安装其他工具

sudo apt-get install ideviceinstaller

sudo apt-get install libimobiledevice-utils

ideviceinfo可以用来查看iphone的相关信息

8. USB拷贝至U盘
```
sudo mount -t exfat /dev/sdb5 /media/udisk
cd /media/udisk
nohup scp root@192.168.1.21:/var/mobile/Documents/inventor2018.zip /media/udisk/
```

### 出现Permission denied的解决办法
ubuntu安装好后，root初始密码（默认密码）不知道，需要设置。

1. 先用安装ubuntu的时候创建的用户登录到系统
2. 然后输入命令：sudo passwd  摁回车
3. 接下来会提示您：输入新密码，重复输入密码，最后提示您passwd：password updated sucessfully
此时已完成root密码的设置
4. 接着就可以输入命令：su root
即以root的身份登录到系统里面去了，此时你再拷贝文件，就ok啦
