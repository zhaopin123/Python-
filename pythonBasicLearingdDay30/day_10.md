#02-生成式
##1.生成式

1.(表达式 for 变量 in 序列 ) -->展开：
                                def func():
                                for 变量 in 序列
                                yeild 表达式

表达式的结果就是每次循环生成器产生的数据
这儿的for循环可以控制产生的次数和值
```
gen1 =(x*10 for x in range(4))
print(next(gen1))
```

格式2 
（表达式 for 变量 in 序列 if 条件语句）- >展开：
                                            def func():
                                                for 变量 in 序列
                                                    if 条件语句
                                                        yeild 表达式
```
gen2 =( x for x in range(10) if x % 2)
print(next(gen2))#1
print(next(gen2))#3
print(next(gen2))#5

re = list( x for x in range(10) if x % 2==0)
print(re)
```
```
交换字典中键值对
dict1 = {'a':1,'b':2}
dict2=dict((value,key)for key,value in dict1.items())
print(dict2)
print(dict1.items())
```

#03-模块的使用
python中一个py文件就是一个模块

##2.怎么关联多个模块
方式1：
import 模块名  - 将指定模块导入当前模块中（模块名就是py文件名），导入所有

说明：
a.执行import的时候，实质会进入py文件中去执行其中代码
b.import导入模块的时候会检查之前是否已经导入过，如果已经导入，就不在导入
c.通过impotrt去导入一个模块后，可以通过 模块名.全局变量 去使用模块内容

```
import test1

 使用test1中的变量
a = test1.test1_a
print('当前',a)

 调用test1中的函数
test1.test1_func1()
```

方式2 ：
from 模块名 import 函数名/变量名-导入模块中指定的变量或模块

说明：
a.执行到导入模块语句时，还是会执行模块所有语句
b.还是会查重
c.只能使用指定变量或函数，能直接使用，不用加模块名
d.import后面可以使用逗号将多个变量隔开，也可以使用*将所有全局变量一起导入
```
from test2 import test2_a,test2_func1
# from test2 import *   #同时导入所有全局变量
print('dang',test2_a )
```


函数 - 封装功能 - 
模块- 封装函数或功能
包 - 封装模块 - 文件夹
什么是包：含有__init__.py文件的文件夹

##3.重命名
import 模块名 as 新的模块名
from 模块名 import 变量名 as 新的变量名



##4.包的导入
import 包名 - 会直接执行__init__.py文件中的代码
import 包名.模块名 - 导入包中指定模块

from 包名 import 模块名
from 包名.模块名 import 变量
```
import test
import test.test1
```

#04-选择性导入

在模块中将不需要其他模块导入和执行的代码写到 if__name__'__main__'语句中
这样就可以阻止代码被其他模块执行

原理：每个模块都有一个__name__属性，默认值是对应模块的名字，
    当直接执行的时候，模块的name属性值就会变成__main__，
    当import模块的时候，执行模块的name属性不是__main__，而是默认值

if __name__ == '__main__':#阻止其他模块导入
    写在这得东西不会被其他模块导入
    print(23)

#05-文件操作

##1.数据本地化
就是将数据以文件的形式，存储到本地磁盘中。（程序中变量保存的数据都是村到内存的，当程序运行结束会销毁）

常见的数据本地化方式：二进制文件（包括视频音频压缩包等），普通文本文件，json文件和xml文件，数据库文件

##2.文件操作（读和写）
文件操作的固定步骤：打开文件（新建文件）- 文件操作（读和写）- 关闭文件

##3.打开文件
open(file,mode='r',...,encoding=None) - 返回的是被打开的文件对象（文件句柄）
说明：
file - 字符串；需要打开的文件的路径（可以是绝对路径也可以是相对路径）
        （一般不使用）绝对路径：
        相对路径：相对当前py文件对应的目录
                ./--当前目录（./可以省略）aaa.txt 或者 ./aaa.txt
                ../  --当前目录的上层目录
                .../ -- 当前...上上层目录

mode - 打开方式；要做不同操作对应的打开方式不一样
        'r' - 默认值，以读的方式打开文件，读出来的是字符串
        ’w'- 以写的方式打开文件
        'rb'/'br' - 以读的方式打开，读出来的是二进制
        'wb'/'bw' -以写的方式打开，二进制写入
        'a' - 以写的方式，追加
        '+' - 以读和写方式打开

encoding - 文本文件的编码方式，一般赋值为'utf-8'
            utf-8 - 支持中文编码
            gbk - 不支持中文编码
```
 以只读的方式打开，对f 进行操作就是对文件操作
open('aaa.txt')
open('./aaa.txt')
f = open('./aaa.txt','r',encoding='utf-8')
```

##4.文件的读操作
文件对象.read() - 从文件读写位置开始到文件结尾（默认获取文件中所有内容）
文件对象.readline - 只读一行
```
# content = f.read()
# print(content)

#将文件读完，一行一行读
content = f.read()
str1 = str(content)
for item in str1:
    print(str1)

content = f.readline()
while content:
    print(content)
    content = f.readline()
```

##5.文件的写操作
文件对象.write（字符串）- 将字符中中的内容写到文件中（完全覆盖原文件中的内容）
’w' -完全覆盖
'a' - 在原文件后直接添加
```
f = open('./aaa.txt','a',encoding='utf-8')
f.write('你好')
```

##6.关闭文件
文件对象.close（） - 关闭指定文件

f.close()


open方法的另外一种写法
with open(文件路径，读写方式，encoding=编码方式) as 文件对象：
    文件操作
--> 打开文件，将文件存在文件对象中。当操作完后自动关闭
```
with open('aaa.txt',encoding='utf-8') as f:
    print(f.read())
```

#06-二进制文件读写

普通文本文件亦可以用二进制形式读和写

##2.二进制文件的读
只要将读写方式设置好就可以了，读出来的数据直接是二进制数据
注意：二进制操作不能设置编码方式
```
with open('aaa.txt','rb') as f:
    content = f.read()
    print(content)
```

##3.文件不存在
当以读的方式打开一个不存在的文件，会报错
当以写的方式打开一个不存在的文件不会报错，并且会创建这个文件
```
with open('bb.txt','w'):
    pass
```


指导思想：
1.第一次使用数据时去文件中取数据
2.数据修改后，将新的数据更新的本地文件中

```
#统计程序执行次数，第一次运行打印1 ....
with open('bb.txt','r',encoding='utf-8')as f:
    count = int(f.read())#读到的是字符串
count += 1
with open('bb.txt','w',encoding='utf-8')as f:

    f.write(str(count))#写入方式为字符串
    print('第%d次执行程序' % count)
```










