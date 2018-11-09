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
```

## 设置静态IP
1. - 编辑/etc/network/interfaces文件：
```shell
    1.vim  /etc/network/interfaces
    //可以看到如下内容
    # The primary network interface
    auto eth0
    #iface eth0 inet dhcp //dhcp为自动的，将这行注释掉

    2.在上述文件中添加如下内容：
    iface eth0 inet static  //static为静态的
    address 192.168.3.101   //ip地址
    netmask 255.255.255.0   //子网掩码
    gateway 192.168.3.1     //网关
    broadcast 192.168.3.255 //广播
    dns-nameservers 10.0.208.1// 设置dns服务器地址(bate)

    3.编辑/etc/resolv.conf，设置相应的DNS
    nameserver 202.96.134.133
    #nameserver 8.8.8.8 //谷歌dns解析，但是速度较慢
    4. 重启网卡
    /etc/init.d/networking restart
```
2. 设置动态IP
```shell
    1. 修改/etc/network/interfaces
    //修改成如下内容
    auto eth0
    iface eth0 inet DHCP 

    2. 重启网卡
    /etc/init.d/networking restart
```

## ubuntu 终端乱码问题解决方案

- 第一种解决方案：改成全英文环境来解决乱码 ：

    用vim配置语言环境变量

    vim /etc/environment
    改成：

    LANG=”en_US.UTF-8″
    LANGUAGE=”en_US:en”
    sudo vim /var/lib/locales/supported.d/local
    改成

    en_US.UTF-8 UTF-8
    保存后，执行命令：

    sudo locale-gen
    sudo vim /etc/default/locale
    修改为：

    LANG=”en_US.UTF-8″
    LANGUAGE=”en_US:en”

    重启Ubuntu Server

    sudo reboot
    至此 方格乱码解决

- Ubuntu默认的中文字符编码

    Ubuntu默认的中文字符编码为zh_CN.UTF-8，这个可以在

    /etc/environment中看到：
    sudo gedit /etc/environment
    可以看到如下内容：

    PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games"
    LANG="zh_CN.UTF-8"
    LANGUAGE="zh_CN:zh:en_US:en"
    第二行即是默认的中文字符编码。注：可以通过这里修改默认的中文编码字符，比如修改为：zh_CN.GBK。

    二. 添加中文字符编码的方法
    1. 直接使用locale-gen
    在终端输入命令：
    sudo locale-gen zh_CN.GB18030
    即可完成中文字符集的添加。完成后可以转到
    /usr/lib/locale/，下面已经有一个zh_CN.gb18030文件夹；在超级终端输入命令：

    gedit /var/lib/locales/supported.d/local，可以发现文件中多了一行：zh_CN.GB18030 GB18030。说明添加成功。

    1. 通过修改/var/lib/locales/supported.d/local文件
    在终端输入命令行
    sudo gedit /var/lib/locales/supported.d/local
    可以看到如下内容：

    zh_CN.UTF-8 UTF-8
    en_US.UTF-8 UTF-8
    在文件尾添加中文字符集

    zh_CN.GBK GBK

    保存后退出。在终端输入命令：

    sudo dpkg-reconfigure locales




    Generating locales...
    en_AU.UTF-8... done
    en_BW.UTF-8... done
    en_CA.UTF-8... done
    en_DK.UTF-8... done
    en_GB.UTF-8... done
    en_HK.UTF-8... done
    en_IE.UTF-8... done
    en_IN.UTF-8... done
    en_NZ.UTF-8... done
    en_PH.UTF-8... done
    en_SG.UTF-8... done
    en_US.UTF-8... done
    en_ZA.UTF-8... done
    en_ZW.UTF-8... done
    zh_CN.GBK... done
    zh_CN.UTF-8... up-to-date
    zh_HK.UTF-8... done
    zh_SG.UTF-8... done
    zh_TW.UTF-8... done
    Generation complete.
    即可生成相应文件：/usr/lib/locale/zh_CN.gbk/

    最后重启ubuntu。


    ### 修改密码
    ```shell
    sudo passwd
    ```
