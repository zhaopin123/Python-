#01-耗时操作

一个进程默认有一个线程，这个线程叫主线程。默认情况下，所有的代码都是在主线程中执行的
```
import time, datetime

def download(film_name):
    print('开始下载:%s' % film_name, datetime.datetime.now())
    time.sleep(5)   # 程序执行到这个地方，线程会阻塞5秒(停5秒)，再执行后面的代码
    print('%s下载结束' % film_name, datetime.datetime.now())

if __name__ == '__main__':
    # 在主线程中下载两个电影
    download('小黄人')
    download('地心游记')
```

#02-多线程

python中提供了threading模块，来支持多线程技术

默认创建的线程叫主线程，其他的线程叫子线程。如果希望代码在子线程中执行，必须手动创建线程对象
```
import threading
import time, datetime


def download(film_name):
    print('开始下载:%s' % film_name, datetime.datetime.now())
    time.sleep(5)   # 程序执行到这个地方，线程会阻塞5秒(停5秒)，再执行后面的代码
    print('%s下载结束' % film_name, datetime.datetime.now())
    print('下载%s:'%film_name,threading.current_thread())

if __name__ == '__main__':
    # download('小黄人')
```

 1.创建线程对象
    a.
    Thread - 线程类
    b.
    Thread(target=函数名,args=参数列表) - 直接创建线程对象, 返回线程对象
    函数名 = 需要在当前创建的子线程中执行的函数变量
    参数列表 = 元祖，元祖的元素就是调用函数的时候给函数传递的参数

  ```
    t1 = threading.Thread(target=download, args=('小黄人',))
    t2 = threading.Thread(target=download, args=('地心游记',))

    # 2.在子线程中执行任务
    在这儿就是调用t1对应的线程中调用download函数，并且传递一个参数'小黄人'

    t1.start()
    t2.start()
```

#03练习
```
import requests
from threading import Thread


def download(url: str):
    """下载函数"""
    image_data = requests.get(url).content
    file_name = url.split('/')[-1]
    with open('images/'+file_name, 'wb') as f:
        f.write(image_data)

# 1.下载接口对应的数据
# url = 'https://www.apiopen.top/satinApi?type=1&page=1'
# data_dict = requests.get(url).json()
# datas = data_dict['data']
# for dict1 in datas:
#     # 拿到一个图片地址，就为它创建一个线程对象，用来在子线程中下载这张图片
#     t = Thread(target=download, args=(dict1['profile_image'],))
#     t.start()
#
# print('下载完成')


# 使用正则获取数据
import re
url = 'https://www.apiopen.top/satinApi?type=1&page=1'
text = requests.get(url).text

all_profile_image = re.findall(r'"profile_image":"(.+?)",', text)
for image_url in all_profile_image:
    Thread(target=download, args=(image_url,)).start()
```

#04-线程类的子类

from threading import Thread, current_thread


创建子线程，除了直接创建Thread的对象，还可以创建这个类的子类对象

注意：一个进程中有多个线程，进程会在所有的线程都结束才会结束;
     线程中的任务执行完了，线程就结束



## 1.声明一个类继承Thread
```
class DownloadThread(Thread):
    # 想要给run方法传递数据，通过添加对象属性来传
    def __init__(self, file_name):
        super().__init__()
        self.file_name = file_name
```
    ## 2.重写run方法
```
    def run(self):
        # 这个方法中的代码会在子线程中执行
        print('开始下载: %s' % self.file_name)
```

## 3.创建线程对象
```
t1 = DownloadThread('小黄人')
# 4.通过线程对象调用start在子线程中执行run方法
t1.start()
# t1.run()   # 直接调用run方法，会在主线程中执行
```

#05join函数
```
from threading import Thread
import time,datetime,random

线程对象.join() - 等待线程对象中的任务执行完成



class Download(Thread):
    def __init__(self, film_name):
        super().__init__()
        self.film_name = film_name

    def run(self):
        print('开始下载:%s' % self.film_name)
        a = random.randint(5, 12)
        time.sleep(a)
        print('%s开始结束' % self.film_name, '耗时%d秒' % a)


if __name__ == '__main__':
    t1 = Download('小黄人')
    t2 = Download('地心游记')
    time1 = time.time()
    t1.start()
    t2.start()

    # t1和t2中的任务都执行完成后才执行后面的代码
    t1.join()
    t2.join()

    time2 = time.time()
    print('总共时间:', time2 - time1)
```

#06-数据共享

import time, threading

注意：当多个线程同时对同一个数据进行操作的时候，可能会出现数据混乱

多个线程对一个数据进行操作，一个线程将数据读出来，还没来得及存进去；
另一个线程又去读了，这个时候就可能产生数据安全隐患 - 解决问题的方案就是加锁

Thread - 线程类(创建子线程)
Lock - 锁(创建锁对象)


```
class Account(object):
    def __init__(self, balance, name):
        self.balance = balance   # 余额
        self.name = name
        self.lock = threading.Lock()   # 创建锁对象

    def save(self, num):
        """存钱"""
        print('开始存钱')
        # 加锁
        self.lock.acquire()
        old_balance = self.balance
        time.sleep(5)
        self.balance = old_balance + num
        print('存钱成功！')
        # 解锁
        self.lock.release()

    def draw(self, num):
        """取钱"""
        # 加锁
        print('开始取钱!')
        self.lock.acquire()
        old_balance = self.balance
        time.sleep(4)
        self.balance = old_balance - num
        print('取钱成功!')
        # 解锁
        self.lock.release()


acount1 = Account(1000, '余婷')

# 支付宝存钱
t1 = threading.Thread(target=acount1.save, args=(1000,))
# 银行卡取钱
t2 = threading.Thread(target=acount1.draw, args=(500,))

t1.start()
t2.start()

t1.join()
t2.join()
print(acount1.balance)
```


#07client
```
import socket

client = socket.socket()
client.connect(('10.7.187.149', 9000))
while True:
    message = input('自己:')
    client.send(message.encode('utf-8'))
```

#08-server
```
import socket
from threading import Thread

class ConversationThread(Thread):
    def __init__(self, conversation, addr):
        super().__init__()
        self.conversation = conversation
        self.addr = addr

    def run(self):
        while True:
            message = self.conversation.recv(1024).decode('utf-8')
            print(self.addr, ': ' + message, sep='')


server = socket.socket()
server.bind(('10.7.187.149', 9001))
server.listen(512)
while True:
    conversation, addr = server.accept()

    # 给服务器发送请求的客户端建立的连接创建一个子线程。在子线程中去处理每个请求
    t = ConversationThread(conversation, addr)
    t.start()
```












