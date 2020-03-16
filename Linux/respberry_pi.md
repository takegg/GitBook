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
static ip_address=192.168.1.190
static routers=192.168.1.1
static domain_name_servers=114.114.114.114


#profile static_wlan0 #备选
#static ip_address=192.168.123.190
#static routers=192.168.123.1
#static domain_name_servers=114.114.114.114
```
9. 更换源
```
国内源 mirrors.ustc.edu.cn
改/etc/apt/sources.list
改/etc/apt/sources.list.d/raspi.list


刷新
sudo apt update
sudo apt upgrade
sudo apt dist-upgrade
sudo rpi-update
```

# 安装docker
```bash
sudo apt update
sudo apt upgrade
curl -sSL https://get.docker.com | sh
sudo usermod -aG docker pi
logout
groups

更换源
编辑/etc/docker/daemon.json
{
  "registry-mirrors" : [
    "http://ovfftd6p.mirror.aliyuncs.com",
    "http://registry.docker-cn.com",
    "http://docker.mirrors.ustc.edu.cn",
    "http://hub-mirror.c.163.com"
  ],
  "insecure-registries" : [
    "registry.docker-cn.com",
    "docker.mirrors.ustc.edu.cn"
  ],
  "debug" : true,
  "experimental" : true
}

docker run hello-world
```

# docker install gitlab
```
不能web访问
sudo docker run -i \
    --hostname 192.168.1.190 \
    --publish 443:443 --publish 80:80 --publish 2222:22 \
    --name gitlab \
    --restart always \
    --volume /srv/gitlab/config:/etc/gitlab \
    --volume /srv/gitlab/logs:/var/log/gitlab \
    --volume /srv/gitlab/data:/var/opt/gitlab \
    --volume /srv/gitlab/logs/reconfigure:/var/log/gitlab/reconfigure \
    ulm0/gitlab
// Docker运行Gitlab，并使用非22标准ssh端口clone项目
git clone ssh://git@192.168.1.190:222/root/testobj.git 
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
# octopi 安装 desktop 无法登陆
```
sudo apt-get install lxde
startlxde
```

# docker install octopi
```
docker run \
  --device=/dev/video0 \
  -p 81:80 \
  -v /mnt/data:/data \
  nunofgs/octoprint
```
# apt-get update “the following signatures couldn’t be verified because the public key is not available”
```
[chris@server ~]$ sudo apt-key adv --keyserver hkp://keys.gnupg.net:80 --recv-keys EB3E94ADBE1229CF
这样将多条密钥添加
尝试使用的备用服务器是：

hkp://keys.gnupg.net:80
hkp://pgp.mit.edu:80
hkp://sks-keyservers.net:80
hkp://keyserver.pgp.com:80
```

# 界面root权限
```
sudo pcmanfm
```

#