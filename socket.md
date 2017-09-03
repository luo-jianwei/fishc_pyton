Socket Server
```
#!/usr/bin/python3
# coding: utf-8

import socket

HOST = '0.0.0.0'
PORT = 18044

s = socket.socket()
s.bind((HOST,PORT))
s.listen(1)

conn,addr = s.accept()

while True:
    print('Connected by',addr)
    data = conn.recv(1024)
    if not data:break
    conn.sendall(data.upper())
    print('Received :',data)
conn.close()

```
Socket Clinet
```
#!/usr/local/bin/python3
# coding:utf-8

import socket

HOST = '192.168.0.211'
PORT = 18044

try:
    c = socket.socket()
    c.connect((HOST,PORT))
except ConnectionRefusedError as reason:
    print('conncet error :',reason)

while True:
    user_input = input('Please input something:').strip()
    if user_input == 'exit':break
    c.sendall(bytes(user_input,encoding='utf-8'))
    data = c.recv(1024)
    print('Received',repr(data))
c.close()
```
