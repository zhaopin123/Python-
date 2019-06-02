#02-字符编码
"""
##1.什么是字符串
序列，有序，不可变的
用单引号或者双引号括起来的任意字符集

##2.字符
a.普通字符：‘23’，‘dsff','字典'
b.转义字符：\n,\t,\',\",\\
阻止转义：r
"""

##3.字符编码
"""
python中的字符采用的是Unicode编码

a.什么是编码
就是数字和字符的对应关系，其中字符对应的数字就是字符的编码

b.编码方式
ASCII码表：针对数字字符、字母字符、英文中常用的符号进行编码
          采用一个字节对字符编码（128个字符）
Unicode码：Unicode码包含了ASCII码，同时对所有语言对应符号进行编码
          采用两个字节进行编码，能编码65536个字符
          中文：4E00-9FA5
          
c.两个函数
chr(编码值) - 将编码转换成字符          
ord(字符) - 获取字符对应的编码值

d.可以将字符编码放到字符串中便是一个字符：\\u + 四位编码
"""
```
print(chr(0xd400))
print(ord('余'))
# d.可以将字符编码放到字符串中便是一个字符：\u + 四位编码
print('hsh\ue12dnf')
```
"""

#03-获取字符串中的字符

一旦一个字符串确定，那么每个字符位置确定，而且每个字符对应一个下标，
用来表示其位置和顺序

##1.下标（索引）
每个字符都有一个下标，代表其位置
下标范围：0~ 字符串长度减一，0代表第一个字符
         -1 ~ -字符串长度， -1代表最后一个字符的位置
"""
```
'abc' # a:0/-3   b:1/-2
'abc\n23'   # 1:4/-3
```
"""
##2.获取单个字符
语法：字符串[下标] - 获取字符串中，指定下标对应指定字符
说明：字符串 - 可以是字符串常量，也可以是变量
    下标 - 字符下标，不可越界
"""
```
str1 = 'hello python'
print(str1[6],str1[-6],str1[-2])
# print(str1[13]) IndexError: string index out of range
```
"""
##3.获取部分字符
语法：字符串【开始下标：结束下标：步长】
说明：字符串 - 可以是字符串常量，也可以是变量
      开始下标、结束下标 - 下标值
      步长 - 整数
功能:
从开始下标开始获取到结束下标前为止，每次下标值增加步长的值
 
注意;
当步长是正数，从前往后取，开始下标在前面
当步长是负数，从后往前取，开始下标在后面

结束下标对应的值取不到
"""
```
str1 = '1234567890'
print(str1[0:6:2]) #135
print(str1[-1:6:-1]) #098
```
"""
方法2：字符串【开始下标：结束下标】 相当于步长为1

"""
```
str1 = 'asj34nc'
print(str1[-1:3]) #'' -空串
print(str1[3:-1])#34n
```
"""
获取部分字符，省略下标
开始下标和结束下标都可以省略
a.开始下标省略
步长正数，从开头往后获取
步长负数，从结尾往前获取
"""
```
str1 = 'asj34nc'
print(str1[:3:1])
print(str1[:3:-1])
```
"""
b.结束下标省略
步长正数，从开始下标获取到结束
步长负数，从开始下标向前获取到开头
"""
```
print(str1[4:])  #4nc
print(str1[::-1]) #字符串倒叙
```

"""

#04-字符串相关运算
##1.+
字符串1 + 字符数2  将两个字符串拼接在一起产生一个新的字符串

1注意：加号两边都必须是字符串
"""
```
str1='123'
str2='abc'
print(str1 + str2)
```
"""
##2.*
字符串 * n(正整数)：字符串的内容重复n次，产生一个新的字符串

"""
```
str1 = 'sdg'
print(str1*3) #sdgsdgsdg
```
"""
##3.比较运算符：>,<,==,!=,>=,<=
字符串1 == 字符串2

"""
`
print('abc' == 'abc')
`
"""
a.>,<,>=,<=
两个字符串比较大小，从第一位开始，找到一对不同的字符，比较大小

"""
`
print('abc' == 'ad')
`
"""
char = input('请输入一个字符：')
print('是否是字母：','a'<=char<='z' or 'A'<=char<='Z')
print('是否中文：',0x4e00 <= ord(char) <=0x9fa5)
"""
"""
##4.in 和 not in
字符串1 in 字符串2： 判断1是否在2中，结果是布尔值
 字符串1 not in 字符串2： 判断1是否不在2中，结果是布尔值
"""
```
print('abc' in 'abc33jf')
```
"""
##5.len
len(字符串) - 获取字符串中字符个数
"""
```
print(len('dsdsewe3r4')) #10
```
"""
##6.str
str(数据)：将数据转字符串

其他数据转字符串：
所有数据类型都可以转字符串。直接最外面加引号

 系统数据类型名不能用来给变量命名
 
"""
```
str1 = str(100)
print(str1,type(str1))
```
"""
b.字符串转其他类型
转整数: int(纯整数字符串)
转浮点型：float(纯数字字符串)
转布尔：bool(字符串) 只有空串才是False
"""
```
print(int('-123'))
print(float('234'))
print(bool(''))
```
#05-格式字符串

