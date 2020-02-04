# respberry_pi

# install 
1. pi4 支持fat32 macOS上格式化dos-fat
2. 下载NOOBS解压内容->SD卡
3. 按引导安装
4. 设置无HDMI的VNC显示
```
sudo raspi-config
选7（Advanced Operations）
选5 
选分辨率，可选最大
```
5. 支持ExFat
```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install exfat-fuse
sudo apt-get install exfat-utils
未完待续。。。
```
6. 设置Wi-Fi
```
vi /etc/wpa_supplicant/wpa_supplicant.conf
按优先顺序排
```
7. 静态IP
```s
sudo vi /etc/dhcpcd.conf

# wlan0无线，eth0有线

interface wlan0 #首选
static ip_address=192.168.123.190
static routers=192.168.123.1
static domain_name_servers=114.114.114.114

profile static_wlan0 #备选
static ip_address=192.168.1.190
static routers=10.246.224.1
static domain_name_servers=114.114.114.114
```
# mac下挂载sd卡文件
1. 只读sd卡
https://piratefache.ch/mount-raspberry-pi-sd-card-on-mac-os/
brew cask install osxfuse  
brew install ext4fuse
2. 读写
安装Fuse Ext2详见https://github.com/alperakcan/fuse-ext2
```
brew tap homebrew/cask
brew tap
brew cask install osxfuse
新建/tmp/ext4/script.sh文件夹不能错
chmod +x script.sh
./script.sh
查询磁盘
diskutil list
挂载
sudo mkdir /Volumes/raspberry
sudo fuse-ext2 /dev/disk2s2 /Volumes/raspberry -o rw+ 
卸载
sudo umount /Volumes/raspberry
```
