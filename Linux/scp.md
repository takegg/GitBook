# scp

### 从本地服务器复制到远程服务器：

(1) 复制文件： 

命令格式： 

scp local_file remote_username@remote_ip:remote_folder 

或者 

scp local_file remote_username@remote_ip:remote_file 

或者 

scp local_file remote_ip:remote_folder 

或者 

scp local_file remote_ip:remote_file 

第1,2个指定了用户名，命令执行后需要输入用户密码，第1个仅指定了远程的目录，文件名字不变，第2个指定了文件名 

第3,4个没有指定用户名，命令执行后需要输入用户名和密码，第3个仅指定了远程的目录，文件名字不变，第4个指定了文件名  

(2) 复制目录： 

命令格式： 

scp -r local_folder remote_username@remote_ip:remote_folder 

或者 

scp -r local_folder remote_ip:remote_folder 

第1个指定了用户名，命令执行后需要输入用户密码； 

第2个没有指定用户名，命令执行后需要输入用户名和密码；

### 从远处复制文件到本地目录

命令：

scp root@192.168.120.204:/opt/soft/nginx-0.5.38.tar.gz /opt/soft/

### 上传本地文件到远程机器指定目录

命令：

scp /opt/soft/nginx-0.5.38.tar.gz root@192.168.120.204:/opt/soft/scptest

### 上传本地目录到远程机器指定目录

命令：

scp -r /opt/soft/mongodb root@192.168.120.204:/opt/soft/scptest

nohup sudo scp -r root@192.168.1.21:/var/mobile/Backups/ /videos/tutorial/electronic/