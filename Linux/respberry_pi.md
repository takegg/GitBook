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