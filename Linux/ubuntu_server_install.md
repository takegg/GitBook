# ubuntu_server_install

## 挂载exfat
```shell
$ sudo apt-get install exfat-fuse exfat-utils
$ sudo mkdir /media/exfat
$ sudo mount -t exfat /dev/sdc1 /media/exfat
$ sudo umount /dev/sdc1 # 卸载U盘
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