"""
##1.格式字符串
指的是字符串中通过占位符来表示字符串中变化部分，然后通过其他值
给占位符赋值
语法：
含有格式占位符的字符串 % （占位符的值）

说明：格式占位符有固定的写法，可以有多个
     % - 固定写法
    （）- 里面值的个数和类型要和前面格式占位符对应
##2.常见占位符
%d - 整数
%s _ 字符串
%f - 小数
%c - 字符
"""
```
name = input('请输入姓名:')
message = '%s今年%d岁，体重:%.1fkg' % (name,15,65)
print(message)
```
#06-字符串常用方法
"""
1.字符串.capitalize() - 字符串首字母转大写
"""

```
str1 = 'hello'
new_str = str1.capitalize()
print(new_str)
```
"""
2.字符串对齐
字符串.center(width,fillchar) - 居中
字符串.ljust(width,fillchar) - 左对齐
字符串.rjust(width,fillchar) - 右对齐
             长度    填充字符
"""
```
import random
num = random.randint(0,20)
print(num)
str1=str(num).rjust(3,'0')
str2='python1808'
new_str=str2+str1
print(new_str)
```
"""
3,join(sep)
字符串1.join(字符串2)
2中出入1
"""
```
str1='**'
str2='abc'
print(str1.join(str2)) #a**b**c
```
"""
4.count(str) - 返回str在string中的次数
"""
```
str1 = 'abdahdaeia'
print(str1.count('a')) #4
```
"""
5.expandtabs(tabsize=8) - 把tab转为空格
"""
"""
6.find(str,beg,end)-检测str是否包含在指定范围beg和end之间
并返回第一个字符下标值

7.  rfind()--和find相同，从右向左找
"""
```
print(str1.find('ah',2,8))
```
"""
8.index(str,beg,end)-和find相同，不在指定范围报错

 9. rindex()-和index相同，从右向左找
"""
```
print(str1.index('ah',2,8))
```
"""
10.isalnum()-字符串中所有字符都为字母或数字则返回True
          否则返回False
"""
```
str1='fiue3抓84rnv'
print(str1.isalnum())
```
"""
11.isalpha()-所有字符都是字母则返回True
          否则返回False
"""
```
str1='fiue384rAnv'
print(str1.isalpha()) #false
```
"""
12.isdigit()-只包含数字则返回True
          否则返回False
   
 13.  isnumeric()     只包含数字则返回True
          否则返回False ,可以中文数字 
"""
```
print(str1.isdigit()) #False
print(str1.isnumeric())
```
"""
14.islower()-字符串包含字母且都是小写则返回True
          否则返回False
"""
```
str1 = 'sue364vvuh'
print(str1.islower())
```
"""
15.isupper()-字符串包含字母且都是大写则返回True
          否则返回False
"""
```
str1 = 'SCSUE34784CH'
print(str1.isupper())
  ```
"""
16.isspace()-只包含空白....
"""

"""
17.istitle()-是标题化则返回True，否则返回False
18.title()-标题化
"""
```
str1 = 'Hello World'
print(str1.istitle())
str2 = 'asnw dwnw'
print(str2.title())#Asnw Dwnw
```
"""
19.len()-返回字符串长度
"""
```
str1 = 'sdnjeee'
print(len(str1))
```
"""
20.lower()-大写转小写
21.upper()-小写转大写
"""
```
str1 = 'DWENmidje'
print(str1.lower())#dwenmidje
print(str1.upper())#DWENMIDJE
```
"""
22.lstrip()-去掉左边空格或指定字符
23.rstrip()-末尾
24.strip()-前后
"""
```
str1 = '  ddjwui3  '
str2 = 'eejici'
print(str2.lstrip('e'))
print(str1.strip())
```
"""
25.split(str='',num=|num=)-以指定字符分割字符串，返回列表
26.splitlines([true/false])-按行分隔，true保留换行符
"""
```
str1 = 'ci cedn ewjuwn e'
print(str1.split())#['ci', 'cedn', 'ewjuwn', 'e']
str2 = '''diecidi
3dusefi
'''
print(str2.splitlines(True))#['diecidi\n', '3dusefi\n']
```
"""
27.startswith(str,beg,end)-检查指定范围是否以指定字符开头
28.endswith(str,beg,end)- ...结尾 
"""
```
str1 = 'aseyobjadd'
print(str1.startswith('e',2,5))
print(str1.endswith('d',4,9))
```
"""
29.swapcase()-大写转小写，小写转大写
"""
```
str1 = 'sdcdeiIWDCoco'
print(str1.swapcase())#SDCDEIiwdcOCO
```
"""
30.translate(table,deletechaes='')根据 str 给出的表(包含 256 个字符)转换 string 的字符, 
要过滤掉的字符放到 deletechars 参数中
"""
```
#from fnmatch import translate
#print(translate('d'))
```
"""
31.zfill(width)-返回指定长度字符串，右对齐，前面填充0
"""
```
str1 = 'sxhwu'
print(str1.zfill(8))#000sxhwu
```
"""
32.isdecimal()-检查字符串是否只包含十进制字符，
            如果是返回 true，否则返回 false
"""
`
print('cwdn7373'.isdecimal())
`
33.translate(old,new,str)
建设一个映射表，将表中对应字符映射到字符串中替换对应字符，str表示需要删除的字符表
```
str1 = 'dheu36hf74b'
trantab = str.maketrans('abcdef','123456','yux')
print(str1.translate(trantab))  #4h536h6742
```
























































