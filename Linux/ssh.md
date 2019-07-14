# ssh

## 端口转发
ssh -i key16730.pem -D 8081 root@206.189.47.212

然后macOs：wifi->open Network Prenferences-> Proxies ->socks Proxy(127.0.0.1:8081)
docker run -e PASSWORD=666666 -p 8388:8388 -p 8388:8388/udp -d --restart always shadowsocks/shadowsocks-libev:latest
**进入容器**
docker exec -it  <containerID> /bin/sh 
ss-server -m aes-256-cfb



## 成功案例
####参考
https://hub.docker.com/u/teddysun/

- 拉取镜像 
```docker pull teddysun/shadowsocks-libev或者docker pull teddysun/shadowsocks-r```
。

### 编写配置文件
- shadowsocks-libev版配置文件请存放在/etc/shadowsocks-libev/config.json 示例
```{
    "server":"0.0.0.0",
    "server_port":9000,
    "password":"ktdcvmi90537543&$%&",
    "timeout":300,
    "method":"aes-256-gcm",
    "fast_open":true,
    "nameserver":"8.8.8.8",
    "mode":"tcp_and_udp",
    # 以下为simple-obfs 配置项 如不启用请注释或删除
    "plugin":"obfs-server",
    "plugin_opts":"obfs=tls"
}```

- shadowsocks-r版配置文件请存放在/etc/shadowsocks-r/config.json 示例:
```{
    "server":"0.0.0.0",
    "server_ipv6":"::",
    "server_port":9000,
    "local_address":"127.0.0.1",
    "local_port":1080,
    "password":"ktdcvmi90537543&$%&",
    "timeout":120,
    "method":"aes-256-cfb",
    "protocol":"origin",
    "protocol_param":"",
    "obfs":"plain",
    "obfs_param":"",
    "redirect":"",
    "dns_ipv6":false,
    "fast_open":true,
    "workers":1
}```


### 启用docker

- shadowsocks-libev版:

```$ docker run -d -p 9000:9000 -p 9000:9000/udp --name ss-libev -v /etc/shadowsocks-libev:/etc/shadowsocks-libev teddysun/shadowsocks-libev```

- shadowsocks-r版：
```docker run -d -p 9000:9000 -p 9000:9000/udp --name ssr -v /etc/shadowsocks-r:/etc/shadowsocks-r teddysun/shadowsocks-r```