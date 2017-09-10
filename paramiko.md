### paramiko
- 安装paramiko模块
```
sudo pip3 install pycrypto paramiko
```

- 密码连接
```
#!/usr/bin/python3
# coding: utf-8
import paramiko
import os,sys
host = sys.argv[1]
port = 22
user = 'root'
password = '*****'
cmd = sys.argv[2]
# 绑定实例
s = paramiko.SSHClient()
# 加载本机HOST主机文件
s.load_system_host_keys()
# 允许连接不在know_hosts文件中的主机
s.set_missing_host_key_policy(paramiko.AutoAddPolicy())
# 连接远程主机
s.connect(host,port,user,password,timeout=5)
# 执行命令
stdin,stdout,stderr = s.exec_command(cmd)
# 读取命令执行结果
cmd_result = stdout.read(),stderr.read()
for each_line in cmd_result:
    print(each_line)
s.close()
```
- 密钥连接
```
#!/usr/bin/python3
# coding: utf-8
import paramiko
import os,sys
host = sys.argv[1]
cmd = sys.argv[2]
port = 22
user = 'root'
# 指定私钥位置
pkey_file = '/home/luojianwei/.ssh/id_rsa'
key = paramiko.RSAKey.from_private_key_file(pkey_file
# 绑定实例
s = paramiko.SSHClient()
# 加载本机HOST主机文件
s.load_system_host_keys()
# 允许连接不在know_hosts文件中的主机
s.set_missing_host_key_policy(paramiko.AutoAddPolicy())
# 连接远程主机
s.connect(host,port,user,pkey=key,timeout=5)
# 执行命令
stdin,stdout,stderr = s.exec_command(cmd)
# 读取命令执行结果
cmd_result = stdout.read(),stderr.read(
for each_line in cmd_result:
    print(each_line)
s.close()
```
- 传输文件
```
#!/usr/bin/python3
# coding: utf-8
import paramiko
import os,sys
host = sys.argv[1]
port = 22
user = 'root'
password = 'jianwei.com'
#pkey_file = '/home/luojianwei/.ssh/id_rsa'
#key = paramiko.RSAKey.from_private_key_file(pkey_file)
t = paramiko.Transport(host,port)
t.connect(username=user,password=password)
#t.connect(username=user,pkey=key)
sftp = paramiko.SFTPClient.from_transport(t)
# 获取远程主机文件
sftp.get('/tmp/socket_server.py','/tmp/test.py')
# 拷贝本地文件到远程主角
sftp.put('/tmp/123.txt','/tmp/test.txt')
t.close()
```
