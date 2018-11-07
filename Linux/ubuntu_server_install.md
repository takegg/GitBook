# ubuntu_server_install

## 挂载exfat
```shell
$ sudo apt-get install exfat-fuse exfat-utils
$ sudo mkdir /media/exfat
$ sudo mount -t exfat /dev/sdc1 /media/exfat
$ sudo umount /dev/sdc1 # 卸载U盘
```