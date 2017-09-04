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

while True:
    conn,addr = s.accept()
    while Ture:
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
### socket多线程
```
#!/usr/bin/python3
# coding: utf-8

import socketserver

class Mysocketserver(socketserver.BaseRequestHandler):
    def handle(self):
        print('Got a new conn from',self.client_address)
        while True:
            data = self.request.recv(1024)
            if not data:break
            print('recv:',data)
            self.request.send(data.upper())

if __name__ == '__main__':
    HOST = '0.0.0.0'
    PORT = 9001
    s = socketserver.ThreadingTCPServer((HOST,PORT),Mysocketserver)
    s.serve_forever()
```
