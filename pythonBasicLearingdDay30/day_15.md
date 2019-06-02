#02-socket编程

socket又叫套接字，指的是实现通信过程的两个端。等待请求的一端叫服务端套接字，
发送请求的一端叫客服端套接字

Python中提供socket模块来支持socket编程

import socket

 服务器套接字
## 1.创建套接字对象
`
socket(family,type)

family,-设置IP类型  AF_INET - ipv4（默认值）  AF_INET - ipv6
type-设置传输类型  SOCK_STREAM - tcp  SOCK_DGRAM-udp

创建一个基于IPV4和tcp的套接字对象
`
server = socket.socket()
`
## 2.绑定IP端口和地址

bind(（ip,端口号）)
ip - 服务器对应的计算机的IP地址，字符串
端口号 - 用来区分计算机上不同服务；是一个数字范围是0-65535，
        但是其中1024以下的是著名端口，用来表示一些特殊的服务，一般不要用
        同一时间一个端口只能对应一个服务
`
server.bind(('10.7.187.130',8082))
`
## 3.开始监听

listen（最大监听数）
最大监听数-用来设置当前服务器一次可以处理多少请求
```
server.listen(100)
print('开始监听')
```
## 4.让服务器一直处于启动状态
`
while True:
  
 接收客户端发送的请求，返回客户端地址和建立的会话；
注意，这段代码会阻塞线程（程序到这回停下来，直到有客户端给当前服务器发送请求为止）
```
    conversation,addr = server.accept()
    print('接受请求',addr)
```
接受消息

    recv(缓存大小) - 获取客户端给服务器发送的数据，返回值是二进制
    缓存大小-决定一次可以接收的最大字节数
```
    re_data = conversation.recv(1024)
    print(re_data)
```
    ## 7.fa送数据

    send(数据)-将制定数据发送给客户端
    数据 - 要求是二进制
    
    字符串（str）转二进制（bytes）
    bytes(字符串,'utf-8')
    字符串.encode（'utf-8'）
    
    二进制转字符串
    str（二进制数据，'utf-8'）
    二进制.decode（'utf-8'）
```
    message = '589554'
conversation.send(bytes(message),encoding='utf-8')
    conversation.send(message.encode(encoding='utf-8'))
```

#03-客户端套接字

import socket
## 创建客户端套接字
`
client = socket.socket()
`
## 2.lianjie服务器

connect(ip,端口)
`
client.connect(('10.7.187.133',8080))
`
## 3.fa送消息
```
while 1:
    message = input()
    client.send(message.encode('utf-8'))

    # 接收消息
    re_data = client.recv(1024)
    print('服务器',re_data.decode('utf-8'))
```
#04-服务器
```
import  socket

server = socket.socket()

server.bind(('10.7.187.130',8824))
server.listen(1024)
while 1:
    conversation,addr = server.accept()

    while 1:
        re_data = conversation.recv(1024)
        # if not re_data:
        #     break
        print('客户端',re_data.decode('utf-8'))
        message = input()
        conversation.send(message.encode('utf-8'))
```

#05-网络请求

import requests

python中做HTTP请求需要一个第三方库；request

get(url,参数字典)-返回响应

 1.向服务器发送get请求
自动拼接url
```
# url = 'https://www.apiopen.top/satinApi?type=1&page=1 '
# response = requests.get(url)
# print(response)
```
```
# 手动拼接url
url = 'https://www.apiopen.top/satinApi'
response = requests.get(url,{'type':1,'page':1})
print(response)
```
# 2.获取响应头
```
header = response.headers
print(header)
```
```
# 获取响应体
# 二进制格式响应头
content = response.content
print(content,(content))
# 获取json格式响应体 - 自动将json数据转换成Python数据
json = response.json()
print(json,type(json))
# 获取字符串格式响应体
text = response.text
print(text,type(text))
```
```
# url = 'https://timgsa.baidu.com/timg?image&quality=80&size=b10000_10000&sec=1543395098&di=2a5bbaa5600097b050ba69a688672de9&src=http://p0.qhimgs4.com/t0112e7ebfdef7f923d.jpg '
url='http://wimg.spriteapp.cn/picture/2018/1114/9be9a9aee81811e8baee842b2b4c75ab_wpd.jpg'
response = requests.get(url)
image = response.content
with open('老王.jpg','wb')as f:
    f.write(image)
```










8.关闭链接
    conversation.close()